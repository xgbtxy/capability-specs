# 把选择结果传给PowerShell继续处理

## 常用命令

```powershell
$file = fd . C:\project | fzf
if ($file) { Get-Content $file -TotalCount 20 }
```

## 重点

- 先判断是否有返回值
- 写操作前先打印确认
