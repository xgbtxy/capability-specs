# 安装Codex必用的所有命令环境

## 目标

先把 Codex 高频会调用的那批命令环境装齐，让它进到一个项目后不用先因为缺命令卡住。

## 最小工具集合

- Git
- ripgrep (`rg`)
- fd
- Python
- uv
- Node.js
- GitHub CLI (`gh`)
- OpenSSH (`ssh`)

Windows 常用补充：

- 7-Zip
- PowerShell 7

## 推荐流程

1. 先检查这些命令是否存在
2. 缺什么补什么
3. 安装后逐个跑版本命令
4. 记录还缺什么

## 最小检查命令

- `git --version`
- `rg --version`
- `fd --version`
- `python --version`
- `uv --version`
- `node --version`
- `gh --version`
- `ssh -V`

## 完成标准

- 以上命令都能正常执行
- 包管理器可用
- 终端重开后 PATH 正常
