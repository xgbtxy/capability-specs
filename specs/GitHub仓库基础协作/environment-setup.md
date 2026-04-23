# environment-setup

## 目标

让不熟悉 Git / GitHub 的执行者具备完成日常 PR 协作所需的最小环境。

---

## 1. 必要软件

### 1.1 Git

要求：

- 本机已安装 Git
- 支持基础命令：`status`、`switch`、`add`、`commit`、`push`、`pull`

建议版本：

- Git for Windows 最新稳定版

验证方式：

```powershell
git --version
git status
```

---

### 1.2 GitHub 访问能力

满足以下任一条件即可：

- 本机 `git push` 到目标仓库正常
- 已安装并登录 `gh`
- 已配置可用的 GitHub 连接器 / API 凭据

验证方式：

```powershell
git remote -v
git push --dry-run
```

---

## 2. 推荐但非必须的软件

- GitHub CLI（`gh`）
- PowerShell 7+

这些工具可以提升体验，但本场景不强制依赖它们。

---

## 3. 仓库前提

目标仓库建议满足：

- 本地已有 checkout
- 远端仓库存在
- 当前执行者具备读取仓库权限
- 若需要上传和发 PR，还需具备 push / PR 权限

---

## 4. 开始前检查

在执行能力前，建议先确认：

- [ ] 知道本地仓库路径
- [ ] 知道团队让你工作的分支名
- [ ] 知道 PR 要合并到哪个分支
- [ ] 本机能够访问 GitHub
- [ ] 当前仓库没有自己不认识的危险改动
