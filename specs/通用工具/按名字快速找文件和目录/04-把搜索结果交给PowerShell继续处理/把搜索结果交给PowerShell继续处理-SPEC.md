# 把搜索结果交给PowerShell继续处理

## 目标

让搜索结果继续参与复制、统计、筛选或打开。

## 常用命令

```powershell
fd --extension log . C:\logs | ForEach-Object { $_ }
fd config C:\project | Set-Content .\matched.txt
fd --type f README C:\Users\15412\Desktop\工具包 | Measure-Object
```

## 注意

- 先确认输出格式再进入管道
- 涉及写入、移动、删除时，先只打印结果
