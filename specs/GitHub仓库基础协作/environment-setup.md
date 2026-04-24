# Environment Setup

这个能力要解决的是：把 GitHub 仓库日常协作跑起来。

## 1. 必要工具

- Git
- 能访问 GitHub 的账号或凭据

## 2. 官方安装入口

- Git: [https://git-scm.com/downloads](https://git-scm.com/downloads)
- GitHub CLI: [https://cli.github.com/](https://cli.github.com/)
- PowerShell: [https://learn.microsoft.com/powershell](https://learn.microsoft.com/powershell)

## 3. 安装方法

### Git

- Windows：
  直接安装官方 Git for Windows，按默认选项即可。
- Linux：
  Debian / Ubuntu: `sudo apt-get update && sudo apt-get install -y git`
- macOS：
  `brew install git`

### GitHub CLI（推荐）

- Windows：
  `winget install --id GitHub.cli`
- Linux：
  参考官方仓库安装说明：[https://github.com/cli/cli#installation](https://github.com/cli/cli#installation)
- macOS：
  `brew install gh`

## 4. 安装后检查

- `git --version`
- `git remote -v`
- `gh --version`
- `gh auth status`

## 5. 和这个能力的关系

- 必须依赖：Git、可用的 GitHub 访问权限
- 可选依赖：GitHub CLI、PowerShell 7+

## 6. 常见问题

- 问题：`git push` 失败
  排查：先看远端地址、当前账号权限、网络是否能访问 GitHub
- 问题：`gh auth status` 失败
  排查：执行 `gh auth login` 重新登录
