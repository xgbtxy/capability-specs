# Environment Setup

这个能力要解决的是：在正式开始项目前，先看本机底座是否齐，再根据项目目标补项目工具。

## 1. 必要工具

- 一个可用终端
- 至少一个包管理器
- 浏览器

## 2. 常见原生工具入口

- PowerShell: [https://learn.microsoft.com/powershell](https://learn.microsoft.com/powershell)
- Git: [https://git-scm.com/downloads](https://git-scm.com/downloads)
- Python: [https://www.python.org/downloads/](https://www.python.org/downloads/)
- Node.js: [https://nodejs.org/](https://nodejs.org/)
- Docker: [https://docs.docker.com/get-docker/](https://docs.docker.com/get-docker/)
- Winget: [https://learn.microsoft.com/windows/package-manager/winget/](https://learn.microsoft.com/windows/package-manager/winget/)
- Homebrew: [https://brew.sh/](https://brew.sh/)

## 3. 安装方法

### 终端和底座

- Windows：
  优先确认 PowerShell、Git、winget 是否可用。
- Linux：
  优先确认 shell、系统包管理器、Git 是否可用。
- macOS：
  优先确认终端、Git、Homebrew 是否可用。

### 项目工具

- 不提前全装
- 先问清楚用户要做什么
- 再按项目类型装 Node.js、Python、Java、Docker、pnpm、uv、poetry、bun 等项目工具

## 4. 安装后检查

- `git --version`
- `python --version`
- `node --version`
- `docker --version`
- `winget --version`
- `brew --version`

## 5. 和这个能力的关系

- 必须依赖：终端、浏览器、至少一个安装通道
- 可选依赖：Git、Python、Node.js、Docker 等原生底座工具

## 6. 常见问题

- 问题：AI 不知道该装什么
  排查：先让 AI 问清楚“你要做什么项目”
- 问题：工具装了但不能用
  排查：先看 PATH、版本命令、当前终端是否已重开
- 问题：同一台机器上工具太多太乱
  排查：先区分原生工具和项目工具，不要混装
