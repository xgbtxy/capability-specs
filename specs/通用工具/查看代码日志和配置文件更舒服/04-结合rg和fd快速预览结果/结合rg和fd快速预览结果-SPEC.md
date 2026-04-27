# 结合rg和fd快速预览结果

## 常用思路

- `fd` 先找目标文件
- `rg` 先找关键字
- `bat` 再高亮预览

## 示例

```powershell
fd config C:\project | ForEach-Object { bat $_ }
```
