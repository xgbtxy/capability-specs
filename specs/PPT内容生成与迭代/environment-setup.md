# Environment Setup

这个能力要解决的是：把输入材料生成或更新成真正可编辑的 `.pptx`。

## 1. 必要工具

- Node.js
- npm
- PptxGenJS

## 2. 官方安装入口

- Node.js: [https://nodejs.org/](https://nodejs.org/)
- Node.js 安装说明: [https://nodejs.org/en/download](https://nodejs.org/en/download)
- PptxGenJS 文档: [https://gitbrent.github.io/PptxGenJS/docs/introduction/](https://gitbrent.github.io/PptxGenJS/docs/introduction/)
- PptxGenJS npm: [https://www.npmjs.com/package/pptxgenjs](https://www.npmjs.com/package/pptxgenjs)

## 3. 安装方法

### Node.js

- Windows：
  安装官方 LTS 版本即可。
- Linux：
  可参考官方安装页，或在 Debian / Ubuntu 上使用系统包管理器安装 `nodejs` 和 `npm`。
- macOS：
  `brew install node`

### PptxGenJS

- 新建一个脚本目录后执行：
  `npm init -y`
- 安装：
  `npm install pptxgenjs`

## 4. 安装后检查

- `node --version`
- `npm --version`
- `npm list pptxgenjs`

## 5. 和这个能力的关系

- 必须依赖：Node.js、npm、PptxGenJS
- 可选依赖：Markdown 解析脚本、图表脚本、图片处理工具

## 6. 常见问题

- 问题：`node` 或 `npm` 不可用
  排查：重新打开终端，确认 PATH 已更新
- 问题：`npm list pptxgenjs` 看不到包
  排查：先确认当前目录是不是安装过依赖的脚本目录
- 问题：PPT 能生成但版式不好
  排查：先缩小到最小样例，确认模板、字体、页面尺寸是否写对
