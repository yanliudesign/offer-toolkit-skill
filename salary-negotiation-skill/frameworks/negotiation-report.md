# Negotiation Playbook — HTML Report 规格

**目标**：把 6 条流程（Diagnosis + Leverage Map + Strategy + Scripts + Counter Simulation + Final Recommendation）融合成**一份可分享的单文件 HTML Playbook**。是 Step 3 的默认产出。

参考实现：[`../examples/negotiation-report-template.html`](../examples/negotiation-report-template.html) + 同一系列的 [`../../job-description-skill/examples/offer-strategy-template.html`](../../job-description-skill/examples/offer-strategy-template.html)（复用视觉系统）。

---

## 双语输出 · Bilingual output（必须）

模板右下角有 中文 / EN 切换按钮，CSS 根据 `<html lang>` 属性切显 `[data-lang="en"]` / `[data-lang="zh"]`。任何**用户可见文案**都必须双语：

```html
<span data-lang="en">English version</span><span data-lang="zh">中文版本</span>
```

**适用范围**：Verdict / SIGN / WALK / FREEZE stop-lines / 招聘官原话（EN 主，ZH 对照）/ 你的应答（EN 主，ZH 对照）/ 邮件/电话脚本（EN 主，ZH 对照）/ 推理和 justification 说明。

**不用双语**：数字 / 公司名 / 岗位名 / placeholder / 静态 HTML shell 标签。

**英文版在前，中文版在后**。

---

## 何时生成

- Step 3 收齐 Offer 数据 + Context 后**默认生成**。
- 用户单独要 → 前提是 Offer Diagnosis + Leverage Map + Final Recommendation 至少都跑过，否则拒绝硬出。
- 用户回来更新新一轮 recruiter 回答 → **同文件名覆盖**（不建新版）。旧数据存 `deal-bank/<slug>.md` 的 Rounds 区。

---

## 文件位置 + 命名

| 优先级 | 路径 |
|---|---|
| 1（默认） | `~/Desktop/Claude skills/salary-negotiation-<company-slug>-<role-slug>-<YYYYMM>.html` |
| 2（兜底） | `deal-bank/<同名>.html` |

**Slug 规则**：`<company>-<role>-<level>-<YYYYMM>`，如 `meta-product-designer-e5-202607.html`。

---

## Report 骨架（必须按此顺序）

### 报告头（章节前）

1. **Header** — 公司 × 岗位 · Level · 地点 · 收到 offer 日期 / deadline · 一句 role hook
2. **Meta strip** — Candidate 画像 / 当前状态 / 手中 competing offers 数
3. **Inside (TOC)** — 8 条：`#assumptions` `#verdict` `#diag` `#leverage` `#strategy` `#scripts` `#counter` `#final`
4. **⚠️ Assumptions（最关键 · 放显眼位置）** — 列出报告依赖的假设：
   - 当前 offer 数字 (base / RSU / sign-on / bonus / 曲线 / clawback / start date)
   - Context (competing offers / deadline / seniority level 认知 / risk tolerance / top-2 priorities)
   - 市场对标数据来源（Levels.fyi P50/P75 或 [需查]）
   - 每条独立成行，明确写 **"任一不对告诉我重新生成"**
5. **Verdict（一句话结论）** — Modality [A/B/C/D] + 一句 Overall Leverage verdict + 3 行展开
6. **If you only read three things** — 3 个黑体加粗 takeaway
7. **关键指标（2 个 gauge / big-number card）** —
   - **Overall Leverage Score** (0-100, HIGH 80+, MED 50-79, LOW <50)
   - **Total Ask Uplift** (current TC → target TC, %) with 视觉条

### 正文 6 节

**§1 · Offer Diagnosis** — `#diag`
- 4 组件诊断卡（Base / RSU / Sign-on / Bonus），每卡 5 行（Offer / Market P50 & P75 / Position / Leverage tier / 一句诊断）
- TC 计算表格（Year 1 vs 4-yr avg）
- RSU 曲线可视化（4 个 bar 展示 vest schedule + reference price）
- Overall Leverage verdict（HIGH / MED / LOW）

**§2 · Leverage Map** — `#leverage`
- **左列 · YOUR POWER** — 8 项 checklist，勾中的每条 1 行说明
- **右列 · RECRUITER'S POWER** — 8 项 checklist
- **底部 · YOUR BLIND SPOTS** — 2-3 张 mitigation 卡片（每卡：weakness + how to mitigate）
- **Power Balance Verdict** — 一句 net 判定

**§3 · Strategy** — `#strategy`
- **Modality Card**（A/B/C/D 中的一个）— 大字标 modality + 一句为什么选它
- **Strategy Table** — 6 列表：Priority / 组件 / 当前 → Ask range / Justification / 触点 / Stop at
- **Timing 建议** — 电话/邮件顺序 + 间隔 + do's/don'ts

