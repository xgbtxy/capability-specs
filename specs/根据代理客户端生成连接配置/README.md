# 根据代理客户端生成连接配置

根据服务端真实参数，给不同代理客户端生成能直接用的连接配置，并处理客户端差异。

## 推荐工具

- Xray / v2ray 客户端 JSON
  官方链接：[Xray-core](https://github.com/XTLS/Xray-core)
- Clash Verge / Mihomo
  官方链接：[Clash Verge Rev](https://github.com/clash-verge-rev/clash-verge-rev) / [Mihomo](https://github.com/MetaCubeX/mihomo)

## 最小使用方式

1. 先从服务端提取连接参数
2. 按客户端类型生成对应配置
3. Clash 类客户端再补分流规则
4. 如果同一节点不同客户端表现不同，再按客户端差异排查

## 包含的能力

- [01-提取服务端连接参数](./01-提取服务端连接参数)
- [02-生成v2ray或xray客户端配置](./02-生成v2ray或xray客户端配置)
- [03-生成Clash Verge配置与分流规则](./03-生成Clash Verge配置与分流规则)
- [04-按客户端差异排查连接与TUN问题](./04-按客户端差异排查连接与TUN问题)
