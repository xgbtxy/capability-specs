# SSH远程连接服务器并开始操作

把“拿到一台服务器的地址、端口、账号后，安全连进去、确认系统情况、开始真正操作”拆成可复用的小能力。

## 推荐工具

- OpenSSH
  官方链接：[OpenSSH for Windows](https://learn.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse)
- PuTTY / Plink
  官方链接：[PuTTY Download](https://www.putty.org/)
- systemd / journalctl
  官方链接：[systemctl](https://www.freedesktop.org/software/systemd/man/latest/systemctl.html) / [journalctl](https://www.freedesktop.org/software/systemd/man/latest/journalctl.html)

## 最小使用方式

1. 先确认服务器 IP、SSH 端口、账号和认证方式
2. 用合适的客户端连上服务器
3. 先确认系统、服务、端口和资源情况
4. 真正改动前先备份关键配置并记录基线

## 包含的能力

- [01-确认连接信息与访问方式](./01-确认连接信息与访问方式)
- [02-用合适客户端发起SSH连接](./02-用合适客户端发起SSH连接)
- [03-第一次登录并确认系统环境](./03-第一次登录并确认系统环境)
- [04-进入实际操作前先做备份与基线记录](./04-进入实际操作前先做备份与基线记录)
