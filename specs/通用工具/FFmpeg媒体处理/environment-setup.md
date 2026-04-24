# Environment Setup

这个能力要解决的是：在命令行里完成常见音视频处理。

## 1. 必要工具

- FFmpeg
- FFprobe
- 一个可用终端

## 2. 官方安装入口

- FFmpeg 文档: [https://ffmpeg.org/documentation.html](https://ffmpeg.org/documentation.html)
- FFmpeg 下载页: [https://ffmpeg.org/download.html](https://ffmpeg.org/download.html)

## 3. 安装方法

### FFmpeg

- Windows：
  按官方下载页选择可信发行包，安装后把 `ffmpeg` 和 `ffprobe` 加入 PATH。
- Linux：
  Debian / Ubuntu: `sudo apt-get update && sudo apt-get install -y ffmpeg`
- macOS：
  `brew install ffmpeg`

## 4. 安装后检查

- `ffmpeg -version`
- `ffprobe -version`
- `ffprobe <media-file>`

## 5. 和这个能力的关系

- 必须依赖：FFmpeg、FFprobe
- 可选依赖：播放器、批处理脚本

## 6. 常见问题

- 问题：命令能跑但文件不能播
  排查：先用 `ffprobe` 看输出编码、时长、流信息
- 问题：找不到命令
  排查：确认 PATH 和终端已刷新
