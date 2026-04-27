# Environment Setup

这个能力要解决的是：让 AI 直接在命令行里批量管理多台服务器。

## 1. 必要工具

- Ansible
- SSH
- 一个可用终端

## 2. 官方安装入口

- Ansible 安装文档: [https://docs.ansible.com/ansible/2.10/installation_guide/](https://docs.ansible.com/ansible/2.10/installation_guide/)

## 3. 安装方法

### Ansible

- Linux：
  按官方安装文档安装 Ansible。
- Windows：
  优先在 WSL 或 Linux 控制端使用 Ansible。
- macOS：
  按官方文档安装，也可以使用 Homebrew。

## 4. 安装后检查

- `ansible --version`
- `ansible all -i '127.0.0.1,' -m ping`

## 5. 和这个能力的关系

- 必须依赖：Ansible、SSH
- 常见输入：inventory、私钥、分组、目标主机变量

## 6. 常见问题

- 问题：连不上机器
  排查：先确认 SSH、端口、用户和密钥
- 问题：playbook 跑了但机器没变
  排查：先看模块参数和目标分组是否写对
