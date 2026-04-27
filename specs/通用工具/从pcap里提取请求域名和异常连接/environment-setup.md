# Environment Setup

这个能力要解决的是：让 AI 直接在 Windows 的 PowerShell 里用 tshark 从抓包文件中提取域名、请求和异常连接。

## 1. 必要工具

- tshark
- PowerShell

## 2. 官方安装入口

- Wireshark / tshark: [https://www.wireshark.org/](https://www.wireshark.org/)

## 3. 安装方法

### tshark

- Windows：
  按官方安装 Wireshark 时，确保同时安装 tshark 并让它进入 PATH。

## 4. 安装后检查

- `tshark --version`
- `tshark -r sample.pcapng -q -z io,phs`

## 5. 和这个能力的关系

- 必须依赖：tshark
- 常见输入：pcap、pcapng、导出的流量文件

## 6. 常见问题

- 问题：看不到想要的协议字段
  排查：先确认流量本身是否包含该协议或该层明文
- 问题：结果太多
  排查：先按时间段、IP、协议或主机做筛选
