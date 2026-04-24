# 把服务器变成代理节点并拉满性能

把“一台普通 Linux 服务器收敛成只跑代理服务的节点，并把稳定性和吞吐尽量拉满”拆成可复用的小能力。

## 推荐工具

- Xray
  官方链接：[XTLS / Xray-core](https://github.com/XTLS/Xray-core)
- systemd
  官方链接：[systemd](https://www.freedesktop.org/software/systemd/man/latest/systemd.html)
- ss / iptables / nftables / journalctl
  官方链接：[ss](https://man7.org/linux/man-pages/man8/ss.8.html) / [nft](https://wiki.nftables.org/wiki-nftables/index.php/Main_Page)

## 最小使用方式

1. 先确认代理服务、配置文件和监听端口
2. 清理无关服务，减少噪音和系统开销
3. 收敛代理服务参数，优先稳定吞吐而不是堆激进参数
4. 验证端口外部可达、服务稳定运行、客户端能正常连上

## 包含的能力

- [01-确认代理服务与监听端口](./01-确认代理服务与监听端口)
- [02-清理无关服务并收敛系统开销](./02-清理无关服务并收敛系统开销)
- [03-收敛代理服务配置并提升稳定吞吐](./03-收敛代理服务配置并提升稳定吞吐)
- [04-排查端口可达性并验证节点可用](./04-排查端口可达性并验证节点可用)
