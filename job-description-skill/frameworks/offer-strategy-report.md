# Offer Strategy Report — HTML 报告规格

把 Flow 1（Decode 精华）+ Flow 2（完整 Match）+ Flow 4（Top 10 题预览）+ Flow 5（完整 Should I Apply）+ 策略层（内推 / portfolio / 时间线）融合成**一份可分享的单文件 HTML 报告**。是 Onboarding Wizard 跑到 Step 7 后**默认产出**的终极交付物。

参考实现：[../examples/offer-strategy-template.html](../examples/offer-strategy-template.html)（CSS / 排版骨架）+ 用户桌面上已生成过的真实样例。

---

## 何时生成

- **Onboarding Wizard 跑完 Step 7（Should I Apply）→ 默认生成。**
- 用户单独要："给我出一份 HTML 报告" → 前提是 **Flow 1 + Flow 2 + Flow 5 至少都跑过**（否则数据不够）。
- 跑完 Flow 3 / Flow 4 之后用户要求更新报告 → 重新生成同文件名（覆盖）。

---

## 文件位置 + 命名

| 优先级 | 路径 |
|---|---|
| 1（默认） | `~/Desktop/Claude skills/offer-strategy-<company-slug>-<role-slug>-<YYYYMM>.html` |
| 2（兜底） | 本 skill 内 `jd-bank/<同名>.html`（如果用户没有 `~/Desktop/Claude skills/` 目录） |

> 历史命名兼容：`should-i-apply-<...>.html` 这种命名是早期版本，新报告统一改用 `offer-strategy-` 前缀。

---

## 报告骨架（必须按此顺序）

报告分两块：**报告头**（Header + Meta strip + TOC + Assumptions + Verdict + If you only read three things + 两个 gauge）和**正文 10 节**。

### 报告头（章节前）

1. **Header** — 公司 × 岗位 · 地点 · 薪资带 · Level · JD 一句话定位
2. **Meta strip** — 候选人画像 / Track Record / Pedigree / 当前 Status
3. **Inside (TOC)** — 12 条目，指向：`#tldr` `#assumptions` `#metrics` `#company` `#product` `#decode` `#match` `#gap` `#yes-no` `#salary` `#nextstep` `#questions` `#timeline`
4. **⚠️ Assumptions（最关键章节，放显眼位置）** — 列出报告所依赖的全部假设（薪资底线 / visa / on-site 接受度 / 心理价位 title / 行业切换接受度 / 当前手里 pipeline 数），每条单独成行，明确写："任一不对，告诉我重新生成"
5. **Verdict（TL;DR · 一分钟摘要）** — 一句话定性 + 3 行展开 + ⭐ 1-5 推荐指数
6. **If you only read three things** — 3 个最重要的 takeaway（黑体加粗，给"不会读完全文"的 reader 用）
7. **关键指标** — Match Score gauge（数字 + Must/Nice/Hidden 加权 + 0–100 视觉条）+ Interview Probability gauge（区间 + 调节因子 + 视觉条）

### 正文 10 节（按编号顺序）

1. **§1 · 公司背景** — `#company`
   公司画像（成立年份、headcount、设计团队规模、估值/营收、CEO/CPO/设计 lead、投资方）+ 文化信号（4 条 craft / pace / review）+ 近 12-24 个月关键产品节点 + 对你而言的特殊信号。**这块是市面工具最缺的"为什么你应该 care 这家公司"。**

2. **§2 · 本职位产品分析** — `#product`
   {{PRODUCT_NAME}} 的设计挑战 + 这个 role 的真实 scope。包含：产品规模（用户/营收/付费层/主要 surfaces）+ 4 个核心设计难题（JD 在找解题人）+ role 真实 scope vs JD 文字 + 成败信号（6 个月/12 个月的 ✅ + 2 个 ⚠️ 失败信号）。**让候选人在面试前就知道"这个团队真正在解什么题"。**

3. **§3 · JD 深度解读** — `#decode`
   Flow 1 精华。每段 JD 原文 → 真实诉求 + Hidden Signal 词典命中（表格：JD 措辞 → 解读 → 是否命中你的画像）。

4. **§4 · JD ↔ 简历 逐条匹配** — `#match` + `#matrix` + `#nicehidden`
   三个子块（同一节，共用 `4.` 编号）：
   - `#match` (4.) — Must Have 命中分析：Flow 2 每条 Must Have 一张卡片（评分 + 简历原文证据 + 风险提示）
   - `#matrix` (4·) — Match Matrix 完整对照表：3 列表格（JD 要求 / 简历证据 / 评分+Gap），覆盖 Must + Nice + Hidden
   - `#nicehidden` (4·) — Nice to Have 隐性命中清单 + 10 维度 Hidden Signal Fit 雷达

   **§4 是「其他工具看不到」的差异化点，必须有完整 Matrix。**

