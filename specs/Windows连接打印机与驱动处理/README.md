# Windows连接打印机与驱动处理

把“确认打印机地址、找到型号、找对驱动、在 Windows 里连上并验证”拆成可复用的小能力。

## 推荐工具

- Windows 打印机设置
  官方链接：[Add or install a printer in Windows](https://support.microsoft.com/en-us/windows/add-or-install-a-printer-in-windows-cc0724cf-793e-3542-d1ff-727e4978638b)
- PowerShell PrintManagement
  官方链接：[Add-PrinterPort](https://learn.microsoft.com/en-us/powershell/module/printmanagement/add-printerport?view=windowsserver2025-ps)
- 厂家官方驱动页面
  官方链接：[HP](https://support.hp.com/us-en/drivers) / [Brother](https://support.brother.com/) / [Canon 中国](https://www.canon.com.cn/support/) / [Canon U.S.](https://www.usa.canon.com/support/software-and-drivers) / [Epson](https://epson.com/support/epson-printer-drivers) / [Xerox](https://www.support.xerox.com/)

## 最小使用方式

1. 先确认打印机的 IP、主机名或连接方式
2. 访问打印机 Web 页面或机身面板，确认准确型号
3. 按型号去厂家官网找对应 Windows 驱动
4. 在 Windows 中按 IP 或主机名添加打印机并验证打印

## 包含的能力

- [01-确认打印机地址与连接方式](./01-确认打印机地址与连接方式)
- [02-访问打印机Web页并确认型号](./02-访问打印机Web页并确认型号)
- [03-查找并安装正确驱动](./03-查找并安装正确驱动)
- [04-在Windows添加打印机并验证打印](./04-在Windows添加打印机并验证打印)
