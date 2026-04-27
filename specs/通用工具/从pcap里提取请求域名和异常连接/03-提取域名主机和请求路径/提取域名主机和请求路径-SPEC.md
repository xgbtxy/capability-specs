# 提取域名主机和请求路径

## 目标

优先抽这些字段：

- HTTP host
- HTTP request uri
- TLS SNI
- DNS query

## 重点

- 先把和目标功能有关的主机列出来
- 再把请求路径和方法关联上
