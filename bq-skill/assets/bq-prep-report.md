# BQ Prep Report — HTML 视觉规范(Editorial)

JD 驱动流程(`prompts/jd-driven-prep.md` Step 7)的 HTML 报告生成规范。**与 job-description-skill 的 Offer Strategy Report 共用同一套 editorial 视觉系统**,保证 Career Copilot 全链路报告风格一致。

## 文件

- 路径:`~/Desktop/Claude skills/bq-prep-<company>-<role>-<YYYYMM>.html`
- 单文件 + 一个 Google Fonts 链接(CJK 在 PDF 里可嵌入)。可离线打开 + Cmd+P 存 PDF。

## 视觉系统 · Editorial(奶油纸感 + 衬线 + ink/yellow)

```
纸底     --paper:#fafaf7  --paper-2:#f3f3ee  --paper-3:#ebebe4
墨色     --ink:#0a0a0a    --ink-2:#1f1f1d    --muted:#6b6b66  --line:#d9d9d2
强调     --accent:#facc15 (yellow)  --go:#18a957  --warn:#d97706  --stop:#c2410c
四类选题边色:
  Behavior 通用     --behavior:#7c3aed (紫)
  公司价值观定制    --values:#c2410c   (rust)
  岗位/专业向       --craft:#2563eb    (蓝)
  Level/阶段定制    --level:#0a0a0a    (ink)
必练星标:accent yellow 胶囊　|　缺口:--stop rust
字体:
  --serif   "Times New Roman","Noto Serif SC"  → 斜体 kicker / 题目中文注释
  --display "SF Pro Display","Noto Sans SC"     → 大标题 / 题目英文 / 序号
  --body    -apple-system,"Noto Sans SC"        → 正文
  --mono    "SF Mono"                            → 小标签(考什么/为什么/配故事)
CJK 字体务必排在系统字体前,确保 PDF 导出中文可嵌入。
```

参考骨架:`../../job-description-skill/examples/offer-strategy-template.html`(同源风格)。

## 关键排版手法(editorial 的灵魂)

- **Masthead**:meta-strip(mono 小字)→ 巨号 display 标题 + serif 斜体副标 → 2px ink header-rule → 四格 role-row(候选人/岗位/匹配度/风格)。
- **Match verdict**:ink 黑底块 + accent 斜体 kicker,匹配画像 + 风险各一段。
- **Section head**:serif 斜体罗马数字(i. ii. iii.)+ display 大标题 + mono pill,下方 1px ink 线。
- **Top 5 must 卡**:左侧 accent 竖条 + **纯黑(--ink)大号序号**(display 800,不要黄填充/不要 text-stroke 描边)+ display 题目;STAR 模板用 mono 标签 + 短横线;A/R 填空用 warn 琥珀虚线框;范例用 serif 斜体 kicker "Model answer"。
- **Top 20**:`.qcard` 左边按四类着色,display 序号 + display 题目 + serif 斜体中文 + mono 元信息行 + 范例段。
- **层级纪律**:题目(display 18–23px,主角)> 范例(body 14px)> 元信息(mono 10–12px,配角)。三档拉开,别让字号挤在一起。

## 报告结构(章节顺序)

1. Masthead(meta-strip + 标题 + role-row)
2. Match verdict(ink 块,匹配画像 + 风险)+ notice(英文范例免责说明)
3. **§i Top 5 必练** — STAR 模板(S/T 填实,A/R 琥珀填空)+ Model answer 范例
4. **§ii Top 20 选题** — 四类分组,每题 q-card + 范例
5. **§iii 缺口清单** — stop 色 gap-card
6. Footer — 编号 next-step + mono colophon

## 内容纪律

- STAR 的 S/T 用简历事实填实;**A/R 用占位符**,绝不杜撰动作和数字。
- 英文范例的动作细节是草稿 → 顶部 notice 注明「用前校对真实情况、核对数字归因」。
- 每题「为什么这家会问」必须指向 JD 的具体 Must Have / Hidden Signal。
- 缺口题如实标 ⚠️,范例只作结构示意,不塞进 Top 5 假装能答。
