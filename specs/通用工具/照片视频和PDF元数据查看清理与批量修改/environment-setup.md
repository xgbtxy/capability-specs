# Environment Setup

这个能力要解决的是：让 AI 直接在命令行里处理素材元数据。

## 1. 必要工具

- ExifTool
- 一个可用终端

## 2. 官方安装入口

- ExifTool 文档: [https://exiftool.org/index.html](https://exiftool.org/index.html)

## 3. 安装方法

### ExifTool

- Windows：
  按官方文档下载对应可执行文件，并放到 PATH 可访问的位置。
- Linux：
  按官方文档或发行版包安装。
- macOS：
  按官方文档安装，也可以使用 Homebrew。

## 4. 安装后检查

- `exiftool -ver`
- `exiftool sample.jpg`

## 5. 和这个能力的关系

- 必须依赖：ExifTool
- 常见输入：照片、视频、PDF
- 常见输出：元数据摘要、清理后的文件、批量修改结果

## 6. 常见问题

- 问题：批量修改后时间不对
  排查：先确认源字段和目标字段对应关系
- 问题：担心破坏原素材
  排查：先对副本操作，或先导出元数据清单
