# environment-setup

这组能力至少要准备这些环境：

- 能发起 SSH 连接的客户端
  官方链接：[OpenSSH for Windows](https://learn.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse)
  官方链接：[PuTTY / Plink](https://www.putty.org/)
- 能查看 systemd 服务的 Linux 服务器
  官方链接：[systemctl](https://www.freedesktop.org/software/systemd/man/latest/systemctl.html)
- 本机能执行基础网络探测
  Windows 可以直接用 `Test-NetConnection`

最小检查方式：

```powershell
ssh -V
Test-NetConnection 1.1.1.1 -Port 22
```

如果要走 `Plink`，也可以检查：

```powershell
& 'C:\Program Files\PuTTY\plink.exe' -V
```
