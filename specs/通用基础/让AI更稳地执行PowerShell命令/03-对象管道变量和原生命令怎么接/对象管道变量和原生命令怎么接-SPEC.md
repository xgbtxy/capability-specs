# 对象管道变量和原生命令怎么接

## 目标

先分清：

- `Get-ChildItem` 这类返回对象
- `git`、`rg` 这类更多返回文本
- 后面是要继续管道，还是只要拿结果字符串

## 默认做法

- 对象优先用 `Select-Object`、`Where-Object`
- 文本结果优先先看一眼再接下一步
- 涉及原生命令时，必要时检查 `$LASTEXITCODE`
