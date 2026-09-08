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

代码已经推到 `main` 分支。**注意：这个仓库目前是 private，GitHub 免费账号的 Pages 只支持 public 仓库。**

### 方案 A — 把仓库改成 public（免费，最简单）

1. **Settings → General →** 最下方 **Danger Zone → Change repository visibility → Public**
   （站点内容全是虚构演示数据，可以公开）
2. **Settings → Pages → Build and deployment**
   - **Source**：`Deploy from a branch`
   - **Branch**：`main` ，文件夹 `/ (root)` → **Save**
3. 等 1–2 分钟，站点上线：**https://lucici07.github.io/AI_Pricing/**

以后改完 `index.html` 再 `git push`，Pages 会自动重新部署。

### 方案 B — 保持 private，用别的免费托管

- **Cloudflare Pages** / **Netlify** / **Vercel**：都能连 private 仓库，免费，自动部署。
  最快的是 Netlify：把整个 `AI_Pricing` 文件夹拖到 <https://app.netlify.com/drop> 就能立刻拿到一个链接。
- 或升级到 **GitHub Pro**，private 仓库就能用 Pages。

## 文件说明

| 文件 | 作用 |
|---|---|
| `index.html` | 整个网站（HTML + CSS + JS 全在里面） |
| `.nojekyll` | 让 GitHub Pages 原样发布静态文件，不走 Jekyll |
| `README.md` | 本说明 |

同一个原型也发布在 Claude Artifact：<https://claude.ai/code/artifact/63a32f45-6dcc-40bd-badb-f4bc5b5d12c2>
