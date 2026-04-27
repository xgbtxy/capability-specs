# Environment Setup

这个能力要解决的是：让 AI 在 Windows 的 PowerShell 环境里少犯低级语法错误，优先按更稳的方式执行命令。

## 1. 默认环境

- Windows
- PowerShell

## 2. 强烈建议

- 优先使用 PowerShell 7 或较新的 Windows PowerShell
- 路径优先用完整绝对路径
- 遇到中文和空格路径时，优先单引号包住整个路径

## 3. 安装后检查

- `$PSVersionTable`
- `Get-Location`
- `Test-Path 'C:\Users\15412\Desktop\工具包'`

## 4. 和这个能力的关系

- 这不是 PowerShell 教材
- 这是根据真实使用经验整理出来的稳妥写法
- 重点是让 AI 少犯混用语法、错误引用路径、乱接管道这些问题

## 5. 常见问题

- 问题：把 cmd 的 `%VAR%`、`dir /b`、`&&` 直接搬进 PowerShell
  排查：先确认这是 PowerShell，不是 cmd
- 问题：中文路径或空格路径报错
  排查：优先单引号包路径，必要时拆成多步
- 问题：原生命令执行了，但 PowerShell 判断结果不对
  排查：同时看 `$?` 和 `$LASTEXITCODE`