**§4 · Scripts** — `#scripts`
- **📞 Phone Script Card** — Beat 1-4 全文（EN + ZH 对照，代码块样式便于复制）+ 底部一句 "STOP TALKING here" warning
- **📧 Email Script Card** — Subject + Body 全文 + tone rules 附注
- 底部：**Copy Both Scripts** button（内联 JS，一键 copy 两个脚本到剪贴板）

**§5 · Counter Simulation** — `#counter`
- **3 张 Pushback Card**（Pushback #1 · "Best offer" / #2 · "Budget fixed" / #3 · "Reconsider pool"），每张：
  - Recruiter Round 1 原话（quote 样式）
  - Your Round 1 应对（按 leverage 分 A/B/C 三种，标你的是哪种）
  - Recruiter Round 2 常见回应
  - Your Round 2 应对
  - ⛔ **Stop-signal** — 什么话意味着"真没空间了 · 停"
- 底部：**Bluff vs Real Detection Table**（招聘官 12 种语言信号 → 大概率是 bluff 还是真）

**§6 · Final Recommendation** — `#final`
- **WHAT TO ASK** — 3-5 行✅ bullet（当前 → target · priority）
- **WHAT NOT TO PUSH** — 3-5 行❌ bullet（组件 · 一句为什么）
- **THREE STOP-LINES**（3 卡片，颜色区分）：
  - **SIGN LINE**（绿）— 达到 X 立刻签 + 一句发送话术
  - **WALK LINE**（红）— 拒到 Y 就走 + 一句 walk 话术
  - **FREEZE LINE**（黄）— 触发 Z 就 24 小时暂停 + freeze 脚本
- **Emergency Protocol** — 一段速查（4 种紧急情况 → 应对）
- **Final Verdict**（大字，一段）— Modality-specific 一句话

### 报告尾

- ⛔ **Footer（强制项 · 必抄）** — 见文末「📌 强制 Footer 区块」
- Meta 行：Generated date · Company × Role · Deadline · 来源标注 · "no fabricated comp data" 声明

---

## 内容铁律

1. **数字给区间，不给单点** — Ask / target / market data 全部 range。
2. **每条假设独立可纠错** — Assumptions 区 6-10 条，每条独立。
3. **Counter Simulation 每种 pushback 必须走 2 轮** — 不能只给 Round 1 应对。
4. **每一句脚本必须一字不改可念** — 禁止 "you might say something like…"。
5. **必须有 3 条 stop-lines**（SIGN / WALK / FREEZE），数字明确。
6. **Verdict 不许中性** — Modality 必须明确到 A/B/C/D，"depends" 是废话。
7. **绝不虚构 comp data** — Levels.fyi 查不到就标 `[需查]`，别编。
8. **preserve recruiter relationship** — 所有脚本禁止对抗性、羞辱性、最后通牒式语言。

---

## 与内部步骤的关系

| 章节 | 数据来源 |
|---|---|
| §1 Diagnosis | [`../prompts/offer-diagnosis.md`](../prompts/offer-diagnosis.md) 完整产出 |
| §2 Leverage Map | [`../prompts/leverage-map.md`](../prompts/leverage-map.md) 完整产出 |
| §3 Strategy | [`../prompts/negotiation-strategy.md`](../prompts/negotiation-strategy.md) Modality + Strategy Table |
| §4 Scripts | [`../prompts/script-generator.md`](../prompts/script-generator.md) 3 份脚本（去掉 recruiter 回答 A/B/C，那部分放 §5） |
| §5 Counter | [`../prompts/counter-simulation.md`](../prompts/counter-simulation.md) 3 pushback × 2 rounds |
| §6 Final | [`../prompts/final-recommendation.md`](../prompts/final-recommendation.md) 完整 |

---

## 生成流程

1. 确认 6 条 prompt 都在内存里跑过。少任何一条 → 告诉用户 "缺 X，先补再出报告"。
2. 组装报告头 + 6 节正文。
3. 用 [`../examples/negotiation-report-template.html`](../examples/negotiation-report-template.html) 骨架填数据。
4. 写到 `~/Desktop/Claude skills/salary-negotiation-<slug>.html`。
5. **自检**：搜 `Dreameryanyan` / `brand-mark` / `yanliudreamer` / `xiaohongshu` 四个词，全部命中才算合格。
6. **同步 `deal-bank/`**：写 `<slug>.md` + 更新 `_index.md` + 报告链接。
7. `open <path>` 自动在浏览器打开。

---

## 视觉规范（复用 job-description-skill 的视觉系统 + 一点差异化）

