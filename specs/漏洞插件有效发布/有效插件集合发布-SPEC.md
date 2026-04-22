# 有效插件集合发布-SPEC

版本：v1.0  
状态：正式  
适用对象：漏洞插件仓库维护者、自动化发布执行者、AI 协作链路  
适用仓库：VulKit 类插件仓库

---

## 1. 问题定义

漏洞插件项目在持续迭代时，发布阶段经常出现以下问题：

- 当前工作树存在大量无关变更
- 多个分支同时推进，难以界定本次 PR 范围
- 历史存在幻觉撤回、错误插件、回滚修订、失效分支
- 不能简单把“当前目录内容”视为可发布结果
- PR 创建能力依赖 `gh`、MCP 或网页自动化时，容易被环境问题卡住

因此，需要一个更稳定的发布流程，用于：

**只发布当前真实有效的插件集合，并在不依赖高级工具的情况下完成 PR 创建。**

---

## 2. 目标

本规范的目标如下：

1. 只发布当前有效插件集合
2. 不从脏工作树直接发版
3. 发布范围必须由清单驱动
4. 可以在 `gh` 不存在时继续工作
5. 使用本机已可用 Git 凭据完成 GitHub PR 创建
6. 整个流程可复现、可审计、可回滚

---

## 3. 真相源定义

发布真相源必须同时满足以下两个条件：

1. `vuln_registry.csv` 中状态为 `DONE`
2. `VulKit/` 中正式文件真实存在

只有满足这两个条件的插件，才允许进入发布集合。

### 3.1 必要附属文件

若对应产品目录下存在 `fingerprint.json`，应一并纳入发布集合。

### 3.2 不纳入发布集合的内容

以下内容禁止进入发布集合：

- `READY`
- `BLOCKED`
- 临时工作区结果
- 历史撤回项
- 审计草稿
- 汇报文档
- 未确认完成状态的插件
- 与本次发布无关的脏工作树改动

---

## 4. 标准流程

### 第 1 步：生成有效交付摘要

执行交付摘要和完整性审计脚本，确认：

- 当前 `DONE` 数量
- 是否存在重复 CVE
- 是否存在 `DONE` 但正式文件缺失

只有在以下条件满足时才允许继续：

- `DONE` 中重复 CVE = 0
- `DONE` 但正式文件不存在 = 0

---

### 第 2 步：生成 include 清单

从 `vuln_registry.csv` 中筛选出：

- `status == DONE`
- `vulkit_path` 非空
- 正式文件真实存在

输出一份 `include` 清单，只保留：

- `.yak`
- 对应的 `fingerprint.json`

该清单是**唯一发布范围依据**。

---

### 第 3 步：从 origin/main 创建干净 worktree

必须从 `origin/main` 派生一个新的干净 `worktree`，作为本次发布环境。

要求：

- 不直接从当前工作树提 PR
- 不直接在长期开发分支上组装发布内容
- 每次发布使用独立 worktree 路径
- 每次发布使用可识别的分支名

分支名示例：

- `feature/chenyan`
- `release/2026-04-22-valid-set`
- `release/2026-04-22-review-batch-001`

---

### 第 4 步：复制 include 清单中的文件

从正式仓库中，按 `include` 清单将文件复制到干净 worktree。

只能复制：

- 有效 `.yak`
- 必要 `fingerprint.json`

禁止复制：

- 临时脚本
- 测试样本
- 说明文档
- 聊天记录
- 本地缓存
- 其他无关文件

---

### 第 5 步：在干净 worktree 中提交并推送

在干净 worktree 中执行：

1. `git add .`
2. `git commit -m "<message>"`
3. `git push -u origin <branch>`

提交信息应清晰表达这次发布的语义，例如：

- `feat: publish validated plugins`
- `feat: publish review-batch-001 plugins`
- `feat: publish two-highs-one-weak plugin set`

---

### 第 6 步：获取本机可用 GitHub 凭据

若 `gh` 不可用，则使用：

```text
git credential fill
```

从本机已经可正常 `git push` 的凭据链中获取 GitHub 可用凭据。

注意：

- 这里获取到的可能是 PAT，不一定是登录密码
- 不得把凭据写入仓库
- 不得把凭据持久化为明文文件

---

### 第 7 步：必要时关闭旧 PR

若存在旧的、过期的、范围不准确的 PR，需要先关闭，再重新创建新 PR。

关闭方式：

通过 GitHub REST API 调用：

```http
PATCH /repos/{owner}/{repo}/pulls/{number}
```

请求体：

```json
{
  "state": "closed"
}
```

---

### 第 8 步：通过 GitHub REST API 创建新 PR

调用接口：

```http
POST /repos/{owner}/{repo}/pulls
```

请求体最小字段：

```json
{
  "title": "PR 标题",
  "head": "发布分支",
  "base": "main",
  "body": "PR 正文",
  "draft": false
}
```

推荐规则：

- `head`：当前发布分支，如 `feature/chenyan`
- `base`：`main`
- 标题和正文必须写清发布范围与统计结果

---

### 第 9 步：后续修订继续在同一干净 worktree 上进行

PR 审核过程中若需要修订：

- 必须在当前发布用的干净 worktree 上修改
- 修订后直接 `git add / commit / push`
- 不要回到脏工作树修改后再二次复制

---

## 5. 输出要求

每次发布应至少输出以下结果：

- 发布分支名
- 最新提交哈希
- PR 编号
- PR URL
- `.yak` 数量
- `fingerprint.json` 数量
- 总处理条目数
- 当前 `DONE` 数
- 重复 CVE 数
- 缺失正式文件数

---

## 6. 安全边界

### 6.1 禁止事项

禁止：

- 直接在脏工作树中提 PR
- 直接全量 `git add -A` 把整个仓库发出去
- 将 PAT / 密码 / token 明文写入仓库
- 将未完成插件、撤回项、临时说明文件纳入发布集合
- 依赖浏览器手工拖文件上传替代 Git 发布流程

### 6.2 允许事项

允许：

- 使用 `git credential fill` 获取本机 GitHub 可用凭据
- 使用 GitHub REST API 创建和关闭 PR
- 使用干净 worktree 作为发布环境
- 使用 `include` 清单精确控制发布范围

---

## 7. 推荐 PR 结构

### 标题建议

- `【两高一弱】review-batch-001 今日插件批次提交`
- `2026-03-31至2026-04-20-有效保留插件汇总`
- `【有效插件集合】YYYY-MM-DD 发布汇总`

### 正文建议包含

1. 变更说明
2. 新增 `.yak` 数量
3. 复用插件数量
4. 合计处理条目
5. 提交背景
6. 范围说明
7. 校验情况
8. 备注

---

## 8. 结论

本规范的核心思想是：

**用“有效集合 + include 清单 + 干净 worktree + GitHub REST API”替代“直接在脏分支提 PR”。**

这样做的收益是：

- 发布范围可控
- 流程可复现
- 结果可审计
- 不依赖高级工具
- 适合大批量漏洞插件的持续发布
