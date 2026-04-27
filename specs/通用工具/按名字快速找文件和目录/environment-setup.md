# Environment Setup

这个能力要解决的是：让 AI 在 Windows 的 PowerShell 里用更顺手的方式找文件和目录。

## 1. 必要工具

- fd
- PowerShell

## 2. 官方安装入口

- fd 项目页: [https://github.com/sharkdp/fd](https://github.com/sharkdp/fd)

## 3. 安装方法

### fd

- Windows：
  按项目页下载 Windows 发行包，解压后把 `fd.exe` 放到 PATH 里可访问的位置。
- 也可以：
  用你当前常用的 Windows 包管理器安装，只要最后 `fd --version` 能跑通就行。

## 4. 安装后检查

- `fd --version`
- `fd README C:\Users\15412\Desktop\工具包`

## 5. 和这个能力的关系

- 必须依赖：fd
- 常见输入：项目目录、下载目录、日志目录、素材目录

## 6. 常见问题

- 问题：结果太多
  排查：先缩小目录范围，再加扩展名或 `--type`
- 问题：找不到隐藏文件
  排查：按需补 `--hidden`
