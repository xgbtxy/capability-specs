# Environment Setup

这个能力要解决的是：识别离线镜像、提取文件、转换格式、恢复 Linux 访问。

## 1. 必要工具

- QEMU 工具组（至少有 `qemu-img`）
- libguestfs 工具组（至少有 `guestfish`、`guestmount`）

## 2. 官方安装入口

- QEMU: [https://www.qemu.org/download/](https://www.qemu.org/download/)
- qemu-img 文档: [https://www.qemu.org/docs/master/tools/qemu-img.html](https://www.qemu.org/docs/master/tools/qemu-img.html)
- libguestfs: [https://libguestfs.org/](https://libguestfs.org/)
- guestfish: [https://libguestfs.org/guestfish.1.html](https://libguestfs.org/guestfish.1.html)
- guestmount: [https://libguestfs.org/guestmount.1.html](https://libguestfs.org/guestmount.1.html)

## 3. 安装方法

### QEMU

- Windows：
  建议安装官方或可信发行版后，确认 `qemu-img.exe` 已加入 PATH。
- Linux：
  Debian / Ubuntu: `sudo apt-get update && sudo apt-get install -y qemu-utils`
- macOS：
  `brew install qemu`

### libguestfs

- Windows：
  不建议作为主环境，优先在 Linux 虚机、WSL2 或真实 Linux 上执行。
- Linux：
  Debian / Ubuntu: `sudo apt-get update && sudo apt-get install -y libguestfs-tools`
- macOS：
  优先改用 Linux 环境；如果必须本机处理，先确认 Homebrew 方案是否满足你的镜像格式需求。

## 4. 安装后检查

- `qemu-img --version`
- `qemu-img info <image>`
- `guestfish --version`
- `guestmount --version`

## 5. 和这个能力的关系

- 必须依赖：`qemu-img`、`guestfish` / `guestmount`
- 可选依赖：`qemu-nbd`、`7z`

## 6. 常见问题

- 问题：`qemu-img info` 读不到镜像
  排查：先确认路径、权限、镜像是否损坏
- 问题：`guestmount` 挂载失败
  排查：先用 `guestfish -i <image>` 看分区是否能识别
- 问题：Windows 环境下工具不全
  排查：优先切到 Linux 或 WSL2 环境执行
