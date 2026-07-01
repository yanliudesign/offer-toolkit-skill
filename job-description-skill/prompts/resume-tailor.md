# Resume Tailor — 流程 3

**目标：** 针对单份 JD，把用户简历改三个版本：ATS 版 / Recruiter 版 / Hiring Manager 版。每条改写给 diff + 对齐说明。

**铁律（最重要的一条）**
- **绝不杜撰**。所有改写只能基于用户简历里**已有的事实**——重新组织、突出、翻译话术。
  - ❌ 不能编造新成就 / 新数字 / 新职责
  - ❌ 不能把"参与"改成"主导"
  - ✅ 可以把"做了 X"翻译成 JD 的措辞习惯
  - ✅ 可以把已有数字换个角度呈现
- 数字、影响范围、Title 一律向用户求证。**用户没说的不写**。

**其他原则**
- 必须先有 Decode 产出（至少 Must Have + Hidden Signal），再 tailor。
- 一次只 tailor 这一份 JD。**这份 tailor 不是简历整体优化**——告诉用户"整体打磨建议去 Resume Skill"。

---

## Step 1 · 收齐输入

1. **JD 的 Decode 产出**（从 jd-bank 调取或现场跑）。
2. **用户简历全文**（必须是全文，不是摘要）。
3. **用户想强调的 1-2 个亮点**（可选）。如果用户没说，按 Match Score 的"强项"自动挑。
4. **目标 Level**（影响措辞激进度）。

---

## Step 2 · 先定改写策略

在动笔之前先告诉用户：

1. 这份 JD 的 **3 个关键词**（从 Must Have 抽，要在简历里反复出现的）。
2. 这份 JD 的 **1 个核心叙事**（用户简历应该围绕的主线，如"AI 产品端到端 ownership"）。
3. **哪些经历需要重写 / 重排序 / 弱化**（让用户先认这个大方向再开动，避免改完了用户说"我不想突出这块"）。

---

## Step 3 · 输出三个版本

**三个版本共享同一份简历事实，只是组织方式和措辞不同。** 改写规则详见 [../frameworks/resume-tailoring.md](../frameworks/resume-tailoring.md)。

### 版本 A · ATS 版（机器友好）

目标：通过简历筛选系统。

要求：
- JD 关键词（动词 + 名词）**原样**出现，密度合理（不堆叠到机器识别为 spam）。
- 标准 section 标题（Experience / Education / Skills）。
- 避免图表 / 双栏 / 复杂格式。
- Skills section 把 JD 里出现的硬技能词汇都列上（用户真有的）。
- 量化数字保留，但措辞用 JD 原词。

### 版本 B · Recruiter 版（30 秒扫读）

目标：让 Recruiter 在 30 秒内看到"这人匹配"。

要求：
- 顶部加 **Headline / Summary** —— 一句话把用户定位成 JD 在找的那种人（事实基础上）。
- 最近 / 最相关的经历置顶 + 加粗最关键的 1-2 条 bullet。
- 每段经历前 1-2 个 bullet 必须**直接对齐 Must Have**。
- 数字 + 影响力前置（金额 / 用户量 / 增长率）。
- 不相关的早期经历压缩到 1 行。

### 版本 C · Hiring Manager 版（体现思考与判断）

目标：让招聘经理看出"这人怎么思考、怎么做决定"。

要求：
- Bullet 句式：**「面对什么 → 做了什么判断 → 推动什么动作 → 取得什么结果」**——而不是只列动作。
- 突出 Hidden Signal 对应的特质（如 JD 强调 ownership，就把"端到端负责"的段落具体化）。
- 加入"决策 / 取舍 / 影响"动词：drove / defined / influenced / aligned / shipped。
- 保留 1-2 个有故事感的细节（招聘经理会在面试里追问这些细节）。
- 不堆 buzzword。

---

## Step 4 · 给 Diff，逐条说"为什么这么改"

**这是 Tailor 的核心体验，不能省。** 每条改动要给：

```
【职位 1 · 改动 #1】

原文：
> Led design for Microsoft Teams

改后（HM 版）：
> Led AI-powered meeting experiences in Microsoft Teams (1M+ enterprise users),
> defining product direction with PM/ENG from 0→1, shipping Teams AI.

对齐了 JD 的：
- Must Have #1（AI 产品经验）— "AI-powered" + "Teams AI"
- Must Have #3（End-to-end design）— "0→1" + "defining...with PM/ENG"
- Hidden Signal（ownership）— "defining product direction"
依据简历事实：用户原简历提到"主导 Teams AI 项目"+"DAU 1M+"
```

**改了几条就给几条 diff，不要只给最终版本。** 用户需要看到"为什么"才能学到下次自己怎么改。

---

## Step 5 · 收尾

1. **三个版本分别用什么场景**告诉用户：
   - ATS 版 → 通过公司官网 / LinkedIn Easy Apply 投递时用
   - Recruiter 版 → 给 recruiter / 内推人 / 猎头时用
   - HM 版 → 面试前发给招聘经理 / Hiring Loop 看的版本
2. **更新 JD 文件**：status 改为 tailored，记录改了哪些段落。
3. **导流**：
   > "Tailor 完成 ✅。建议：
   > - 简历整体的打磨 / 排版 / 一致性 → 去 **Resume Skill**
   > - 准备面试可能问的题 → **流程 4 Interview Predictor**
   > - 还想试着 tailor 另一份 JD → 把那份 JD 发我"

---

## 常见卡点

| 症状 | 处理 |
|---|---|
| 用户简历缺数字 | **不要编**。告诉用户"这块没有数字会弱很多，你能去查一下 / 估一个保守区间吗？" |
| 用户希望"夸张一点" | 提醒："夸张到面试讲不出细节就是反噬。简历每句话都会被 follow up 问。" |
| 用户简历跟 JD 差距太大 | 别硬 tailor，回到流程 5："匹配度可能不足以 tailor 出有效版本，先决定要不要投" |
| JD 是中文岗位 | 三版本逻辑一样，但 ATS 版关键词要用中文招聘平台的标准词（智联 / Boss / LinkedIn 中文） |
| 用户只想要 1 个版本 | 问他用什么场景，按场景给对应版本。但提醒他三个版本各有用，建议都留一份 |
