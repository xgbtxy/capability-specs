# tools-and-safety

## 常用工具

- `systemctl`
- `journalctl`
- `ss`
- `free`
- `iptables` / `nft`
- `xray run -test`

## 安全边界

- 先备份配置，再调服务
- 先看端口是否外部可达，再下“云厂商拦截”的结论
- 先收敛无关服务和明显绕路，再去碰更激进的性能参数
- 对代理节点来说，稳定和可验证比“看起来拉满”更重要
