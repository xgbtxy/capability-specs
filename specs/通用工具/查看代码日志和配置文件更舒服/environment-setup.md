# Environment Setup

这个能力要解决的是：让 AI 在 Windows 的 PowerShell 里更舒服地查看代码、日志和配置文件。

## 1. 必要工具

- bat
- PowerShell

## 2. 官方安装入口

- bat 项目页: [https://github.com/sharkdp/bat](https://github.com/sharkdp/bat)

## 3. 安装方法

### bat

- Windows：
  按项目页下载 Windows 发行包，解压后把 `bat.exe` 放到 PATH 里可访问的位置。
- 也可以：
  用你当前常用的 Windows 包管理器安装。

## 4. 安装后检查

- `bat --version`
- `bat C:\Users\15412\Desktop\工具包\capability-specs\README.md`

## 5. 和这个能力的关系

- 必须依赖：bat
- 常见输入：代码文件、日志文件、YAML/JSON/INI 配置

## 6. 常见问题

- 问题：终端颜色不正常
  排查：优先在 Windows Terminal 或 PowerShell 7 下使用
- 问题：大文件滚动不顺
  排查：按需加 `--paging=always`
