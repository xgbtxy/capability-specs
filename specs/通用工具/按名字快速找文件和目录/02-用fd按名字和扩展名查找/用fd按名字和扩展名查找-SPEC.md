# 用fd按名字和扩展名查找

## 目标

在已知目录范围内，快速找出目标路径。

## 常用命令

```powershell
fd config C:\project
fd --type f --extension log . C:\logs
fd --type d backup C:\data
```

## 建议

- 先用最小条件确认是否有命中
- 文件和目录分开找
- 扩展名搜索优先用 `--extension`
