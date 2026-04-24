# 离线重装虚拟机系统与镜像瘦身

把“离线重建干净系统盘、清理历史痕迹、再把镜像重新瘦身”拆成可复用的小能力。

## 推荐工具

- virt-sysprep
  官方链接：[virt-sysprep](https://libguestfs.org/virt-sysprep.1.html)
- virt-sparsify
  官方链接：[virt-sparsify](https://libguestfs.org/virt-sparsify.1.html)
- qemu-img
  官方链接：[qemu-img](https://www.qemu.org/docs/master/tools/qemu-img.html)
- guestfish
  官方链接：[guestfish](https://libguestfs.org/guestfish.1.html)

## 最小使用方式

1. 先确认原镜像、目标系统和输出镜像
2. 离线重建干净系统盘
3. 离线清理无用数据和历史痕迹
4. 离线稀疏化镜像并验证体积变化

## 包含的能力

- [01-确认离线重装输入与输出](./01-确认离线重装输入与输出)
- [02-离线重建干净系统盘](./02-离线重建干净系统盘)
- [03-离线清理历史痕迹与无用数据](./03-离线清理历史痕迹与无用数据)
- [04-离线稀疏化并验证镜像体积](./04-离线稀疏化并验证镜像体积)
