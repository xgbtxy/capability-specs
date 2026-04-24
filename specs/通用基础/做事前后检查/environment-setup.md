# Environment Setup

这个能力要解决的是：在正式做事前后，快速检查环境、输入、结果和失败点。

## 1. 必要工具

- 一个可用的终端
- 基本文件查看命令

## 2. 官方安装入口

- PowerShell: [https://learn.microsoft.com/powershell](https://learn.microsoft.com/powershell)
- PowerShell 安装说明: [https://learn.microsoft.com/en-us/powershell/scripting/install/installing-powershell](https://learn.microsoft.com/en-us/powershell/scripting/install/installing-powershell)
- Git Bash: [https://git-scm.com/downloads](https://git-scm.com/downloads)

## 3. 安装方法

### PowerShell

- Windows：
  系统通常自带；如需新版可按微软官方文档安装 PowerShell 7。
- Linux：
  参考微软官方安装文档。
- macOS：
  `brew install --cask powershell`

### Git Bash（可选）

- Windows：
  安装 Git for Windows 后即可获得 Git Bash。

## 4. 安装后检查

- `pwd`
- `Get-ChildItem`
- `echo test`

## 5. 和这个能力的关系

- 必须依赖：可用终端、基础查看命令
- 可选依赖：Git Bash、PowerShell 7+

## 6. 常见问题

- 问题：命令执行不了
  排查：先确认当前终端类型和 PATH
- 问题：文件路径找不到
  排查：先用 `pwd` 和目录查看命令确认当前位置
