# Environment Setup

这个能力要解决的是：在命令行里做文档格式转换和发布。

## 1. 必要工具

- Pandoc
- 一个可用终端

## 2. 官方安装入口

- Pandoc 安装页: [https://pandoc.org/installing.html](https://pandoc.org/installing.html)
- Pandoc 手册: [https://pandoc.org/MANUAL.html](https://pandoc.org/MANUAL.html)

## 3. 安装方法

### Pandoc

- Windows：
  按官方安装页下载安装包。
- Linux：
  参考官方安装页或系统包管理器安装。
- macOS：
  `brew install pandoc`

## 4. 安装后检查

- `pandoc --version`
- `pandoc -f markdown -t html sample.md -o sample.html`

## 5. 和这个能力的关系

- 必须依赖：Pandoc
- 可选依赖：LaTeX、模板文件、Lua filters

## 6. 常见问题

- 问题：能转格式但样式不对
  排查：先看模板和 reference doc，而不是怀疑正文内容
