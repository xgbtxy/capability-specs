# 排除目录并限制搜索范围

## 目标

当结果太多时，排除无关目录，减少误命中。

## 常用命令

```powershell
fd config C:\project --exclude node_modules --exclude .git
fd --type f --extension yaml . C:\project --exclude vendor
```

## 重点

- 优先排 `node_modules`、`.git`、`dist`、`build`
- 优先从项目根目录开始，不要默认整个磁盘
