# 验证证书访问和续期状态 SPEC

- 用 `curl -I https://域名` 验证 HTTPS 响应
- 查看 Caddy 日志确认是否成功申请证书
- 验证后端页面、API 或静态资源是否正常返回
