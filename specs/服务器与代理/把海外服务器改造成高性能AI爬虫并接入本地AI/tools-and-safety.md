# tools-and-safety

## 工具分工

- Docker Compose：声明镜像、资源、端口、健康检查、卷和重启策略
- Crawl4AI：JavaScript 渲染、Markdown、结构化提取、深爬和高级浏览器能力
- OpenSSH：把只监听服务器回环地址的 API 映射到本地
- crawlerctl：隐藏连接细节，提供友好命令和原生透传
- AI Skill：把自然语言意图映射到 crawlerctl，并告诉 AI 何时使用高级入口

## 完整能力边界

“受限 SSH 通道”只表示 API 不直接暴露公网，并不限制爬虫字段或端点。

在单所有者可信部署中，本地 AI 经过 SSH 通道后应能使用：

- crawl、batch、site 等常用命令
- run 透传任意 CrawlRequest JSON，不设置字段白名单
- api 调用任意已存在的 Crawl4AI API 路径和 HTTP 方法
- Header、Cookie、代理、JavaScript、截图、PDF、深爬和 hooks 等高级参数

如果 API 需要向多个不可信用户开放，不使用此“可信完整”配置，应回到官方安全默认值并建立租户隔离。

## 不能省略的保护

这些保护不降低爬取能力，反而保证长期可用：

- 不把 SSH、API Token、Cookie、代理凭据和私钥写入公开仓库或命令历史
- Crawl4AI API 只监听服务器 127.0.0.1
- 保留 API Token；由 crawlerctl 自动附加
- 所有源码改造进入派生镜像，禁止只在运行中的容器里手改
- 变更前保存 compose、env、镜像标签和旧服务配置
- 设置容器内存与 shm，监控 OOM、重启和浏览器泄漏
- 尊重目标站授权、robots、服务条款、速率和当地法律

## 性能边界

- “并发最大”不等于“吞吐最大”
- 海外往返延迟用持久通道和批量请求摊薄，不靠无限加进程
- 冷启动、热缓存、动态页面、原始 HTML 和深爬要分开测
- 目标站限速、验证码或封禁不能用单机并发硬顶
- 每次升级 Crawl4AI、Chromium 或基础镜像后重跑关键基准
