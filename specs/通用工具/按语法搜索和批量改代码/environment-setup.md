# Environment Setup

这个能力要解决的是：让 AI 直接按代码语法结构搜索和改写代码。

## 1. 必要工具

- ast-grep
- 一个可用终端

## 2. 官方安装入口

- ast-grep 文档: [https://ast-grep.github.io/](https://ast-grep.github.io/)
- ast-grep CLI 文档: [https://ast-grep.github.io/reference/cli.html](https://ast-grep.github.io/reference/cli.html)

## 3. 安装方法

### ast-grep

- Windows：
  按官方文档下载对应二进制，并放到 PATH 可访问的位置。
- Linux：
  按官方文档安装对应包或二进制。
- macOS：
  按官方文档安装，也可以使用 Homebrew。

## 4. 安装后检查

- `ast-grep --version`
- `ast-grep scan -p 'console.log($A)' .`

## 5. 和这个能力的关系

- 必须依赖：ast-grep
- 常见输入：JavaScript、TypeScript、Python、Go、Rust 等代码目录

## 6. 常见问题

- 问题：匹配不到
  排查：先确认语言识别和模式语法
- 问题：改写范围太大
  排查：先用只读扫描缩小路径和模式
