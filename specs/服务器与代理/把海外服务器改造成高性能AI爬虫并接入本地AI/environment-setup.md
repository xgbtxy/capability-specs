# environment-setup

## 远程服务器

- Linux 服务器，已经能通过 SSH 登录
- 推荐使用 systemd 管理 Docker 和持久服务
- 已安装 Docker Engine 与 Docker Compose 插件
- 磁盘能容纳镜像、浏览器缓存、日志和爬取产物
- 能从服务器访问待爬目标

最小检查：

    uname -a
    nproc
    free -h
    df -h
    ss -lntup
    docker version
    docker compose version

## 本地环境

- 默认按 Windows + PowerShell 执行
- OpenSSH 客户端可用
- Python 3 可用
- 可以把 crawlerctl 放入 PATH
- AI 客户端支持读取项目说明或安装本地 Skill

最小检查：

    ssh -V
    python --version
    crawlerctl --version

## 必需输入

执行前必须明确这些值，缺少时标记为 missing，不要猜：

- SERVER_HOST
- SSH_USER
- SSH_PORT
- SSH_KEY_PATH 或其他 SSH 登录方式
- REMOTE_CRAWLER_PORT，默认可用 11235
- LOCAL_TUNNEL_PORT，例如 11236
- CRAWL4AI_VERSION
- API_TOKEN
- 服务器原有代理服务名和配置路径

所有秘密只进入本机私有配置、环境变量或服务器私有 env 文件，不进入 Git。

## 版本策略

- 首选当前 Crawl4AI 官方自托管镜像和公开 API
- 部署前读取当前版本的 self-hosting 文档、迁移文档、OpenAPI、Schema 和容器内源码
- 已验证的完整能力改造基线是 Crawl4AI 0.9.1；其他版本必须重新定位限制点并重跑全部验收
- 镜像至少固定版本，生产复现时进一步记录 digest
