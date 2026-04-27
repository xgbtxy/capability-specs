# Environment Setup

这个能力要解决的是：让 AI 在 Windows 的 PowerShell 里把项目高频命令收成统一入口。

## 1. 必要工具

- just
- PowerShell

## 2. 官方安装入口

- just 项目页: [https://github.com/casey/just](https://github.com/casey/just)

## 3. 安装方法

### just

- Windows：
  按项目页下载 Windows 发行包，解压后把 `just.exe` 放到 PATH 里可访问的位置。
- 也可以：
  用你当前常用的 Windows 包管理器安装。

## 4. 安装后检查

- `just --version`
- 在一个空目录里创建最小 `justfile` 后运行 `just --list`

## 5. 和这个能力的关系

- 必须依赖：just
- 常见输入：构建命令、测试命令、启动命令、打包命令、清理命令

## 6. 常见问题

- 问题：任务里引用 PowerShell 语法报错
  排查：明确命令是在 PowerShell 下运行
- 问题：团队有人跑不通
  排查：先用 `just --list` 和单条最小任务确认环境一致
