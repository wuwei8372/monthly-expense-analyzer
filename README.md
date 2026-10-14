# 月度开销分析 (Monthly Expense Analyzer)

一个**完全在浏览器本地运行**的月度开支分析工具：上传银行 / 信用卡账单（CSV / OFX / QFX / 文本型 PDF），自动算出 **FIRE 口径**的真实月度开销——自动去重、自动排除还款、转账与退款。

> 这是 [Crazy WW](https://www.youtube.com/) 频道「FIRE 工具」系列的第一个开源小工具，
> 由 Muse（AI 编程助手）结对开发。

## 为什么敢说"隐私安全"？

因为代码里**没有任何网络请求**：

- ✅ 零外部资源：无 CDN、无字体、无统计代码，单文件离线可运行
- ✅ 零网络 API：代码中没有 `fetch` / `XMLHttpRequest` / `WebSocket`，你的账单数据**不可能**被发送到任何地方
- ✅ 零本地存储：没有 `localStorage` / `IndexedDB` / `Cookie`，数据只在页面内存中，**关闭或刷新页面即清空**

不信？两步验证：

1. 打开浏览器 DevTools → Network 面板，上传账单，全程**零请求**；
2. 直接读源码：`index.html` 是唯一的源文件，搜索 `fetch(`、`http` 即可确认。

## 快速开始

**方式一：直接打开**

下载 `index.html`，双击用浏览器打开即可（无需联网、无需安装）。

**方式二：GitHub Pages（推荐，可分享给朋友）**

1. 把本仓库 Fork / 上传到你的 GitHub；
2. Settings → Pages → Deploy from branch → 选择 `main` 分支 → Save；
3. 得到 `https://<你的用户名>.github.io/monthly-expense-analyzer/`，打开即用。

**先用演示数据试试**（均为虚构数据）：

1. 打开页面，把 `demo-data/` 下的两个 CSV 文件拖进去；
2. 应该看到：FIRE 口径支出 **$1,587.14**，年化 **$19,045.68**，19 笔计入 / 6 笔排除（含 1 笔跨文件重复自动去重）。

## 功能

- 📥 导入 CSV / OFX / QFX / 文本型 PDF 账单（Chase 等银行导出的 CSV 可直接用）
- 🧹 自动排除：信用卡还款、退款、转账（含 Zelle）、工资入账等非消费
- 🔁 跨文件自动去重（日期 + 商户 + 金额完全相同即判重）
- 📊 月度 FIRE 口径支出、年化基线、分类占比、交易明细
- ✏️ 分类可手动调整；月份可切换

### CSV 格式说明

表头需包含日期、描述、金额三列（大小写不敏感），例如：

```csv
Transaction Date,Description,Amount
09/01/2026,Whole Foods,85.32
```

- 文件名含 `card` / `credit`，或表头含 `Transaction Date`，即按**信用卡账单**处理（金额取绝对值）；
- 普通 checking 账单中，正金额视为入账（工资、转账存入等），自动排除。

## 免责声明

本工具为个人经验分享，仅用于记录与分析开支，**不构成任何投资建议**。FIRE 口径支出基于 4% 法则等简化假设，实际退休规划请咨询专业人士。

## License

MIT — 详见 [LICENSE](LICENSE)。

---

## English Summary

A **100% client-side** monthly expense analyzer for FIRE planning: drop in bank/credit-card statements (CSV/OFX/QFX/text PDF) and get your true monthly spending — auto-deduped, with repayments, transfers and refunds excluded.

**Privacy by construction:** single self-contained `index.html`, zero external resources, zero network calls (`fetch`/`XHR`/`WebSocket` — none), zero local storage. Data lives only in page memory and is wiped on refresh. Verify it yourself in DevTools → Network (zero requests) or by reading the source.

**Try it:** open `index.html` in any browser, or deploy free via GitHub Pages. Sample (fictional) data in `demo-data/` should yield **$1,587.14** FIRE-basis spending for September.

Built with Muse (AI pair-programming) for the Crazy WW channel. MIT licensed. Personal experience only — not investment advice.