5. **§5 · Gap 要提升的** — `#gap`
   从 Matrix 里红/橙色格收集起来，2-4 张 Gap 卡。每张写：Gap 名称 + 严重度（高/中）+ "为什么 HM 会担心" + "4 周内怎么补"（链到 §8 portfolio audit）。**独立成节，不要塞回 Matrix 内部。**

6. **§6 · 为什么投 / 不投** — `#yes-no`（也叫 `#duo`）
   各 3 条，**"不投"每条必须附 "HM probe 应对"**（市面工具最缺这块）。

7. **§7 · 薪资 reality check** — `#salary`（也叫 `#comp`）
   JD 带宽 + 同岗位市场数据（base / equity / sign-on）+ 谈判 talking points + 当前包对比。

8. **§8 · Next step（叙事 + 内推 + portfolio）** — `#nextstep` 锚点 → 三个子块共用 `8.` 编号：
   - `#narrative` / `#arc` (8.) — 为什么这个 role 是你叙事的下一步：职业弧线 + role 在弧线上的位置
   - `#referral` (8·) — 内推 playbook：找谁（LinkedIn 搜法）/ 怎么开口 / 完整 DM 模板
   - `#audit` / `#portfolio` (8·) — Portfolio audit：4 周内必须做的 3-5 件具体动作（不是泛泛而谈）

   **`<span id="nextstep"></span>` 锚点要放在三块的最前面**，让 TOC 跳转准确。

9. **§9 · Top 10 面试题预测** — `#questions` / `#qs`
   Flow 4 preview，每题标"为什么会问 + 准备方向"。结尾导流："要完整 Top 20 + Behavior 故事，去 BQ Skill"。

10. **§10 · 6 周行动时间线** — `#timeline`
    按周拆解：投递前 / 投递后 / 面试前。每周 2-4 条具体 to-do。

### 报告尾

- ⛔ **Footer（强制项 · 必须用完整签名版，绝不简化）** — `JD SKILL.` brand mark + `Created by Dreameryanyan · Job Description Decoder & Offer Strategy OS` 副标题 + 三个社交圆形按钮（LinkedIn `yanliudesign` / X `yanliudreamer` / 小红书红方块）+ meta 行（生成时间戳 + JD source URL + 评分方法引用 + "no fabricated facts" 声明）+ 同 JD 的 markdown 文件链接。
  - **这是作者署名，不是可选装饰。** 这是市面工具丢得最多、本 skill 最高频的 bug：模型为了省篇幅或「没数据」把整个 footer 删了 / 简化成一行。**无论报告多长、多缺数据，都必须原样包含。**
  - 生成时**直接抄本文件末尾的「📌 强制 Footer 区块」**（HTML + 配套 CSS 都在），把 `{{...}}` 占位符填好即可，不要凭记忆重写。
  - 写完文件后**自检**：必须能搜到 `Dreameryanyan` / `brand-mark` / `yanliudreamer` / `xiaohongshu` 四个关键词，缺一个就是 footer 丢了。

---

## 视觉规范（必须保留，否则报告看起来像玩具）

### 色板
- 底色：`#fafaf7` / `#faf8f3` 系 cream/sand
- 卡片背景：`#fff8e6` / `#fef0d4` 暖米
- 文字主色：`#1f1f1d` / `#2a2308` / `#2a1c04` 深棕近黑
- 文字次色：`#6b6b66` 中灰
- Accent 红：`#d11838` / `#ff2442`（单一红，不要再加红色）
- Accent 绿：`#0d8a45` / `#18a957`（用于"命中" / "值得投"）
- 警示橙：`#d97706` / `#f59e0b`（用于"假设"和"风险"）
- 边框 / 分隔线：`#ebebe4` / `#d9d9d2` / `#c8c8c3`

### 字体系统（CSS variables）
```css
--display: serif（如 Tiempos / Source Serif / Crimson）—— 36–72px，用于章节大标题和 Verdict
--serif:   serif —— body 引用 / case quote
--body:    sans（如 Inter / Söhne / system-ui）—— 15–17px，用于正文
--mono:    monospace（如 JetBrains Mono / Berkeley Mono / SF Mono）—— 数字 / score / code
```