### 色板（复用）
- 底色：`#fafaf7` / `#faf8f3`
- 卡片：`#fff8e6` / `#fef0d4`
- 文字主：`#1f1f1d`
- 文字次：`#6b6b66`
- **SIGN 绿**：`#18a957` / `#0d8a45`
- **WALK 红**：`#c2410c` / `#dc2626`（比 JD skill 更 emphatic —— 谈判是高 stakes）
- **FREEZE 黄**：`#d97706` / `#f59e0b`
- **HIGH leverage**：`#18a957`
- **MEDIUM leverage**：`#d97706`
- **LOW leverage**：`#6b6b66`

### 字体系统（复用）
```css
--display: "SF Pro Display", -apple-system, "Helvetica Neue", "Noto Sans SC", sans-serif;
--serif: "Times New Roman", "Noto Serif SC", "Songti SC", Georgia, serif;
--body: -apple-system, BlinkMacSystemFont, "SF Pro Text", "Noto Sans SC", sans-serif;
--mono: "SF Mono", "JetBrains Mono", Menlo, "Noto Sans SC", monospace;
```

**⚠️ 必须** `<head>` 里加 Google Fonts Noto SC 链接，理由同 JD skill（CJK PDF embed）。

### 关键 UI 组件
- **Leverage tier badge**：HIGH（绿背景 + 白字）/ MEDIUM（橙）/ LOW（灰）
- **RSU vest schedule bars**：4 条 vertical bar 显示 Y1/Y2/Y3/Y4 vest %
- **Script block**：`<pre>` 样式 + 顶部 "Copy" 按钮 + Beat 编号
- **Recruiter quote**：italic serif + 左侧 orange bar + "🎙️ Recruiter" 标签
- **Your response block**：sans-serif + 左侧 green bar + "🗣️ You" 标签
- **Stop-line card**：3 张并排，绿 / 红 / 黄 3 色背景
- **Modality badge**：大字（A/B/C/D）+ 一句 tagline

### 文件特性
- 单文件 + Google Fonts 一个外链
- 无 JS 依赖（仅：export markdown / copy scripts 两段内联 JS）
- 右下角 2 个胶囊按钮：**Copy All Scripts** + **Export PDF**
- 打印规则同 JD skill（小原子单元 `break-inside: avoid`，长 section 允许跨页）

---

## 📌 强制 Footer 区块（每份报告原样抄，只填 `{{}}` 占位符）

**配套 CSS（放 `<style>`）：**

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

**HTML（放正文末尾）：**

```html
<footer>
  <div class="brand-block">
    <div>
      <h2 class="brand-mark">SALARY SKILL<span class="dot-yellow">.</span></h2>
      <div class="brand-sub">Created by <strong>Dreameryanyan</strong> · Salary Negotiation Coach</div>
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
    Generated {{YYYY-MM-DD}} · {{COMPANY}} × {{ROLE}} ({{LEVEL}}) · Deadline: {{DEADLINE}} · Candidate: {{CANDIDATE}}<br>
    数据来源：Recruiter 提供的 offer letter + 用户提供的 context + Levels.fyi / Blind 公开薪资情报。每项数字都给区间；单点数字仅在 stop-lines 中出现。<strong>无杜撰 comp 数据 · 无 fabricated recruiter 原话</strong>。<br>
    上游：Offer Strategy Report → Job Description Skill · 下游：新一轮谈判进展 → 更新本 report（同文件名覆盖）。
  </div>
</footer>
```

---

## 常见卡点

| 症状 | 处理 |
|---|---|
| Recruiter 已经回了第 2 轮 offer，要不要重出 report | 是。同文件名覆盖。旧数据进 `deal-bank/<slug>.md` 的 Rounds 区 |
| 用户还没做过 offer diagnosis 就要报告 | 拒绝 + 一句 "先跑 diagnosis 才能出报告" |
| Modality 判定和用户直觉不合 | 报告顶部 Assumptions 区强化 leverage 判定依据，让用户看到"为什么我说是 Modality X"。用户不 accept 就调 Step 2 context |
| 用户没 competing offer 但坚持要 Modality A 激进打法 | 报告里明确警告风险 + 给一个"如果失败你能承受吗"的自检问题。不硬拒，但把风险显式化 |
| 中国公司 offer | 字体换 Noto SC；薪资用 RMB；Level 对标 P7/P8；招聘官话术换中文（部分 recruiter playbook 需 localize） |
| RSU 是 private company (OpenAI / Anthropic) | Diagnosis 加 illiquidity discount 一节（20-40%）；strategy 里降低 RSU push 优先级，pivot 到 base + sign-on |
| 用户情绪化 / 半夜发狂说"我要 walk" | 报告里的 FREEZE 脚本必须显眼；补一句"睡一觉再打" |
| Footer 丢了 / 简化了（最高频 bug） | 从本文件 「📌 强制 Footer 区块」 整段抄回；自检必须搜 Dreameryanyan / brand-mark / yanliudreamer / xiaohongshu 全部命中 |
