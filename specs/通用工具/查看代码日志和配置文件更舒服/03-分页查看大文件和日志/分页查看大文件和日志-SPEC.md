# 分页查看大文件和日志

## 常用命令

```powershell
bat --paging=always .\server.log
bat --paging=always --style=numbers .\big.json
```

## 注意

- 先分页，再决定是否配合搜索
- 大日志通常更适合先 `rg` 再 `bat`
