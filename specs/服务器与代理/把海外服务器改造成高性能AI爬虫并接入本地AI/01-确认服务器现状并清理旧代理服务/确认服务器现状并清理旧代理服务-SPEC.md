# 确认服务器现状并清理旧代理服务 SPEC

## 目标

把“这台机器以前做代理”变成一组可验证事实，安全释放旧代理占用的资源，同时保留明确回滚点。

## 执行前必读

- 上级 README.md
- 上级 environment-setup.md
- 上级 tools-and-safety.md
- 用户明确提供的服务器地址、SSH 端口和登录方式

缺少服务器地址、SSH 登录方式或服务器唯一目标时，标记为 missing 并停止变更。

## 1. 建立保底连接

先验证当前 SSH 会话，再开启第二个会话保持不退出。记录当前 sshd 监听，不在本步骤修改 SSH 端口、认证方式或防火墙。

    whoami
    hostname
    date -Is
    ss -lntp
    systemctl status sshd --no-pager || systemctl status ssh --no-pager

## 2. 采集事实基线

至少采集：

    uname -a
    nproc
    lscpu
    free -h
    swapon --show
    df -h
    df -i
    ulimit -n
    systemctl --type=service --state=running --no-pager
    systemctl list-unit-files --state=enabled --no-pager
    ss -lntup
    docker ps -a
    docker stats --no-stream

同时检查最近是否有 OOM、磁盘、内核或服务异常：

    journalctl -p warning..alert --since "24 hours ago" --no-pager
    journalctl -k --since "24 hours ago" --no-pager

输出必须区分：

- 系统必需服务
- SSH 管理服务
- 已确认的代理服务
- 其他业务服务
- 未知服务，保持不动并标记 missing

## 3. 定位旧代理

从以下证据交叉确认，而不是只看名字：

- systemd unit 的 ExecStart 和 EnvironmentFile
- Docker 容器镜像、端口、挂载和 compose labels
- ss 显示的监听端口与进程
- 服务配置目录
- journal 日志

常见名字可能包括 xray、sing-box、hysteria、v2ray、nginx、haproxy 或自定义名称，但名字本身不是删除依据。

## 4. 保存回滚点

回滚材料至少包含：

- systemd unit 和 drop-in
- compose.yaml、env 文件和服务配置
- 当前镜像名与 digest
- 当前启用状态、端口和启动命令
- 备份时间和恢复命令

备份放在服务器的私有目录，权限仅限管理员。仓库只记录备份位置和摘要，不保存秘密原文。

## 5. 停用而不是立即销毁

对已经确认且不再需要的服务，按依赖顺序执行：

    systemctl stop SERVICE_NAME
    systemctl disable SERVICE_NAME

容器服务先用原 compose 项目停止，并保留镜像和卷作为第一阶段回滚点。确认爬虫稳定运行一段时间后，再由用户单独决定是否清理旧数据。

不要停用：

- sshd 或 ssh
- Docker
- 网络、DNS、时间同步
- 当前不确定用途的服务

## 6. 清理后验证

重新从本地建立一个全新 SSH 会话，然后检查：

    systemctl --failed --no-pager
    systemctl --type=service --state=running --no-pager
    ss -lntup
    free -h
    docker ps -a

完成标准：

- 新 SSH 会话可以登录
- 旧代理 unit 和容器不再运行
- 旧代理公网端口不再监听
- 未出现新的 failed unit
- 释放的内存和 CPU 有前后对比
- 回滚材料存在且恢复方法明确

## 输出格式

输出一份简短基线：

1. 服务器规格
2. 清理前服务与监听
3. 已停用项目及证据
4. 清理后服务与监听
5. 回滚位置
6. missing 或仍需用户判断的项目
