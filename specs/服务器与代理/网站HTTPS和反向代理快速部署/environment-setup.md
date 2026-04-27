# Environment Setup

这个能力要解决的是：用 Caddy 快速部署 HTTPS 和反向代理。

## 1. 必要工具

- Caddy
- curl
- systemctl 或等价服务管理工具

## 2. 官方安装入口

- Caddy 文档: [https://caddyserver.com/docs/](https://caddyserver.com/docs/)
- Caddy 安装文档: [https://caddyserver.com/docs/install](https://caddyserver.com/docs/install)
- Caddyfile 文档: [https://caddyserver.com/docs/caddyfile](https://caddyserver.com/docs/caddyfile)
- reverse_proxy 文档: [https://caddyserver.com/docs/caddyfile/directives/reverse_proxy](https://caddyserver.com/docs/caddyfile/directives/reverse_proxy)

## 3. 安装方法

### Caddy

- Linux：
  按官方安装文档使用对应发行版安装方式。
- Windows：
  下载官方二进制或使用包管理器安装。
- macOS：
  按官方文档安装，也可以使用 Homebrew。

## 4. 安装后检查

- `caddy version`
- `caddy validate --config Caddyfile`
- `curl -I https://你的域名`

## 5. 和这个能力的关系

- 必须依赖：Caddy
- 常用辅助：curl、systemctl、DNS 查询工具
- 前置条件：域名解析到服务器，80 和 443 端口可访问

## 6. 常见问题

- 问题：证书申请失败
  排查：先看域名解析、80/443 端口、防火墙和云安全组
- 问题：HTTPS 能打开但后端 502
  排查：确认后端服务地址和端口是否真的在监听
