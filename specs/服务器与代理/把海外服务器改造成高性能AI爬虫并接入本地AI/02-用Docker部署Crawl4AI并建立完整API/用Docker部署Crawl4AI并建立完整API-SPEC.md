# 用 Docker 部署 Crawl4AI 并建立完整 API SPEC

## 目标

产出一个可以从空服务器重新构建的 Crawl4AI 服务。所有版本适配进入 Dockerfile 和补丁资产，运行容器本身不承载不可追踪的手工修改。

## 执行前必读

- Crawl4AI Self-Hosting 官方文档
- 当前版本的迁移说明
- 当前容器导出的 /openapi.json 与 /schema
- 当前版本容器内与请求校验、provenance、governor、deep crawl 和 hooks 有关的源码
- 上级 environment-setup.md、tools-and-safety.md

已知基线：Crawl4AI 0.9.1 已经完成过本 SPEC 的可信完整部署。版本不同只可复用目标和验证，不可盲目复用补丁行号。

## 1. 建立部署目录与版本清单

推荐服务器目录：

    /opt/overseas-crawler/
      compose.yaml
      .env
      Dockerfile
      patches/
      config/
      data/
      backups/
      DEPLOYMENT.md

DEPLOYMENT.md 至少记录：

- 官方基础镜像版本与 digest
- 派生镜像标签
- 构建时间和补丁摘要
- compose 配置版本
- 当前回滚镜像
- 已执行的验收清单

.env 权限仅限管理员，禁止提交 Git。

## 2. 先运行官方镜像并观察事实

不要先假设官方 API 缺能力。启动固定版本后依次检查：

    GET /health
    GET /monitor/health
    GET /openapi.json
    GET /schema

然后用最小 CrawlRequest 分别测试：

- 普通 HTTPS 页面
- JavaScript
- Header 和 Cookie
- 代理字段
- screenshot 和 pdf
- BFS 或 DFS 深爬策略
- streaming
- execute_js 和 hooks

记录每项是成功、Schema 拒绝、provenance 拒绝、固定上限截断，还是服务实现缺失。

如果当前官方版本已经满足需求，直接使用官方镜像，不为了“定制”而定制。

## 3. 建立可信完整派生镜像

只有官方版本实际拒绝所需能力时才构建派生镜像。派生过程必须：

1. FROM 固定的官方镜像版本或 digest
2. COPY 版本专用补丁脚本或补丁文件
3. 补丁前断言原始代码特征存在
4. 修改后断言目标特征存在且旧限制不存在
5. 对改动的 Python 文件运行编译检查
6. 构建阶段失败时立即退出，不能生成半成功镜像
7. 为派生镜像使用独立标签，例如 overseas-crawler-full:VERSION

### Crawl4AI 0.9.1 已验证改造目标

0.9.x 默认把外部配置作为 UNTRUSTED 输入，强字段会被拦截。单所有者可信入口需要在已经鉴权的请求装载路径中：

- 将 /app/api.py 与 /app/server.py 对请求配置的 provenance 改为 TRUSTED
- 保留 Pydantic 类型和业务校验，不把所有验证整体关掉
- 移除服务器层对 URL 数、请求体、深爬页数、深度、墙钟、队列、hook 数和 hook 超时的固定夹断
- 统一 0 的语义：配置为 0 时代表不设固定上限，不能被 governor 当成零字节
- 允许 execute_js、内部 URL 和按请求控制 TLS 校验
- 保留 bearer token 校验

“不设固定上限”不代表无限内存。容器内存、浏览器并发、调用方超时和目标站速率仍然形成真实资源边界。

### 结果语义

目标网页失败和爬虫服务故障必须分开：

- DNS、目标 4xx/5xx、页面导航失败等目标级错误：HTTP 响应保持可解析，结果中 success=false，并提供 error_message
- 请求 JSON 无效、鉴权失败、服务内部异常：继续使用对应 HTTP 错误

这样 AI 才能读取批量结果中的局部失败，而不会因一个目标失败丢掉整批结果。

## 4. Compose 运行约束

compose 至少表达：

- 只绑定服务器回环地址，例如 127.0.0.1:11235:11235
- API Token 来自私有 env
- restart: unless-stopped
- 健康检查
- 明确的 mem_limit 和 shm_size
- 日志轮转
- 配置、数据和产物卷
- 派生镜像标签，不使用悬空 latest

2 vCPU / 2 GB 的已验证起点：

- 容器内存约 1.56 GiB
- shm 512 MiB
- 为系统、sshd 和 Docker 守护进程保留剩余内存

这只是起点。机器规格不同，必须根据第 03 步实测调整。

## 5. 启动顺序

    docker compose config
    docker compose build --no-cache
    docker compose up -d
    docker compose ps
    docker compose logs --tail 200

检查：

    docker inspect CONTAINER_NAME
    docker stats --no-stream
    ss -lntp

预期 Crawl4AI 只出现在 127.0.0.1:REMOTE_CRAWLER_PORT，不出现在 0.0.0.0 或公网地址。

## 6. 完整能力验收

至少执行并保存摘要：

1. health、monitor/health、openapi.json、schema
2. 普通页面到 Markdown
3. JavaScript 改变 DOM 后再抓取
4. Header、Cookie 和代理参数被服务接受
5. CSS 或 JSON Schema 结构化提取
6. screenshot 和 PDF 产物非空
7. 服务器侧 BFS 深爬
8. streaming 返回逐条 NDJSON
9. execute_js 和 hooks
10. 一个故意失败的目标返回可解析 result.success=false
11. 一个无效请求仍返回正确的 4xx
12. 容器健康、无 OOM、无重启

不要只看 HTTP 200；要核对结果字段、Markdown、记录数和文件内容。

## 7. 回滚

回滚必须能在数分钟内完成：

1. 停止当前 compose 项目
2. 恢复上一份 compose 和 env 引用
3. 启动上一可用镜像标签或 digest
4. 重新跑 health 与最小 crawl
5. 保留失败镜像和日志供诊断，不覆盖证据

## 输出格式

1. 版本和 digest
2. 官方镜像能力矩阵
3. 实际需要的改造项
4. 派生镜像构建结果
5. Compose 资源和监听
6. 十二项活体验收结果
7. 回滚入口
8. missing 与版本升级风险
