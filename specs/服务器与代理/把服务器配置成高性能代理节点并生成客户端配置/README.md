# 把服务器配置成高性能代理节点并生成客户端配置

把这类真实链路收在一起：

- 先 SSH 连上服务器
- 再把服务器收成只干代理的高性能节点
- 再按客户端生成连接配置
- 最后排查端口、分流、TUN 这类连接问题

## 推荐工具

- OpenSSH / PuTTY
  官方链接：[OpenSSH for Windows](https://learn.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse) / [PuTTY Download](https://www.putty.org/)
- Xray
  官方链接：[XTLS / Xray-core](https://github.com/XTLS/Xray-core)
- Clash Verge Rev / Mihomo
  官方链接：[Clash Verge Rev](https://github.com/clash-verge-rev/clash-verge-rev) / [Mihomo](https://github.com/MetaCubeX/mihomo)

## 最小使用方式

1. 先连上服务器并确认系统情况
2. 把服务器收敛成只跑代理的节点
3. 提取服务端参数，生成不同客户端配置
4. 遇到不通时，继续按客户端差异排查

## 包含的能力

- [01-SSH远程连接服务器并开始操作](./01-SSH远程连接服务器并开始操作)
- [02-把服务器变成代理节点并拉满性能](./02-把服务器变成代理节点并拉满性能)
- [03-根据代理客户端生成连接配置并排查问题](./03-根据代理客户端生成连接配置并排查问题)
