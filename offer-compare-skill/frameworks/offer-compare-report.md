# Offer Compare Report — HTML 报告规格

把 Breakdown + Dimension Compare + Hidden Signals + Risk Analysis + Recommendation 融合成**一份可分享的单文件 HTML 报告**，Step 3 一口气生成并 `open` 弹到浏览器。

参考骨架：[../examples/offer-compare-template.html](../examples/offer-compare-template.html)

---

## 双语输出 · Bilingual output（必须）

模板右下角有一个 中文 / EN 切换按钮，靠 CSS 根据 `<html lang>` 属性切换 `[data-lang="en"]` / `[data-lang="zh"]`。**你写进占位符的每一句用户可见拷贝**都必须产出双语：

```html
<span data-lang="en">English version</span><span data-lang="zh">中文版本</span>
```

**适用范围：**
- Verdict / 主推荐 一句话 / ⭐ 决心指数副标
- Offer breakdown 每行 note
- Dimension compare 每维的 winner note + a_note + b_note
- Hidden signals 5 张卡里的 verdict / for / against
- Risk analysis 每条 risk 的 name / reason / if_realized / mitigation
- Recommendation 4 block 的所有 body
- "If you are X → A / If Y → B" 分叉判定
- Next 72 hours 4 条动作

**不用双语：** 数字 / 百分比 / 币种 / 人名 / 公司名 / 职位名 / 静态模板标签（已在 HTML shell 里）。

**英文版在前，中文版在后**。归 span 就用 span，归 li/p/td 就在内部放两个 span。

---

## 何时生成

- Step 3 default 产出 — 收齐 Offer A + Offer B 后立刻生成，不再请示。
- 用户单独要"给我出一份 HTML 报告" → 前提 breakdown + dimension + recommendation 至少都在内存里跑过。
- 用户补充信息（priorities 变了 / 新的谈判结果）→ 重新生成同文件名（覆盖）。

---

## 文件位置 + 命名

| 优先级 | 路径 |
|---|---|
| 1（默认） | `~/Desktop/Claude skills/offer-compare-<companyA-slug>-vs-<companyB-slug>-<YYYYMM>.html` |
| 2（兜底） | 本 skill 内 `offer-bank/<同名>.html`（用户桌面没这个目录时） |

**Slug 规则：** 全小写 · 空格换 `-` · 去掉常见后缀（Inc / LLC / .com）。例：`openai-vs-anthropic-senior-designer-202607.html`。

---

## 报告骨架（必须按此顺序）

### 报告头（章节前）

1. **Header** — "Offer Compare · {A_COMPANY} vs {B_COMPANY}" 大标题 + 候选人一句话画像（e.g., "Senior Product Designer · 8 yrs · SF · 现在 Adobe"）
2. **Meta strip** — 两份 offer 的 role / level / location / TC midpoint（四栏对照）
3. **Inside (TOC)** — 7 条：`#tldr` `#assumptions` `#metrics` `#breakdown` `#dimensions` `#signals` `#risks` `#recommendation`
4. **⚠️ Assumptions** — 显式列所有假设（RSU vest schedule / 币种汇率 / bonus target 假设 / refresh 假设 / 股价波动带 / 用户 priorities 权重来源）· 每条独立成行 · 明确写"任一不对，告诉我重新生成"
5. **Verdict** — 一句话推荐（"接 Offer B"）+ 3 行展开 + ⭐ 决心指数
6. **Two Gauges（并排）** — 左：Offer A 加权总分（0-100）· 右：Offer B 加权总分。中间标 "**{DELTA_TEXT}**"（e.g., "B leads by 14 pts"）

### 正文 5 节（按编号顺序）

1. **§1 · Offer Breakdown** — `#breakdown`
   两份 offer **并排对照表**（3 列：Metric / A / B），行：Base · Bonus · RSU (Y1 vest) · Sign-on · Y1 total · **4-yr TC (low ~ high)** · Equity Risk · Stability · Comp Quality Type · Currency
   + 底下加一段 **"数字之外的一句话"**：解释 4-yr TC 区间 low/high 的假设是什么

2. **§2 · Dimension Comparison** — `#dimensions`
   7 维卡片式对比：
   - 每维一行：图标 + 名字 · A 分 · B 分 · Winner badge · 一句话说明
   - 每行下有小 bar 视觉化 A vs B（10 分制 bar）
   - 结尾：加权总分 gauge（如报告头已放，此处只放解释文字：加权公式 + 用户 priorities 说明）

3. **§3 · Hidden Signals** — `#signals`
   5 张卡片：Front-loaded · Long-term Upside · Uncertainty · Resume Value · Switch-out
   每张卡片：Signal 名 + 🏆 Winner + Verdict 一句话 + "For you if" + "Against"

