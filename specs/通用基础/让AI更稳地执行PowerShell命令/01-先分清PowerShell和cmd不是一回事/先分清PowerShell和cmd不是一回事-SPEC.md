# 先分清PowerShell和cmd不是一回事

## 目标

先避免这些混用：

- `cmd` 的 `%VAR%` 和 PowerShell 的 `$env:VAR`
- `cmd` 的 `dir /b` 和 PowerShell 的 `Get-ChildItem`
- `cmd` 的 `del`、`copy` 习惯和 PowerShell 的对象式命令

## 默认做法

- 当前环境只要是 PowerShell，就优先写 PowerShell 风格
- 不确定时，先用 PowerShell 原生命令，不先写 cmd 兼容写法
