# Environment Setup

这个能力要解决的是：让 AI 直接在 Windows 的 PowerShell 里把抓包导出的 JSON、CSV 和结果文件变成可查询数据。

## 1. 必要工具

- DuckDB
- PowerShell

## 2. 官方安装入口

- DuckDB: [https://duckdb.org/](https://duckdb.org/)

## 3. 安装方法

### DuckDB

- Windows：
  按官方安装 CLI，确保 `duckdb` 能直接在 PowerShell 里运行。

## 4. 安装后检查

- `duckdb --version`
- `duckdb -c "select 1"`

## 5. 和这个能力的关系

- 必须依赖：DuckDB
- 常见输入：抓包摘要、JSON 结果、CSV 导出、请求响应清单

## 6. 常见问题

- 问题：JSON 结构不统一
  排查：先抽样看字段，再决定怎么展开
- 问题：CSV 列名不稳定
  排查：先读表头，再统一别名
