# Environment Setup

这个能力要解决的是：用 Docker 稳定拉镜像、跨平台构建二进制，并在需要时走国外代理。

## 1. 必要工具

- Docker Engine 或 Docker Desktop
- Docker Buildx
- 一个可用终端

## 2. 官方安装入口

- Docker 安装文档: [https://docs.docker.com/engine/install/](https://docs.docker.com/engine/install/)
- Docker Buildx 文档: [https://docs.docker.com/build/building/multi-platform/](https://docs.docker.com/build/building/multi-platform/)
- Docker daemon 代理文档: [https://docs.docker.com/engine/daemon/proxy/](https://docs.docker.com/engine/daemon/proxy/)
- Docker registry mirror 文档: [https://docs.docker.com/docker-hub/image-library/mirror/](https://docs.docker.com/docker-hub/image-library/mirror/)

## 3. 安装方法

### Docker

- Windows：
  安装 Docker Desktop，并确认 `docker version`、`docker buildx version` 可用。
- Linux：
  按官方文档安装 Docker Engine，再确认当前用户能运行 `docker ps`。
- macOS：
  安装 Docker Desktop。

## 4. 安装后检查

- `docker version`
- `docker buildx version`
- `docker info`
- `docker pull hello-world`

## 5. 和这个能力的关系

- 必须依赖：Docker、Buildx
- 常用增强：BuildKit、QEMU、多阶段构建
- 镜像加速优先用当前网络环境里已验证可用的地址，不把单个第三方镜像源写死成唯一答案

## 6. 常见问题

- 问题：拉镜像很慢
  排查：确认是否已经配置镜像加速或 daemon 代理
- 问题：能构建但架构不对
  排查：确认 `--platform` 和输出文件架构
- 问题：静态编译后仍缺库
  排查：确认链接方式，不要把动态依赖误当成静态产物
