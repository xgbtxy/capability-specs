# Environment Setup

这个能力要解决的是：让 AI 直接用命令行扫描代码安全规则。

## 1. 必要工具

- Semgrep CLI
- 一个可用终端

## 2. 官方安装入口

- Semgrep 文档: [https://semgrep.dev/docs/](https://semgrep.dev/docs/)
- Semgrep CLI 文档: [https://semgrep.dev/docs/getting-started/cli](https://semgrep.dev/docs/getting-started/cli)

## 3. 安装方法

### Semgrep

- Windows：
  按官方文档安装 CLI。
- Linux：
  按官方文档用 `pipx`、`pip` 或包管理方式安装。
- macOS：
  按官方文档安装，也可以使用 Homebrew。

## 4. 安装后检查

- `semgrep --version`
- `semgrep scan --config auto .`

## 5. 和这个能力的关系

- 必须依赖：Semgrep CLI
- 常见输入：应用代码仓库、某语言目录、某类高风险代码

## 6. 常见问题

- 问题：误报多
  排查：先缩小目录和语言，再改规则集
- 问题：扫描慢
  排查：先从关键目录或关键语言开始
