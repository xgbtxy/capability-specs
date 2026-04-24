# Environment Setup

这个能力要解决的是：在 Windows 上把网络打印机连起来，并处理最容易卡住的驱动问题。

## 1. 必要工具

- Windows 10 或 Windows 11
- 浏览器
- PowerShell
- 打印机所在网络的访问权限

## 2. 官方安装入口

- Windows 打印机安装说明: [https://support.microsoft.com/en-us/windows/add-or-install-a-printer-in-windows-cc0724cf-793e-3542-d1ff-727e4978638b](https://support.microsoft.com/en-us/windows/add-or-install-a-printer-in-windows-cc0724cf-793e-3542-d1ff-727e4978638b)
- 最新打印机驱动说明: [https://support.microsoft.com/en-us/windows/how-to-download-and-install-the-latest-printer-drivers-4ff66446-a2ab-b77f-46f4-a6d3fe4bf661](https://support.microsoft.com/en-us/windows/how-to-download-and-install-the-latest-printer-drivers-4ff66446-a2ab-b77f-46f4-a6d3fe4bf661)
- PowerShell PrintManagement: [https://learn.microsoft.com/en-us/powershell/module/printmanagement/add-printerport?view=windowsserver2025-ps](https://learn.microsoft.com/en-us/powershell/module/printmanagement/add-printerport?view=windowsserver2025-ps)

## 3. 常见厂家驱动入口

- HP: [https://support.hp.com/us-en/drivers](https://support.hp.com/us-en/drivers)
- Brother: [https://support.brother.com/](https://support.brother.com/)
- Canon 中国: [https://www.canon.com.cn/support/](https://www.canon.com.cn/support/)
- Canon U.S.: [https://www.usa.canon.com/support/software-and-drivers](https://www.usa.canon.com/support/software-and-drivers)
- Epson: [https://epson.com/support/epson-printer-drivers](https://epson.com/support/epson-printer-drivers)
- Xerox: [https://www.support.xerox.com/](https://www.support.xerox.com/)

## 4. 安装后检查

- `Get-Printer`
- `Get-PrinterPort`
- `ping <printer-ip>`
- 在浏览器里打开 `http://<printer-ip>` 或 `https://<printer-ip>`

## 5. 和这个能力的关系

- 必须依赖：Windows、浏览器、网络可达、打印机地址或可定位到打印机本机
- 可选依赖：管理员权限、厂家通用驱动、Print Management 控制台

## 6. 常见问题

- 问题：不知道打印机 IP
  排查：先在同一局域网内扫描，或者去打印机面板、网络配置页、标签上看
- 问题：找到了打印机但不能打印
  排查：先确认驱动是否与型号和系统位数匹配
- 问题：Web 页面打不开
  排查：先确认 IP 是否正确、网络是否同段、打印机是否开启 Web 管理
