# Environment Setup

这个能力要解决的是：用命令行处理压缩、解压、分卷、加密和交付。

## 1. 必要工具

- 7-Zip
- 一个可用终端

## 2. 官方安装入口

- 7-Zip 主页: [https://www.7-zip.org/](https://www.7-zip.org/)
- 7-Zip 下载页: [https://www.7-zip.org/download.html](https://www.7-zip.org/download.html)

## 3. 安装方法

### 7-Zip

- Windows：
  安装官方版本后，确认 `7z.exe` 可用。
- Linux：
  Debian / Ubuntu 可安装 `p7zip-full`
- macOS：
  `brew install p7zip`

## 4. 安装后检查

- `7z`
- `7z i`

## 5. 和这个能力的关系

- 必须依赖：7-Zip 命令行
- 可选依赖：图形界面 7-Zip、校验命令、额外脚本

## 6. 常见问题

- 问题：系统里装了 7-Zip 但命令行不可用
  排查：确认 `7z.exe` 是否在 PATH 中
- 问题：压缩包能生成但别人打不开
  排查：先本地测试解压和密码，再交付