**⚠️ CJK 字体必须用 Noto Sans SC / Noto Serif SC（强制）**

 macOS 系统自带的 `PingFang SC` / `Songti SC` / `Hiragino Sans GB` **license 不允许嵌入 PDF**。Chrome 的「Save as PDF」遇到这些字符时不嵌入字形 → PDF 阅读器显示成空白宽位（中文整段「消失」）。

 解决：在 `<head>` 里加一行 Google Fonts，并把 `Noto * SC` **排在系统 CJK 字体之前**（Latin 字符不受影响，因为 Noto 用 `unicode-range` 圈在 CJK 区间）：

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Noto+Sans+SC:wght@400;500;700;900&family=Noto+Serif+SC:wght@400;700;900&display=swap" rel="stylesheet">
```

```css
--serif:   "Times New Roman", "Noto Serif SC", "Songti SC", Georgia, serif;
--display: "SF Pro Display", -apple-system, "Helvetica Neue", "Noto Sans SC", "PingFang SC", sans-serif;
--body:    -apple-system, BlinkMacSystemFont, "SF Pro Text", "Helvetica Neue", "Noto Sans SC", "PingFang SC", "Microsoft YaHei", sans-serif;
--mono:    "SF Mono", "JetBrains Mono", Menlo, "Noto Sans SC", monospace;
```

这是「单文件零依赖」原则的**唯一例外**——必须保留这一行 `<link>`。

### 关键 UI 组件
- **对角线条纹背景**：用于区分 ✓ 值得投 / ✗ 不值得投 / ⚠️ 假设 三类块（每类一种条纹色 + 角度）
- **Gauge**（评分条）：纯 SVG 或 CSS，不要外部库；显示数字 + 0/55/70/85/100 刻度
- **雷达图**（Hidden Signal Fit）：纯 SVG 10 维度多边形
- **TOC**：左侧 sticky 或顶部 inline，点击平滑滚动到锚点

### 文件特性
- **单文件 + 一个 Google Fonts 外链**（CJK 字体必需，见上）
- CSS 内联、图表用 SVG、无 JS 依赖（仅一段内联的 DOM→Markdown 转换器）
- 可离线打开（首次加载后字体进浏览器缓存）/ 邮件附件直接传
- 总体积控制在 80KB 以内
- **右下角固定有两个胶囊按钮**（`.export-tools` 容器内的 `.export-btn.md` + `.export-btn.pdf`）：
  - **导出 Markdown** — 调用内联的 `exportMarkdown()`：遍历 DOM，跳过按钮和 SVG，把标题/段落/列表/表格/链接/强调还原成 Markdown，浏览器下载 `.md` 文件
  - **导出 PDF** — 调用 `window.print()`，用户选「另存为 PDF」即可
  - 两个按钮在 `@media print` 中 `display: none`，不会出现在导出的 PDF 里

### 打印 / PDF 排版规则（关键）
**反模式**：不要给 `section` 加 `page-break-inside: avoid`。这会让长 section 整块挤到下一页，留出半页空白——这是这类报告的高频问题。

**正确做法**：只对**原子单元**禁止跨页拆分；让长 section 自然跨页流动：
```css
@media print {
  @page { margin: 14mm; }
  body { background: white; }
  .page { padding: 0; max-width: none; }
  .export-tools, .export-btn { display: none !important; }
  * { -webkit-print-color-adjust: exact; print-color-adjust: exact; }

  /* 只对小卡片 / 行 / 列表项保持完整 */
  .verdict, .tldr li, .num-card, .match-row, .nice-row, .probe-row, .signal,
  .decode-card, .comp-card, .play-card, .audit-card, .q-row, .arc-step,
  .toc, .notice, .radar-block, .gauge-card, .role-row {
    break-inside: avoid; page-break-inside: avoid;
  }
  /* 标题不孤立在页底 */
  h1, h2, h3, h4, .section-head { break-after: avoid; page-break-after: avoid; }
  /* 紧凑垂直节奏 */
  section { margin-bottom: 18px; }
}
```

---

## 内容铁律

1. **数字必须给区间，不给单点** —— Match Score / 拿面概率 / 薪资预期都给范围。给"78%"这种单点数字是这类工具最大的可信度杀手。
2. **每条假设单独可纠错** —— Assumptions 区列 5-7 条，每条独立成行，明确写"任一不对，告诉我重新生成"。
3. **"不投"那部分每条必须给 HM probe 应对** —— 不是只说"有风险"，要给"如果 HM 这么问，你这么答"。
4. **简历事实必须引用原文** —— Must Have 命中分析里的证据必须是简历 / LinkedIn 里能查到的原文片段，不能是"我推断你大概有"。
5. **绝不杜撰** —— 数字 / 公司 / 项目 / Title 用户没说过的，标 `[需用户补充]`，不要凭空填。
6. **Verdict 不许中性** —— ⭐ 1-5 必须明确，倾向不投也要敢说，模糊就标"Match 不足或假设缺失，建议先补 ___ 再生成"。

---

## 与五条 Flow 的关系

| 章节 | 数据来源 |
|---|---|
| §1 公司背景 | 公司 research（网站 / Crunchbase / TechCrunch / Glassdoor）+ 选择性拼接，不能编 |
| §2 本职位产品分析 | 产品组件拆解 + JD 中隐含的 design challenge，可推演 |
| §3 JD 深度解读 | Flow 1（精简版，2-3 段就够） |
| §4 JD ↔ 简历 逐条匹配 | Flow 2（完整 6 条左右 Must Have + Matrix 重组 + Nice/Hidden）。三个子块：Must Have 卡·Match Matrix 表·Nice + Hidden Signal 雷达 |
| §5 Gap 要提升的 | 从 Matrix 里红/橙色格提炼，2-4 张 Gap 卡。Gap 不能空，宁可标「本报告未发现关键 gap」也不要删 |
| §6 为什么投 / 不投 | Flow 5 |
| §7 薪资 reality check | Flow 5 + 外部数据（Levels.fyi 等） |
| §8 Next step | Flow 5 + Flow 3 简版（会叙事弧/内推/portfolio audit 三子块） |
| §9 Top 10 面试题 | Flow 4 preview（不替代完整 Top 20） |
| §10 6 周行动计划 | Flow 5 collapse 后的执行版 |

**这份报告不替代单独跑 Flow 3 / Flow 4 完整版。** 报告底部要明确导流：
- 想要三版简历 → 跑 Flow 3 Resume Tailor
- 想要完整 Top 20 + Behavior 故事 → 跑 Flow 4 + 转 BQ Skill

---

## 生成流程

1. 确认 Flow 1 / 2 / 5 数据齐全（至少这三条）。少了就**告诉用户"先跑完 ___ 再生成报告"**，不要硬出。
2. 在内存里组装报告头 + 10 节正文的内容。§1 公司背景 和 §2 本职位产品分析 需要额外跑一轮公司 / 产品 research。
3. 用 [examples/offer-strategy-template.html](../examples/offer-strategy-template.html) 的 CSS / 结构当骨架，把内容填进去。
4. 写到 `~/Desktop/Claude skills/offer-strategy-<slug>.html`。
5. **同步更新 jd-bank 文件**：把 §6 / §8 / §9 三个占位符回填 + 在文件最后加一行 `> 📊 HTML 报告：~/Desktop/Claude skills/offer-strategy-<slug>.html`。
6. **同步更新 [jd-bank/_index.md](../jd-bank/_index.md)**：status 改为 `matched` 或更高，加一列 `report` 链接。

---

## 常见卡点

| 症状 | 处理 |
|---|---|
| 用户没跑完 Flow 5 就要报告 | 拒绝 + 一句话引导："还需要先跑 Should I Apply 才能出报告，要不要现在跑？" |
| 用户简历事实不足，§4 / §5 写不出证据 | **标 `[需用户补充：具体项目 / 数字]`**，不要编。报告顶部 Assumptions 加一条"简历未完全提供，部分章节为占位" |
| 用户希望"只要 Verdict 那一段" | 给一份**极简单页摘要**（5 个 block：Verdict / Match / 概率 / 3 投 3 不投 / 下一步），不要塞 20 章 |
| 公司是中国公司 | 字体换思源宋体 / 思源黑体；薪资章节用 RMB 区间 + level 对标（P7/P8 等）|
| 报告超过 80KB | 砍 §10 时间线和 §8 内推模板的字数，保留所有视觉组件 |
| **导出的 PDF 里中文消失 / 变成空位** | 检查 `<head>` 里 Noto Sans SC 的 `<link>` 是否在；CSS 变量里 `Noto * SC` 是否排在 `PingFang SC` 之前。原因见「字体系统」段。 |
| **导出的 PDF 整页只有一两个 card，下面全是空白** | 检查 `@media print` 里有没有 `section { page-break-inside: avoid; }` —— 有就删掉。只允许小原子单元用 `break-inside: avoid`，长 section 必须能自然跨页。详见「打印 / PDF 排版规则」。 |
| **footer 没有作者名字 / 社交按钮（最高频）** | 生成时漏抄了 footer。从下方「📌 强制 Footer 区块」整段抄回去，并跑自检搜 `Dreameryanyan`。原因：footer 是软提醒时最容易被模型省略。 |

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
      <h2 class="brand-mark">JD SKILL<span class="dot-yellow">.</span></h2>
      <div class="brand-sub">Created by <strong>Dreameryanyan</strong> · Job Description Decoder &amp; Offer Strategy OS</div>
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
    Generated {{YYYY-MM-DD}} · {{COMPANY}} × {{ROLE}} · Candidate: {{CANDIDATE}} · Source: <a href="{{JD_SOURCE_URL}}" target="_blank">{{JD_SOURCE_DISPLAY}}</a><br>
    数据来源：JD 原文 + 用户简历 + 公开公司情报。薪资 / 假设见顶部「假设说明」。Match 按 0.6/0.2/0.2 权重，拿面概率按 go-no-go 估算法，均为区间非单点。<strong>无杜撰事实</strong>。<br>
    下游：整体简历打磨 → Resume Skill · 完整 Top 20 + Behavior 故事 → BQ Skill。
  </div>
</footer>
```
