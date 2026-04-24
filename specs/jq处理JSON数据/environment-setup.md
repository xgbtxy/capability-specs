# Environment Setup

这个能力要解决的是：在命令行里快速处理 JSON 数据。

## 1. 必要工具

- jq
- 一个可用终端

## 2. 官方安装入口

- jq 主页: [https://jqlang.org/](https://jqlang.org/)
- jq 下载页: [https://jqlang.org/download/](https://jqlang.org/download/)

## 3. 安装方法

### jq

- Windows：
  `winget install jqlang.jq`
- Linux：
  Debian / Ubuntu: `sudo apt-get update && sudo apt-get install -y jq`
- macOS：
  `brew install jq`

## 4. 安装后检查

- `jq --version`
- `echo '{\"a\":1}' | jq .`

## 5. 和这个能力的关系

- 必须依赖：jq
- 可选依赖：curl、日志文件、API 输出文件

## 6. 常见问题

- 问题：过滤器写不对
  排查：先用 `jq .` 看结构，再逐步加过滤器
