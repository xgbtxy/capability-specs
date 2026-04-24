# environment-setup

这组能力至少要准备这些环境：

- 已经能 SSH 登录服务器
- 服务器上有 `systemd`
- 代理服务二进制和配置文件可访问
- 本机能做基础端口探测

推荐工具：

- Xray
  官方链接：[Xray-core](https://github.com/XTLS/Xray-core)
- systemd
  官方链接：[systemctl](https://www.freedesktop.org/software/systemd/man/latest/systemctl.html)

最小检查方式：

```bash
systemctl status xray
ss -lntup
free -h
```