4. **§4 · Risk Analysis** — `#risks`
   两列并排（A 一列、B 一列），每列 4-6 张 risk 卡：
   - Risk 名 · Severity badge（high / medium / low 颜色区分）· Category（Equity / Role / Team / Market / Life）
   - Reason · If Realized · Mitigation
   - 每列顶部放"总风险画像"一句话（"A 整体 medium risk · 主要集中在 team & equity"）

5. **§5 · Recommendation** — `#recommendation`
   4 block（严格顺序）：
   - **主推荐** — 大字加粗（"🎯 接 Offer B"）+ 3-5 条支撑 + 保留意见
   - **Tradeoff 展开** — 选 X 意味着放弃什么
   - **"If you are X → A / If Y → B" 分叉** — 至少 2 条分叉，允许第 3 条 hybrid path
   - **Next 72 hours** — 4 条具体动作

### 报告尾

- ⛔ **Footer（强制项 · 必须用完整签名版，绝不简化）** — `OFFER COMPARE.` brand mark + `Created by Dreameryanyan · Offer Decision Advisor` 副标题 + 三个社交圆形按钮（LinkedIn / X / 小红书）+ meta 行（生成时间 · 两家公司 × 岗位 · 候选人 · 决策方法学引用 · "no fabricated facts" 声明）+ offer-bank markdown 文件链接。
  - **这是作者署名，不是可选装饰。** 生成时**直接抄本文件末尾的「📌 强制 Footer 区块」**（HTML + CSS 都在），把 `{{...}}` 占位符填好即可，不要凭记忆重写。
  - 写完文件后**自检**：必须能搜到 `Dreameryanyan` / `brand-mark` / `yanliudreamer` / `xiaohongshu` 四个关键词，缺一个就是 footer 丢了。

---

## 视觉规范（必须保留）

### 色板（与 JD Skill 保持同一 design language）
- 底色：`#fafaf7` / `#faf8f3` cream/sand
- 卡片背景：`#fff8e6` / `#fef0d4` 暖米
- 文字主色：`#1f1f1d` / `#2a2308` 深棕近黑
- 文字次色：`#6b6b66` 中灰
- **Winner 绿：** `#18a957` / `#0d8a45`
- **Warn 橙：** `#d97706` / `#f59e0b`（假设 · medium risk）
- **Stop 红：** `#c2410c` / `#d11838`（high risk · lose）
- **Accent 黄：** `#facc15`（品牌色 · brand mark 点 · ⭐）
- 边框：`#ebebe4` / `#d9d9d2`

**Offer A / Offer B 主色对比（贯穿全报告）：**
- **Offer A：** 深蓝 `#1e40af` / `#3b82f6` accent
- **Offer B：** 深绿 `#065f46` / `#059669` accent
（这样每张 gauge、每个 bar、每个 header 一眼能分清 A / B）

### 字体系统（CSS variables · 跟 JD Skill 保持一致）

```css
--display: "SF Pro Display", -apple-system, "Helvetica Neue", "Noto Sans SC", "PingFang SC", sans-serif;
--serif:   "Times New Roman", "Noto Serif SC", "Songti SC", Georgia, serif;
--body:    -apple-system, BlinkMacSystemFont, "SF Pro Text", "Helvetica Neue", "Noto Sans SC", "PingFang SC", "Microsoft YaHei", sans-serif;
--mono:    "SF Mono", "JetBrains Mono", Menlo, "Noto Sans SC", monospace;
```

