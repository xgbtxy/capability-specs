# Environment Setup

这个能力要解决的是：在不依赖虚机在线安装流程的前提下，离线重建系统盘并把镜像重新瘦身。

## 1. 必要工具

- libguestfs 工具组
- qemu-img
- 一个 Linux 环境

## 2. 官方安装入口

- libguestfs: [https://libguestfs.org/](https://libguestfs.org/)
- virt-sysprep: [https://libguestfs.org/virt-sysprep.1.html](https://libguestfs.org/virt-sysprep.1.html)
- virt-sparsify: [https://libguestfs.org/virt-sparsify.1.html](https://libguestfs.org/virt-sparsify.1.html)
- guestfish: [https://libguestfs.org/guestfish.1.html](https://libguestfs.org/guestfish.1.html)
- qemu-img: [https://www.qemu.org/docs/master/tools/qemu-img.html](https://www.qemu.org/docs/master/tools/qemu-img.html)

## 3. 安装方法

### Linux 环境

- Debian / Ubuntu：
  `sudo apt-get update && sudo apt-get install -y libguestfs-tools qemu-utils`

### 说明

- Windows 不建议作为主环境
- 优先在 Linux 或 WSL2 里处理离线镜像

## 4. 安装后检查

- `guestfish --version`
- `virt-sysprep --version`
- `virt-sparsify --version`
- `qemu-img --version`

## 5. 和这个能力的关系

- 必须依赖：guestfish、virt-sysprep、virt-sparsify、qemu-img
- 可选依赖：额外的系统镜像模板、自动化脚本

## 6. 常见问题

- 问题：镜像能读但处理失败
  排查：先确认镜像没被占用、格式能识别、输出目录空间够
- 问题：镜像重建后还是很大
  排查：先确认是否真的执行了离线稀疏化，而不是只做了文件删除
