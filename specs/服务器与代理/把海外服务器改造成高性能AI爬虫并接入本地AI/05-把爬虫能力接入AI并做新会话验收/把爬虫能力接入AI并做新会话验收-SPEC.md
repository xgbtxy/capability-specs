# 把爬虫能力接入 AI 并做新会话验收 SPEC

## 目标

让另一个完全不了解部署历史的 AI，仅靠项目入口就能：

1. 判断任务是否应该使用海外爬虫
2. 找到 crawlerctl
3. 选择 crawl、batch、site、run 或 api
4. 完成任务并验证结果
5. 在需要扩展架构时读到完整部署事实、性能结论和边界

## 三层入口

### 第一层：能力包

本目录是部署、能力、限制、实战结果和验收标准的事实源。另一个 AI 要扩展架构时必须先读：

- README.md
- spec.yaml
- environment-setup.md
- tools-and-safety.md
- 实战记录.md
- 五个步骤的 README.md、spec.yaml 和 SPEC.md

### 第二层：Skill

Skill 只保存稳定路由知识：

- 什么任务触发海外爬虫
- 用户意图映射到哪个 crawlerctl 命令
- 调用前如何检查 status
- 常用参数和结果验证
- 何时切换到 run 或 api
- 能力包事实源路径

Skill 不复制 Token、服务器地址、SSH 密钥和大段版本补丁。

### 第三层：crawlerctl

crawlerctl 是唯一执行入口，负责本地通道、鉴权、HTTP、输出文件和错误格式。Skill 不重新实现网络调用。

## Skill 最小结构

建议安装位置：

    CODEX_HOME/skills/overseas-crawler/SKILL.md

如果 AI 客户端不支持个人 Skill，就在项目 AGENTS.md 中放一条路由规则，指向本能力包和 crawlerctl；不要把整份能力包重复粘贴进 AGENTS.md。

Skill 的 description 必须覆盖这些显式和隐式意图：

- 网页爬取、抓取、采集
- URL 转 Markdown
- JavaScript 动态页面
- 批量 URL
- 整站、栏目、左侧导航全部页面
- 深度爬取
- CSS / XPath / Schema 结构化提取
- 截图或 PDF
- Header、Cookie、代理
- Crawl4AI 高级请求
- 爬虫健康检查

不应触发：

- 只有主题、没有目标 URL 的普通网络搜索
- 不需要网页正文的简单事实查询
- 本地文件解析

## 用户意图到命令的映射

| 用户意图 | 默认入口 | 切换条件 |
| --- | --- | --- |
| 抓一个 URL 到 Markdown | crawlerctl crawl | 需要原生复杂字段时改用 run |
| 抓明确的 URL 列表 | crawlerctl batch | URL 来自站点发现时改用 site |
| 抓栏目、左侧导航或整站 | crawlerctl site | 站点规则特殊时先 crawl 入口页并生成 URL 清单 |
| 发送完整 CrawlRequest | crawlerctl run | 不得删减未知字段 |
| 调 OpenAPI、Schema、execute_js 或 hooks | crawlerctl api | 任意现有 API 路径均可 |
| 检查服务是否可用 | crawlerctl status | 失败时先诊断通道，再诊断容器 |

执行默认规则：

1. 先运行 crawlerctl status
2. 单页用 crawl，多页合并为 batch，站点发现用 site
3. 动态页面确认 JavaScript 后的内容，不只检查 HTTP 状态
4. 大结果写到项目内明确输出目录，返回清单和绝对路径
5. 每页保留 source_url、final_url、标题、抓取时间、success 和 error
6. 失败页可单独重试，不覆盖已成功结果
7. 需要 Crawl4AI 新字段时直接使用 run，不等 CLI 增加选项

## 给另一个 AI 的完整入口 Prompt