**⚠️ CJK 字体必须用 Noto Sans SC / Noto Serif SC（强制 Google Fonts 外链）** —— PingFang SC / Songti SC 无法嵌入 PDF，会导致导出的 PDF 里中文变成空白。**这是单文件零依赖原则的唯一例外。**

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Noto+Sans+SC:wght@400;500;700;900&family=Noto+Serif+SC:wght@400;700;900&display=swap" rel="stylesheet">
```

### 关键 UI 组件

- **对比表格（§1）**：3 列 · A 列头浅蓝底 · B 列头浅绿底 · winner 单元格加金色 border-left
- **Dimension bar**（§2）：10 分制水平条 · A 条深蓝 · B 条深绿 · winner 加 🏆 emoji + winner 那一档加金框
- **Signal card**（§3）：5 张卡 · 每张顶部有 winner 大 badge（"🏆 A" 或 "🏆 B"）· 卡片背景根据 winner 微染色
- **Risk card**（§4）：两列并排 · severity 用左边框颜色区分（red / orange / gray）
- **Recommendation banner**（§5 主推荐）：深黑底 + 金色边 + 大字 · 视觉上是整份报告最"重"的 block
- **Gauge**（Verdict 下方）：纯 SVG · 两个圆环并排（A 深蓝 · B 深绿）· 中间标 delta

### 文件特性
- 单文件 + 一个 Google Fonts 外链
- CSS 内联 · 图表纯 SVG · 无 JS 依赖（仅一段内联 exportMarkdown + toggleLang + toggleExportMenu）
- 总体积 <100KB
- **右下角固定 tools 胶囊按钮**：EN / 中文 切换 + Export（下拉：Markdown / PDF）
- `@media print` 时 `.report-tools` 隐藏

### 打印 / PDF 排版规则

**反模式：** 不要给 `section` 加 `page-break-inside: avoid`（会导致长 section 挤到下一页留半页空白）。

**正确做法：** 只对**原子单元**禁止跨页拆分：

```css
@media print {
  @page { margin: 14mm; }
  body { background: white; }
  .page { padding: 0; max-width: none; }
  .report-tools { display: none !important; }
  * { -webkit-print-color-adjust: exact; print-color-adjust: exact; }
  .verdict, .num-card, .comp-row, .dim-row, .signal-card, .risk-card,
  .rec-block, .action-item, .gauge-card, .role-row, .toc, .notice {
    break-inside: avoid; page-break-inside: avoid;
  }
  h1, h2, h3, h4, .section-head { break-after: avoid; page-break-after: avoid; }
  section { margin-bottom: 18px; }
}
```

---

## 内容铁律

1. **数字给区间不给单点** — 4-yr TC 永远给 `$X ~ $Y` · 加权总分 gauge 用具体数字但配 confidence 说明。
2. **每条假设单独可纠错** — Assumptions 区 5-8 条 · 每条独立成行 · 明确"任一不对告诉我重新生成"。
3. **Verdict 不许中性** — 明确推荐 A / B / walk-away · ⭐ 1-5 明确 · 模糊态只在真的势均力敌 (<0.5 分差) 时允许。
4. **"If you are X → A / If Y → B" 分叉必须给** — 至少 2 条 · 判定条件必须具体（不许"如果你比较保守"这种）。
5. **每份 offer 4-6 条 risk 对等** — 不许一边 8 条一边 2 条。
6. **绝不杜撰** — 数字 / 公司数据 / 内部情报没确认的标 `[需用户核对]`。

---

## 生成流程

1. 内存里跑完 5 条流程（Breakdown / Dimension / Signals / Risks / Recommendation）。
2. 用 [../examples/offer-compare-template.html](../examples/offer-compare-template.html) 骨架 · 把内容填进 `{{PLACEHOLDER}}`。
3. 写到 `~/Desktop/Claude skills/offer-compare-<slug>.html`。
4. **自检 4 关键词** — `Dreameryanyan` / `brand-mark` / `yanliudreamer` / `xiaohongshu`，缺一必补。
5. 同步 [../offer-bank/](../offer-bank/) 里的 md 文件 + 更新 `_index.md`。
6. `open <path>` 自动弹到浏览器。

---

## 常见卡点

| 症状 | 处理 |
|---|---|
| 用户只给 1 份 offer | 拒绝生成 · "本 skill 是对比工具，至少要 2 份 offer。1 份 offer 请转 JD Skill 分析是否值得投。" |
| 用户给 3+ 份 offer | 支持 · 但每维度对比表格改为 N 列 · Recommendation 依然只推荐 1 家 |
| RSU vest schedule 完全没说 | 一次追问 · 默认 25/25/25/25 且在 Assumptions 显式写 |
| 币种混杂 | 换到用户所在地本币 · 汇率 + 换算日期写进 Assumptions |
| 用户拒绝提供 priorities | 用 Balanced default 权重 · Assumptions 写 "用户未提供 priorities，按 Balanced 权重给出" · 依然要给明确推荐 |
| 报告 >100KB | 砍 Risk 卡的 mitigation 长度 · 或每份 risk 数量降到 4 条 · 保留所有视觉组件 |
| 导出 PDF 中文变空白 | 检查 Noto Sans SC 的 `<link>` · CSS 里 Noto 排在 PingFang 前 |
| 导出 PDF 整页空白 | 检查 `@media print` 里没有 `section { page-break-inside: avoid; }` |
| **Footer 丢了作者签名（最高频）** | 从下方「📌 强制 Footer 区块」整段抄回 · 自检搜 `Dreameryanyan` |

---

## 📌 强制 Footer 区块（每份报告原样抄，填 `{{}}` 占位符）

> ⛔ 这一整块（CSS + HTML）是**必抄项**。生成报告时把它接在正文 `</div>`（`.page` 收尾）之前的 `<footer>`，并确保 CSS 已在 `<style>` 里。**只替换 `{{...}}`，其余一字不改。**

**配套 CSS（放进 `<style>`）：**

```css
footer { margin-top: 40px; }
.brand-block { display: grid; grid-template-columns: 1fr auto; gap: 36px; align-items: end; padding: 44px 0 28px; border-top: 1px solid var(--line); }
.brand-block .brand-mark { font-family: var(--display); font-weight: 800; font-size: 92px; line-height: 0.92; letter-spacing: -0.045em; color: var(--ink); margin: 0; }
.brand-block .brand-mark .dot-yellow { color: var(--accent); -webkit-text-stroke: 1px var(--ink); }
.brand-block .brand-sub { font-family: var(--serif); font-style: italic; font-size: 15px; color: var(--muted); margin-top: 10px; }
.brand-block .brand-sub strong { font-style: normal; font-family: var(--display); font-weight: 700; color: var(--ink); }
.socials { display: flex; gap: 12px; align-items: center; }
.socials a { display: inline-flex; align-items: center; justify-content: center; width: 46px; height: 46px; border: 1.5px solid var(--ink); border-radius: 50%; background: var(--paper); color: var(--ink); transition: all 0.18s ease; }
.socials a:hover { background: var(--ink); color: var(--paper); transform: translateY(-2px); }
.socials a svg { width: 20px; height: 20px; display: block; }
.socials a.xhs { width: 46px; height: 46px; padding: 0; border-radius: 11px; background: #ff2442; border: 1.5px solid #ff2442; color: white; font-family: "PingFang SC", "Hiragino Sans GB", "Microsoft YaHei", sans-serif; font-weight: 900; font-size: 11px; font-style: italic; letter-spacing: -0.02em; line-height: 1; }
.socials a.xhs span { display: inline-block; transform: skewX(-6deg); white-space: nowrap; }
.socials a.xhs:hover { background: #d11838; border-color: #d11838; transform: translateY(-2px); }
.foot-meta { font-size: 11px; color: var(--muted); line-height: 1.75; padding-top: 16px; }
@media (max-width: 720px) { .brand-block { grid-template-columns: 1fr; gap: 18px; } .brand-block .brand-mark { font-size: 56px; } }
```

**HTML（放进正文末尾）：**

```html
<footer>
  <div class="brand-block">
    <div>
      <h2 class="brand-mark">OFFER COMPARE<span class="dot-yellow">.</span></h2>
      <div class="brand-sub">Created by <strong>Dreameryanyan</strong> · Offer Decision Advisor</div>
    </div>
    <div class="socials">
      <a href="https://www.linkedin.com/in/yanliudesign/" target="_blank" rel="noopener" aria-label="LinkedIn" title="LinkedIn · yanliudesign">
        <svg viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><path d="M20.45 20.45h-3.55v-5.57c0-1.33-.03-3.04-1.85-3.04-1.86 0-2.14 1.45-2.14 2.95v5.66H9.36V9h3.41v1.56h.05c.48-.9 1.64-1.85 3.37-1.85 3.6 0 4.27 2.37 4.27 5.46v6.28zM5.34 7.43a2.06 2.06 0 1 1 0-4.12 2.06 2.06 0 0 1 0 4.12zM7.12 20.45H3.56V9h3.56v11.45zM22.22 0H1.77C.79 0 0 .77 0 1.72v20.56C0 23.23.79 24 1.77 24h20.45c.98 0 1.78-.77 1.78-1.72V1.72C24 .77 23.2 0 22.22 0z"/></svg>
      </a>
      <a href="https://x.com/yanliudreamer" target="_blank" rel="noopener" aria-label="X (Twitter)" title="X · @yanliudreamer">
        <svg viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><path d="M18.244 2.25h3.308l-7.227 8.26 8.502 11.24H16.17l-5.214-6.817L4.99 21.75H1.68l7.73-8.835L1.254 2.25H8.08l4.713 6.231zm-1.161 17.52h1.833L7.084 4.126H5.117z"/></svg>
      </a>
      <a class="xhs" href="https://www.xiaohongshu.com/user/profile/5b2afdf311be104ac3c22931" target="_blank" rel="noopener" aria-label="Xiaohongshu" title="小红书 · Dreameryanyan">
        <span>小红书</span>
      </a>
    </div>
  </div>
  <div class="foot-meta">
    Generated {{YYYY-MM-DD}} · {{A_COMPANY}} × {{A_ROLE}} vs {{B_COMPANY}} × {{B_ROLE}} · Candidate: {{CANDIDATE}}<br>
    数据来源：用户提供的 offer 明细 + 用户 priorities + 公开公司情报。4-yr TC 均按 low/high 区间计算，非单点。Recommendation 按用户 priorities 加权 · 若未提供则用 Balanced default。<strong>无杜撰事实</strong>。<br>
    上游：JD Skill / Resume Skill / BQ Skill · 决策后转 BQ Skill 挖 onboarding 90-day 故事 + 谈判 talking points。
  </div>
</footer>
```
