# GA Repricing Platform — Prototype

可点击原型，基于《GA Repricing Process Overview》的 Solution 部分（p.8–16）。

| Tab | 内容 | 角色 |
|---|---|---|
| **1 · LBP · RPT** | Sale 在 LBP 提交 bid，**Bid Type = Repricing / Exception**，Fulfillment = Direct / Indirect。Pricer / PM / Director 点开单个 bid → bid 详情页里有 **RPT** 和 **LPS** 两个工具按钮（不在列表页）。RPT 三个角色长一样：Run → 结果 → Sync to LPS → copy pricing note → Save record（**不做审批**）。**Repricing 的 approve / reject 在 LBP 详情页**，点完弹一个留 comment 的框（Sale 能看到这段 pricer feedback）；不需要先开 RPT。Exception 在 LBP 只有 **Reassign**（PM↔Director）。 | Sale · Pricer · Profit Mgr · Director/CFO · RPT records |
| **2 · Tracker**（PowerApps，独立 app） | LBP 里的 **Sync to Tracker** 小窗口写进这里。**PM 在 Tracker 填 exception 内容**（past performance / 附件），点 **Save**（存草稿）或 **Send**（→ 进 Director 的 Tracker）。**Director 在 Tracker 有 Approve / Reject 按钮** + KPI 计算器，点完带 note，结果回 PM + Sale（未读）。Sale / PM / Director 三个颜色看板（黄=待处理、蓝=Repricing、绿=已批、红=拒绝，黄色排最前）。有 **+ Add new**：LBP 没同步过来的 bid 可手动加，账户只能选 Main Table 里已有的。 | Sale · Profit Mgr · Director/CFO |
| **3 · Reporting**（Power BI） | 右上角显示今天日期。GA 分解树 / GTP 按 vertical 拆分。Exception 按 **uplift** 分类：**Partial Uplift → Partial Exception**、**No Uplift → Full Exception**；exception 明细表有 Geo / Vertical / **Exception class** 三个筛选 + Partial/Full Exception 的 sizing（Accts / Rev / GP / GP Impact），列对齐截图（HQ Geo · ISR · GAM · Valid Date · CA No. · Exc REV · GP · GP Impact）。 | GA · GTP |

**Uplift 模型**：Sale 在 Tracker form 里选 Full Uplift / Partial Uplift / No Uplift。Full Uplift = 普通 Repricing；Partial / No Uplift 自动变成 Partial / Full Exception 并路由给 PM。PM / Director 在各自的 Tracker 页可以看到并**改** Sale 填的所有字段（active / uplift / valid date / LNL / CA No.）。Sale 的 Tracker 页只显示自己填的信息 + 上一个负责的 Sale / PM + 账户状态。

三个 tab 共用同一份 account + bid + RPT record 状态。右上角 **Activity log** 记录每一步。

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
