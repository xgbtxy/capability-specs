# 建立持久 SSH 通道和 crawlerctl 入口 SPEC

## 目标

本地 AI 只需要调用 crawlerctl，不需要知道 SSH 参数、服务器地址、Token 或 HTTP 细节；高级场景又能直接透传 Crawl4AI 原生请求。

## 1. 通道模型

数据路径：

    AI -> crawlerctl -> http://127.0.0.1:LOCAL_TUNNEL_PORT
       -> persistent SSH local forward
       -> server 127.0.0.1:REMOTE_CRAWLER_PORT
       -> Crawl4AI

这条路径限制的是网络暴露面，不限制 Crawl4AI API 能力。

先在服务器确认：

    ss -lntp

Crawl4AI 必须只监听服务器回环地址。再从本地建立通道：

    ssh -N -T -L 127.0.0.1:LOCAL_TUNNEL_PORT:127.0.0.1:REMOTE_CRAWLER_PORT -p SSH_PORT -i SSH_KEY_PATH -o ExitOnForwardFailure=yes -o ServerAliveInterval=30 -o ServerAliveCountMax=3 SSH_USER@SERVER_HOST

在 PowerShell 自动化中建议使用参数数组，避免字符串拼接和转义问题。

## 2. 持久化要求

通道管理器至少做到：

- 本机登录后自动启动，或由 crawlerctl status 按需启动
- 使用密钥实现非交互登录
- 本地只监听 127.0.0.1
- ExitOnForwardFailure 防止“进程存在但转发未建立”
- SSH keepalive 检测失效链路
- 进程退出后有限退避重连
- 能区分端口被占用、鉴权失败、服务器离线和 API 未健康
- 提供 start、stop、restart、status 和日志位置

Windows 可用计划任务或用户级后台进程承载，启动时隐藏窗口。不要用每条爬虫命令临时运行一次 ssh。

## 3. crawlerctl 命令契约

至少提供：

    crawlerctl configure
    crawlerctl status
    crawlerctl crawl URL
    crawlerctl batch URL_FILE_OR_JSON
    crawlerctl site START_URL
    crawlerctl run REQUEST_JSON_OR_FILE
    crawlerctl api METHOD PATH BODY_OR_FILE

### configure

保存：

- 本地 endpoint
- Token 的安全引用或私有配置
- 默认超时
- 默认输出目录

配置优先级建议：

1. 当前命令显式参数
2. 环境变量
3. 用户级私有配置
4. 非秘密默认值

配置输出必须遮蔽 Token。

### status

依次检查：

1. 本地端口是否监听
2. SSH 通道进程是否存活
3. /health
4. /monitor/health
5. 当前 API 版本或 Schema 可读

返回机器可解析的退出码和 JSON 摘要。

### crawl

面向单 URL 的友好入口，默认返回：

- success
- url
- final_url
- markdown
- title 或元信息
- error_message
- 产物路径

允许添加等待条件、CSS selector、截图、PDF、Header、Cookie 和代理等常见参数。

### batch

在一个 API 请求或有限数量的批次中发送多个 URL，避免为每页支付海外往返延迟。保留输入顺序，并逐条返回成功或失败。

### site

映射服务器侧 BFS / DFS 深爬，必须支持：

- max_depth
- max_pages
- include / exclude
- same-domain 策略
- streaming
- 每页结果与发现关系

调用方未给上限时，要根据任务明确合理范围；可信 API 可以不硬编码上限，但 AI 不应无意无限遍历。

### run

直接提交完整 CrawlRequest JSON：

- 不建立字段 allowlist
- 不静默删除未知字段
- 服务端验证错误原样返回
- 支持从文件读取，避免 PowerShell 引号破坏 JSON

这是 AI 使用 Crawl4AI 新能力时不必先升级 crawlerctl 的关键入口。

### api

允许指定 HTTP 方法、API 路径、查询参数和 JSON body，用于：

- /schema
- /openapi.json
- /monitor/health
- /execute_js
- hooks 和未来新增端点

只自动处理 endpoint、鉴权、超时、输出和错误格式，不限制 API 路径。

## 4. CLI 实现要求

- Python 标准库或成熟 HTTP 库均可
- 请求和响应统一 UTF-8
- JSON、NDJSON、Markdown、截图和 PDF 能输出到文件
- 大结果默认避免全部塞进 AI 上下文，返回摘要与绝对路径
- HTTP 超时区分连接、首字节和长任务
- 只对传输级临时故障有限重试，不自动重复有副作用的调用
- 目标级 success=false 保持为结果，不误判为 CLI 崩溃
- 非零退出码用于鉴权、无效请求、通道或服务故障
- --version 可查看 crawlerctl 版本

## 5. 性能验收

使用相同健康检查和热缓存 crawl，对比：

1. 每次新建 SSH 的临时桥接
2. 已建立的持久 SSH 通道

已验证场景：

| 路径 | health | 热缓存 crawl |
| --- | ---: | ---: |
| 每命令新建 SSH | 约 2131 ms | 约 2935 ms |
| 持久 SSH 通道 | 约 472 ms | 约 809 ms |

因此默认使用持久通道。多个 URL 进一步使用 batch 或 site 摊薄 RTT。

## 6. 故障恢复验收

依次模拟并验证：

- 通道尚未启动
- 本地端口被占用
- SSH 进程被结束
- 服务器重启
- Crawl4AI 容器重启
- Token 错误
- 目标 URL 失败
- 大响应写入文件

每种情况都应返回明确诊断，通道恢复后不要求用户重新配置 endpoint 和 Token。

## 完成标准

- status 能确认通道与服务
- crawl、batch 和 site 可用
- run 能接受 Crawl4AI 当前 Schema 的高级字段
- api 能访问任意现有端点
- Token 不出现在日志和普通状态输出
- 持久通道的同负载延迟明显低于临时桥接
- 通道中断后能自动或一条命令恢复
