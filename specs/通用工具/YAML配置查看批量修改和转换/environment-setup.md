# Environment Setup

这个能力要解决的是：让 AI 直接在命令行里处理 YAML 配置。

## 1. 必要工具

- yq
- 一个可用终端

## 2. 官方安装入口

- yq 项目页: [https://github.com/mikefarah/yq](https://github.com/mikefarah/yq)

## 3. 安装方法

### yq

- Windows：
  按项目页下载对应二进制，并放到 PATH 可访问的位置。
- Linux：
  按项目页说明安装对应发行版包或二进制。
- macOS：
  按项目页说明安装，也可以使用 Homebrew。

## 4. 安装后检查

- `yq --version`
- `yq '. as $x | $x' example.yaml`

## 5. 和这个能力的关系

- 必须依赖：yq
- 常见输入：应用配置、CI 配置、Kubernetes 配置、Docker Compose

## 6. 常见问题

- 问题：字段路径写错
  排查：先用只读查询确认层级
- 问题：批量修改后格式不对
  排查：先输出到新文件，再重新读取关键字段
