# Job Description Skill

> 🌐 **中文** · [English](./README.md)

> **JD Decoder & Offer Strategy OS** — 把任何 Job Description 翻译成"该不该投 / 怎么投 / 怎么赢"的完整作战图。求职链路的入口。

一份 JD ≠ 一份招聘文案。它是招聘经理的真实期望、团队当前的痛点、公司文化的暗号——只是被 HR 模板包了一层。这个 Skill 把它解码回来。

---

## 整个 skill 只有 3 步

用任何模糊的话调用（“帮我看看这个职位” / "help me with this job"）都会走同一条路径：

1. **贴 JD** — 链接或全文。
2. **给简历**，三选一：
   - 🅰️ 上传 / 粘贴简历全文（推荐，结果最准）
   - 🅱️ 粘贴 LinkedIn 全文
   - 🅲️ 还没简历 → 简略介绍一下自己。这条路线下的结论会被标 “未经简历事实校验”，并提示你去 **[Resume Skill](https://github.com/yanliudesign/resume-builder-skill)** 先建一份正式简历。
3. **HTML 报告自动弹出** — 单文件 Offer Strategy Report 生成到 `~/Desktop/Claude skills/offer-strategy-<slug>.html`，自动在浏览器打开。里面包含：TL;DR 结论、两个仪表、下表里的 10 节内容，以及页内的 Export PDF / Export Markdown 按钮。

就这些。没有多步引导、也没有分开的 "Flow 1 / Flow 2" 交付物要你逐个看——5 条内部流程（Decode / Match / Tailor / Predict / Should I Apply）都静默跑完后拼装进同一份 HTML 报告。

如果你明确只要其中某一条流程（“只解码这份 JD” / “只算匹配度”），skill 会跳过报告生成，只给那条流程的原始输出。

---

## 📊 Offer Strategy Report · 10 节报告框架

Wizard 跑完的默认交付物是一份单文件 HTML 报告，存到 `~/Desktop/Claude skills/offer-strategy-<slug>.html`。这份报告是**区别市面其他 JD 工具的核心交付物**。固定 10 节主骸 + TL;DR 预头 + 关键指标仪表：

![Offer Strategy Report 预览](docs/report-preview.png)

*一份真实报告的顶部 — Verdict + Assumptions + TL;DR + 两个仪表，右下角是页内的导出 PDF / Markdown 按钮。*

| # | 章节 | 回答什么 |
|---|------|----------|
| — | **TL;DR · 一分钟摘要** | 这到底能不能投？⭐ 1–5 分。 |
| — | **关键指标** | Match Score 仪表 + Interview Probability 仪表。 |
| **1** | **公司背景** | 这家公司谁在掌舷 / 文化信号 / 近 12–24 个月出了什么。 |
| **2** | **本职位产品分析** | 这个 role 管哪个 surface + 4 个核心设计难题 + JD 背后的**真实** scope。 |
| **3** | **JD 深度解读** | 为什么这份 JD 这样写（Flow 1 精华 + Hidden Signal 词典命中）。 |
| **4** | **JD ↔ 简历 逐条匹配** | Must Have 卡片 + 完整 Match Matrix（3 列：JD 要求 / 简历证据 / 评分+Gap）+ Nice + 10 维 Hidden Signal 雷达。 |
| **5** | **Gap 要提升的** | 2–4 张 Gap 卡，标明严重度（高/中）+ 4 周应对动作。 |
| **6** | **为什么投 / 为什么不投** | 各 3 条。每条“不投”都携 HM probe 应对。 |
| **7** | **薪资 reality check** | JD 带宽 + 市场数据 + 谈判 talking points。 |
| **8** | **Next step** | 职业弧套不套 + 内推 playbook（找谁·DM 模板）+ Portfolio audit（4 周必做的具体动作）。 |
| **9** | **Top 10 面试题预测** | Flow 4 preview。完整 Top 20 + behavior 故事 → 交接给 BQ Skill。 |
| **10** | **6 周行动计划** | 按周拆解：投递前 / 投递后 / 面试前。 |

报告内置 **一键 Export PDF**（修复了中文字体在 PDF 里不嵌入的问题，Noto SC 工作中）和 **一键 Export Markdown**（单文件 .md 下载）。规格见 [`frameworks/offer-strategy-report.md`](frameworks/offer-strategy-report.md)，骨架见 [`examples/offer-strategy-template.html`](examples/offer-strategy-template.html)。

---

## 三铁律

1. **先解码，再行动** — 没跑过 Flow 1 不允许直接跳 Flow 2/3。匹配错对象 = 匹配错了。
2. **不杜撰** — 候选人没说过的经历 / 技能 / 数字一律不发明。出不了真实证据就标 ❌。
3. **一次只走一条流程** — 不混跑。Flow 1 出来如果还有 ambiguity，先澄清再前进。

---

## 文件结构

```
job-description-skill/
├── SKILL.md                      # 入口 · 路由 · 三铁律
├── prompts/                      # 5 条流程的执行 prompt
│   ├── jd-decoder.md
│   ├── match-score.md
│   ├── resume-tailor.md
│   ├── interview-predictor.md
│   └── should-i-apply.md
├── frameworks/                   # 复用的框架 / 评分尺
│   ├── decode-patterns.md        # JD 关键词 → 真实意图字典
│   ├── match-rubric.md           # 评分尺 (Must / Nice / Hidden)
│   ├── resume-tailoring.md       # 三版本简历策略
│   ├── go-no-go.md               # ⭐ 推荐指数 + 拿面概率公式
│   └── offer-strategy-report.md  # 最终 HTML 报告 — 10 节骨架 + 视觉规范 + 生成说明
├── examples/                     # 参考骨架（不含个人数据）
│   └── offer-strategy-template.html
└── jd-bank/                      # 已分析过的 JD 反查库（本地不进 git）
    ├── _index.md                 # 索引
    └── _jd-template.md           # 新 JD 起手模板
```

---

## 设计原则

- **JD 是一面镜子，不是一份题目** — 它照出公司、HM、产品三层信息。我们要做的是看穿包装层。
- **决策优先于优化** — 大多数候选人在错的 role 上反复优化简历。这个 Skill 先帮你决定该不该投。
- **可复现的逻辑，不是玄学** — 每个评分 / 概率都有显式公式，不喜欢可以反驳前提。
- **配合 [BQ Skill](https://github.com/yanliudesign/Behavior-question-skill)（故事挖掘）+ [Resume Skill](https://github.com/yanliudesign/resume-builder-skill)（简历美化）形成完整求职链路。**

---

## License

MIT — fork it, remix it, ship your own version.

Created by [Dreameryanyan](https://www.linkedin.com/in/yanliudesign/) ·
[LinkedIn](https://www.linkedin.com/in/yanliudesign/) ·
[X](https://x.com/yanliudreamer) ·
[小红书](https://www.xiaohongshu.com/user/profile/5b2afdf311be104ac3c22931)
