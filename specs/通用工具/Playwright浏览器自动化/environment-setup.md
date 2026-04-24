# Environment Setup

这个能力要解决的是：在浏览器里自动化处理真实网站任务。

## 1. 必要工具

- Node.js
- Playwright
- 一个可用浏览器环境

## 2. 官方安装入口

- Playwright: [https://playwright.dev/](https://playwright.dev/)
- Playwright 安装: [https://playwright.dev/docs/intro](https://playwright.dev/docs/intro)

## 3. 安装方法

### Node.js

- Windows：
  安装官方 LTS 版本。
- Linux：
  使用官方安装说明或系统包管理器。
- macOS：
  `brew install node`

### Playwright

- `npm init -y`
- `npm install -D playwright`
- `npx playwright install`

## 4. 安装后检查

- `node --version`
- `npx playwright --version`

## 5. 和这个能力的关系

- 必须依赖：Node.js、Playwright
- 可选依赖：浏览器账号、测试数据

## 6. 常见问题

- 问题：脚本能跑但页面状态不对
  排查：先看等待条件、登录态和选择器是否稳定