把下面文字和具体任务一起交给另一个 AI。先把 CAPABILITY_PACKAGE_PATH 替换为本目录的真实绝对路径。

    你现在可以使用一台已经部署完成的海外 AI 爬虫服务器。

    先完整读取 CAPABILITY_PACKAGE_PATH 下的 README.md、spec.yaml、
    environment-setup.md、tools-and-safety.md、实战记录.md，以及五个编号步骤内的
    README.md、spec.yaml 和 SPEC.md。把它们作为这项任务的事实源，不要猜测缺失信息，
    缺少的输入标记为 missing。

    实际调用统一使用本机 crawlerctl。开始先运行 crawlerctl status。
    单页优先 crawl，明确 URL 列表优先 batch，栏目/左侧导航/整站优先 site；
    需要完整 CrawlRequest JSON 时使用 run，需要任意 Crawl4AI 端点时使用 api。
    run 和 api 是完整能力入口，不要因为友好命令没有某个参数就判定服务器不支持。

    不要输出或写入服务器地址、SSH 密码、API Token、Cookie、代理凭据和私钥。
    大量 Markdown、截图、PDF 和 JSON 写入当前项目的专用输出目录，保留 manifest，
    每页记录源 URL、最终 URL、标题、文件路径、成功状态、错误和抓取时间。

    执行时先做小样本，再做完整批次；完成后验证页面数量、失败清单、Markdown 非空、
    JavaScript 内容、重复 URL、断链和 crawlerctl/容器健康。只有活体验证通过才宣布完成。

    当前具体任务：
    TASK

这个 Prompt 同时适合执行爬取和让 AI 延伸架构。延伸架构时要求 AI 区分：

- 已验证事实
- 当前项目约定
- 新建议
- missing

不得把建议反写成已经部署的事实。

## 文档站左侧导航完整下载 Prompt

下面是常见刚需，可直接替换 URL 和输出目录：

    使用海外爬虫能力，把 START_URL 所属文档栏目左侧导航中的每一篇文档完整下载为 Markdown。

    先读取能力包并运行 crawlerctl status。先抓入口页并渲染 JavaScript，识别左侧导航的
    层级、展开项、懒加载、分页和路由规则；同时检查页面内嵌数据、站点地图和网络返回，
    选择能得到最完整导航 URL 的来源。只采集目标栏目，规范化 URL，去掉锚点、跟踪参数、
    重复项和非正文页面。

    先用 3 至 5 页做样本，验证标题、正文、代码块、表格、图片链接、面包屑和下一层导航。
    样本通过后再批量抓取。动态页面必须以渲染后内容为准；优先 batch 或服务器侧 site，
    需要高级 CrawlRequest 时使用 crawlerctl run。

    输出到 OUTPUT_DIR：
    - 每页一个 UTF-8 Markdown 文件
    - 按导航层级建立目录或用稳定序号保序
    - manifest.jsonl 记录 order、nav_path、title、source_url、final_url、file、
      fetched_at、success、error、content_hash
    - index.md 重建完整导航并链接每个本地文件
    - failed.jsonl 保存失败页和原因

    支持断点续跑；已成功且 content_hash 未变化的页面不要重复覆盖。对失败页有限重试，
    最后核对导航 URL 数、成功文件数、失败数、空正文、重复内容和断链。返回输出目录、
    统计、失败清单和 crawlerctl status，不要只说“已完成”。

## 新会话验收

必须新开一个没有继承当前部署对话的 AI 会话。至少执行四项：

### 1. 隐式单页

只说“把这个 URL 抓成 Markdown”，不说 Skill 名。预期 AI 自动选择海外爬虫、先检查 status，再调用 crawl。

### 2. 隐式文档站

只说“把左侧导航每一页下载成 Markdown”。预期 AI 选择 site 或入口发现加 batch，生成 manifest 和失败清单。

### 3. 高级能力

要求 JavaScript、Header/Cookie、截图或 PDF、结构化提取中的至少两项。预期 AI 能切换到 run，而不是说 CLI 不支持。

### 4. 原生端点

要求读取 Schema 或调用 execute_js。预期 AI 使用 api。

每项验收都检查：

- 实际命令
- 退出码
- 结果字段
- 输出文件
- 页面内容
- status
- 是否泄露秘密

## 通过标准

- 未点名 Skill 也能因 URL 抓取意图自动触发
- 常见任务使用友好命令
- 高级任务使用 run 或 api，不丢字段
- 大结果落盘并返回 manifest
- 服务或通道失败时给出可执行诊断
- 另一个 AI 能从能力包区分已部署事实和后续架构建议
