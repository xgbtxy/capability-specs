# environment-setup

## 目标

让执行者具备运行“有效插件集合发布”能力所需的最小环境。

---

## 1. 必要软件

### 1.1 Git

要求：

- 本机已安装 Git
- 支持 `git worktree`
- 支持 `git credential fill`

建议版本：

- Git for Windows 最新稳定版

验证方式：

```powershell
git --version
git worktree --help
git credential fill
```

---

### 1.2 PowerShell

建议使用：

- PowerShell 7+

验证方式：

```powershell
pwsh --version
```

---

### 1.3 Python

建议安装：

- Python 3.10+

用途：

- 处理 `vuln_registry.csv`
- 生成 include 清单
- 辅助统计 `.yak` 与 `fingerprint.json` 数量

验证方式：

```powershell
python --version
```

---

## 2. GitHub 凭据前提

必须满足以下条件之一：

1. 本机 `git push` 到 GitHub 正常
2. 本机 `git credential fill` 能返回 GitHub 可用凭据

验证方式：

```powershell
git credential fill
```

输入示例：

```text
protocol=https
host=github.com
path=owner/repo.git
username=<your-username>

```

注意：

- 若返回 `username` 和 `password`，说明凭据链可用
- 这里的 `password` 可能是 PAT
- 不要把该结果写入仓库

---

## 3. 仓库前提

目标仓库需要满足：

- 本地已有可写 checkout
- 远端 GitHub 仓库存在
- 当前账号具备：
  - push 权限
  - PR 创建权限

建议验证：

```powershell
git remote -v
git push --dry-run
```

---

## 4. 非必需工具

以下工具不是必须的：

- `gh`
- GitHub MCP 连接器
- Playwright

本能力默认不依赖上述工具。

---

## 5. 推荐目录准备

建议存在以下目录：

```text
工作区/
├─ VulKit/
├─ 临时工作区/
├─ 收集的最新漏洞/
└─ workflows/
```

其中：

- `VulKit/`：正式仓库
- `临时工作区/`：发布 worktree 和 include 清单输出目录
- `收集的最新漏洞/`：台账与注册表数据源
- `workflows/`：脚本入口目录

---

## 6. 推荐检查清单

在正式执行发布前，建议确认：

- [ ] Git 已安装
- [ ] PowerShell 可用
- [ ] Python 可用
- [ ] `git push` 正常
- [ ] `git credential fill` 可返回 GitHub 凭据
- [ ] 本地仓库远端配置正确
- [ ] `vuln_registry.csv` 可读
- [ ] `VulKit/` 正式文件目录可读
