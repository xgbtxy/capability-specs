# Environment Setup

这个能力要解决的是：让 AI 在 Windows 的 PowerShell 里从大量结果中快速交互筛选。

## 1. 必要工具

- fzf
- PowerShell

## 2. 官方安装入口

- fzf 项目页: [https://github.com/junegunn/fzf](https://github.com/junegunn/fzf)

## 3. 安装方法

### fzf

- Windows：
  按项目页下载 Windows 发行包，解压后把 `fzf.exe` 放到 PATH 里可访问的位置。
- 也可以：
  用你当前常用的 Windows 包管理器安装。

## 4. 安装后检查

- `fzf --version`
- `@('a','b','c') | fzf`

## 5. 和这个能力的关系

- 必须依赖：fzf
- 常见输入：文件列表、git 输出、历史命令、日志搜索结果

## 6. 常见问题

- 问题：中文或路径显示不舒服
  排查：优先在 PowerShell 7 或 Windows Terminal 中使用
- 问题：预览命令无输出
  排查：先确认传入的是文件路径还是普通文本
