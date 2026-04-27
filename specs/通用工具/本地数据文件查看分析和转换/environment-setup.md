# Environment Setup

这个能力要解决的是：让 AI 能直接用命令行分析本地数据文件。

## 1. 必要工具

- DuckDB CLI
- 一个可用终端

## 2. 官方安装入口

- DuckDB 安装文档: [https://duckdb.org/docs/installation/](https://duckdb.org/docs/installation/)
- DuckDB CLI 文档: [https://duckdb.org/docs/stable/clients/cli/overview.html](https://duckdb.org/docs/stable/clients/cli/overview.html)
- DuckDB 数据导入文档: [https://duckdb.org/docs/stable/data/overview](https://duckdb.org/docs/stable/data/overview)

## 3. 安装方法

### DuckDB

- Windows：
  按官方安装文档下载 DuckDB CLI，放到 PATH 可访问的位置。
- Linux：
  按官方安装文档下载对应二进制，或使用系统包管理器。
- macOS：
  可以按官方文档安装，也可以使用 Homebrew。

## 4. 安装后检查

- `duckdb --version`
- `duckdb -c "select 1 as ok;"`

## 5. 和这个能力的关系

- 必须依赖：DuckDB CLI
- 常见输入：CSV、JSON、Parquet、Excel 转出的 CSV
- 常见输出：CSV、Parquet、查询表格、汇总结果

## 6. 常见问题

- 问题：中文或编码乱码
  排查：先确认源文件编码，必要时先转换成 UTF-8
- 问题：字段识别不对
  排查：显式指定读取参数，先抽样确认列名和类型
