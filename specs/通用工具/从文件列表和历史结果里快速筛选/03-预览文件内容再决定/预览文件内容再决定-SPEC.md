# 预览文件内容再决定

## 常用命令

```powershell
fd . C:\project | fzf --preview "bat --style=numbers --color=always {}"
```

## 注意

- 预览优先只读
- 路径里有空格时注意引用
