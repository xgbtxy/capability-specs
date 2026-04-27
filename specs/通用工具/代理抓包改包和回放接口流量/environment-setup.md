# Environment Setup

这个能力要解决的是：让 AI 直接在 Windows 的 PowerShell 里用 mitmproxy 抓包、改包和回放接口流量。

## 1. 必要工具

- mitmproxy 或 mitmdump
- PowerShell

## 2. 官方安装入口

- mitmproxy 项目页: [https://mitmproxy.org/](https://mitmproxy.org/)
- GitHub: [https://github.com/mitmproxy/mitmproxy](https://github.com/mitmproxy/mitmproxy)

## 3. 安装方法

### mitmproxy

- Windows：
  优先按项目页安装，确保 `mitmproxy` 或 `mitmdump` 能直接在 PowerShell 里运行。

## 4. 安装后检查

- `mitmproxy --version`
- `mitmdump --version`

## 5. 和这个能力的关系

- 必须依赖：mitmproxy 或 mitmdump
- 常见输入：浏览器流量、移动端代理流量、接口回放目标

## 6. 常见问题

- 问题：没有抓到流量
  排查：先确认浏览器或设备是否真正走了这个代理
- 问题：HTTPS 看不到明文
  排查：确认 mitmproxy 证书是否正确安装和信任
