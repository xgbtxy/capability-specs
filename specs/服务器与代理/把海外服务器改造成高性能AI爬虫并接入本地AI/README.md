# 把海外服务器改造成高性能 AI 爬虫并接入本地 AI

把一台已有的海外 Linux 服务器收敛成单用途爬虫节点：移除旧代理服务，部署完整 Crawl4AI，按真实负载调优，再通过持久 SSH 通道、crawlerctl 和 Skill 交给本地 AI 使用。

这组能力追求的不是“能请求一个网页”，而是让 AI 稳定获得这些能力：

- JavaScript 渲染后的正文和干净 Markdown
- 单页、批量、站点深爬和流式结果
- CSS / XPath / JSON Schema 等结构化提取
- 截图、PDF、会话、Cookie、Header 和代理参数
- 原生 Crawl4AI 请求 JSON 与任意 API 端点
- 可重复部署、可回滚、可基准测试的服务器运行环境

## 适合

- 已有一台可以 SSH 登录的海外 Linux 服务器
- 希望服务器不再做代理，只专门负责网页爬取
- 希望本地 AI 不经 MCP，也能用 CLI 和 Skill 完整调用
- 动态网页、文档站、RAG 采集、批量 URL 或深度爬取

## 不适合

- 只需要搜索结果，不需要抓取已知 URL
- 需要把爬虫 API 直接开放给多个不可信租户
- 没有目标网站授权，或目标站条款明确禁止当前采集方式
- 想用一个固定并发数字适配所有服务器和网站

## 推荐工具

- Crawl4AI：[Self-Hosting](https://docs.crawl4ai.com/core/self-hosting/) / [Deep Crawling](https://docs.crawl4ai.com/core/deep-crawling/) / [Docker Migration](https://github.com/unclecode/crawl4ai/blob/main/deploy/docker/MIGRATION.md)
- Docker Compose：[Docker Compose](https://docs.docker.com/compose/)
- OpenSSH：[OpenSSH](https://www.openssh.com/)
- Python：用于实现本地 crawlerctl 统一入口
- AI Skill：用于把用户意图稳定路由到 crawlerctl

## 事实来源

- Crawl4AI 的接口与部署行为以所选版本的官方文档、迁移说明、OpenAPI、Schema 和运行时源码为准
- 已经成功跑通的 2 vCPU / 2 GB 部署、性能数字和能力清单见 [实战记录.md](./实战记录.md)
- 服务器地址、凭据和目标站秘密不属于能力事实，不进入本仓库
- 机器规格、Crawl4AI 版本或目标负载不同时，把未知项标记为 missing，并重新验证，不沿用旧结论

## 最小使用方式

1. 盘点服务器资源、服务和监听端口，备份后移除旧代理
2. 固定 Crawl4AI 版本，用可重建的派生镜像启用所需完整能力
3. 用冷启动、热缓存、并发和长任务实测找到性能拐点
4. 建立本地持久 SSH 通道，并配置 crawlerctl
5. 安装海外爬虫 Skill，再用一个全新 AI 会话做隐式调用验收

## 包含的能力

- [01-确认服务器现状并清理旧代理服务](./01-确认服务器现状并清理旧代理服务)
- [02-用Docker部署Crawl4AI并建立完整API](./02-用Docker部署Crawl4AI并建立完整API)
- [03-按真实负载调优浏览器并发](./03-按真实负载调优浏览器并发)
- [04-建立持久SSH通道和crawlerctl入口](./04-建立持久SSH通道和crawlerctl入口)
- [05-把爬虫能力接入AI并做新会话验收](./05-把爬虫能力接入AI并做新会话验收)

## 完成标准

- 服务器只保留预期的 SSH 和爬虫监听，旧代理服务不再运行
- 容器健康、无 OOM、无意外重启，资源限额与机器规格匹配
- JavaScript、深爬、批量、流式、截图/PDF、结构化提取和失败结果均通过活体验证
- crawlerctl 的友好命令和原生透传命令都能使用
- 全新 AI 会话在不点名 Skill 的情况下，也能识别网页爬取意图并完成调用

## 反馈与维护位置

- 新的真实部署结果追加到 [实战记录.md](./实战记录.md)，并注明机器规格、版本和负载
- Crawl4AI 版本适配变化更新第 02 步
- 性能拐点与压测方法变化更新第 03 步
- AI 误触发、漏触发或命令路由问题更新第 05 步
- 未经活体验证的建议只能标记为待验证，不能写成已部署事实
