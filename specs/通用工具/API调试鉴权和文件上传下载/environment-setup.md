# Environment Setup

这个能力要解决的是：让 AI 直接用命令行调试接口。

## 1. 必要工具

- HTTPie
- 一个可用终端

## 2. 官方安装入口

- HTTPie 文档: [https://httpie.io/docs](https://httpie.io/docs)
- HTTPie 安装文档: [https://httpie.io/docs/cli/installation](https://httpie.io/docs/cli/installation)

## 3. 安装方法

### HTTPie

- Windows：
  按官方文档安装，确认 `http` 命令可用。
- Linux：
  按官方文档使用包管理器或 `pipx` 安装。
- macOS：
  按官方文档安装，也可以使用 Homebrew。

## 4. 安装后检查

- `http --version`
- `http https://httpbin.org/get`

## 5. 和这个能力的关系

- 必须依赖：HTTPie
- 常见输入：REST API、文件上传接口、需要 token 的接口

## 6. 常见问题

- 问题：401 或 403
  排查：先确认认证头、token 和请求方法
- 问题：文件上传失败
  排查：确认 multipart 写法和服务端要求
