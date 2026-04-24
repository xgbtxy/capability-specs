# Environment Setup

这个能力要解决的是：先把 Codex 开工最常用的一批命令环境装齐，让它一上来就能工作。

## 1. 必要工具

- 一个可用终端
- 至少一个包管理器
- 浏览器

## 2. 常见工具入口

- PowerShell: [https://learn.microsoft.com/powershell](https://learn.microsoft.com/powershell)
- Git: [https://git-scm.com/downloads](https://git-scm.com/downloads)
- ripgrep: [https://ripgrep.dev/](https://ripgrep.dev/)
- fd: [https://github.com/sharkdp/fd](https://github.com/sharkdp/fd)
- Python: [https://www.python.org/downloads/](https://www.python.org/downloads/)
- uv: [https://docs.astral.sh/uv/](https://docs.astral.sh/uv/)
- Node.js: [https://nodejs.org/](https://nodejs.org/)
- GitHub CLI: [https://cli.github.com/](https://cli.github.com/)
- OpenSSH for Windows: [https://learn.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse](https://learn.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse)
- 7-Zip: [https://www.7-zip.org/download.html](https://www.7-zip.org/download.html)
- winget: [https://learn.microsoft.com/windows/package-manager/winget/](https://learn.microsoft.com/windows/package-manager/winget/)
- Homebrew: [https://brew.sh/](https://brew.sh/)

## 3. 安装方法

- Windows：
  先用 `winget` 安装 PowerShell、Git、Python、Node.js、GitHub CLI、7-Zip。
- macOS：
  先用 `brew` 安装 git、ripgrep、fd、python、uv、node、gh。
- Linux：
  先用系统包管理器安装 git、ripgrep、fd、python3、nodejs、openssh-client，再补 `uv` 和 `gh`。

## 4. 安装后检查

- `git --version`
- `rg --version`
- `fd --version`
- `python --version`
- `uv --version`
- `node --version`
- `gh --version`
- `ssh -V`

## 5. 和这个能力的关系

- 必须依赖：终端、包管理器、Git、`rg`、`fd`
- 强烈建议：Python、`uv`、Node.js、GitHub CLI、OpenSSH
- Windows 常用补充：7-Zip
