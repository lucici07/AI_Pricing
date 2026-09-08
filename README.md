# GA Repricing Platform — Prototype

三层可点击原型，基于《GA Repricing Process Overview》的 Solution 部分（p.8–16）：

| Layer | 内容 | 角色 |
|---|---|---|
| **1 · Repricing** | Sale 提交并打 Tag → Pricer 自动算价（line-by-line margin，flag RTX 等特殊 CPU）→ 直接批 / 转 Profit Manager | Sale · Pricer · Profit Manager |
| **2 · Tracking**（PowerApps） | Sale 看板 + 确认表单；PM / Director 颜色看板（黄=待处理、蓝=RPG、绿=已批、红=拒绝）；Director 侧带一个有数据源支撑的影响计算器 | Sale · Profit Manager · Director/CFO |
| **3 · Reporting**（Power BI） | GA 分解树 + GTP 按 vertical 拆分；exception / missing input 明细表 | GA · GTP |

三层共用同一份 account + bid 状态，一处操作会同步到其它层。右上角 **Activity log** 记录每一步。

## 技术栈

- **纯前端单文件**：`index.html`，无构建步骤、无后端、无依赖安装。
- 唯一的外部资源是 Google Fonts（Newsreader / IBM Plex）——离线时会自动回退到系统字体。
- 数据全部是写死在文件里的演示数据（账户名、PN、价格均为虚构）。

## 本地打开

直接双击 `index.html`，或用 VS Code 的 Live Server 打开。

## 用 GitHub Pages 托管

代码和**自动部署流水线**（`.github/workflows/deploy.yml`）都已经在 `main` 分支上。
每次 `git push`，GitHub Actions 会自动把网站发布到 Pages，不需要再手动操作。

只剩下一次性开关，这个只能仓库 owner 在网页上点（GitHub 不允许别人代操作）：

1. **仓库是 private 的话先改 public** —— `Settings → General → Danger Zone → Change repository visibility → Public`
   （免费账号的 Pages 只支持 public 仓库；本站内容全是虚构演示数据，可以公开。有 GitHub Pro 则可跳过这步。）
2. **Settings → Pages → Build and deployment → Source** 选 **`GitHub Actions`**
3. 回到 **Actions** 标签，等那条 “Deploy to GitHub Pages” 跑完（约 1 分钟）

站点地址：**https://lucici07.github.io/AI_Pricing/**

之后每次改完 `index.html`：

```bash
git add -A && git commit -m "update" && git push
```

推上去就自动重新部署。

## 文件说明

| 文件 | 作用 |
|---|---|
| `index.html` | 整个网站（HTML + CSS + JS 全在里面） |
| `.nojekyll` | 让 GitHub Pages 原样发布静态文件，不走 Jekyll |
| `README.md` | 本说明 |

同一个原型也发布在 Claude Artifact：<https://claude.ai/code/artifact/63a32f45-6dcc-40bd-badb-f4bc5b5d12c2>
