# 开始项目前让大模型安装常用工具和项目工具

把“先让大模型按自己原生常用命令判断是否需要安装常用工具，再问用户要做什么事，最后按项目目标补项目工具”拆成可复用的小能力。

## 推荐工具

- PowerShell
  官方链接：[PowerShell](https://learn.microsoft.com/powershell)
- Git
  官方链接：[Git](https://git-scm.com/downloads)
- Node.js / Python / Docker 等项目工具
  官方链接：[Node.js](https://nodejs.org/) / [Python](https://www.python.org/downloads/) / [Docker](https://docs.docker.com/get-docker/)

## 最小使用方式

1. 先让大模型按自己常用命令检查本机是否缺少常用工具
2. 询问用户这次到底要做什么项目
3. 只安装这次项目真正需要的工具
4. 验证这些工具能不能真的跑起来

## 包含的能力

- [01-先让大模型安装常用工具](./01-先让大模型安装常用工具)
- [02-询问用户要做什么事](./02-询问用户要做什么事)
- [03-按项目目标安装项目工具](./03-按项目目标安装项目工具)
- [04-验证工具是否真的可用](./04-验证工具是否真的可用)
