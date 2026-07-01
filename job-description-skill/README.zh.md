# Job Description Skill

> 📦 属于 **[offer-toolkit-skill](https://github.com/yanliudesign/offer-toolkit-skill)** 求职工具包 — 装工具包等于一次性拿到 JD · Resume · BQ 三条子 skill。

> 🌐 **中文** · [English](./README.md)

一个专门读 JD 的 Claude skill。贴一份 JD 和你的简历，它给你一份 HTML 报告，告诉你：这岗位到底该不该投、你和它多匹配、差在哪里、面试大概会问什么、薪资合不合理、接下来 6 周该做什么。一份 JD 不只是招聘文案——它一般是招聘经理的真实期望包在 HR 模板里，这个 skill 把它拆开。

---

## 整个 skill 只有 3 步

用任何模糊的话调用（“帮我看看这个职位” / "help me with this job"）都会走同一条路径：

1. **贴 JD** — 链接或全文。
2. **给简历**，三选一：
   - 🅰️ 上传 / 粘贴简历全文（推荐，结果最准）
   - 🅱️ 粘贴 LinkedIn 全文
   - 🅲️ 还没简历 → 简略介绍一下自己。这条路线下的结论会被标 “未经简历事实校验”，并提示你去 **[Resume Skill](https://github.com/yanliudesign/resume-builder-skill)** 先建一份正式简历。
3. **HTML 报告自动弹出** — 单文件 Offer Strategy Report 生成到 `~/Desktop/Claude skills/offer-strategy-<slug>.html`，自动在浏览器打开。里面包含：TL;DR 结论、两个仪表、下表里的 10 节内容，以及页内的 Export PDF / Export Markdown 按钮。

就这些。没有多步引导、也没有分开的 "解码流程 / 匹配流程" 交付物要你逐个看——5 条内部流程（Decode / Match / Tailor / Predict / Should I Apply）都静默跑完后拼装进同一份 HTML 报告。

如果你明确只要其中某一条流程（“只解码这份 JD” / “只算匹配度”），skill 会跳过报告生成，只给那条流程的原始输出。

---

## Offer Strategy Report · 10 节报告框架

Wizard 跑完的默认交付物是一份单文件 HTML 报告，存到 `~/Desktop/Claude skills/offer-strategy-<slug>.html`。固定 10 节骨架 + TL;DR 预头 + 关键指标仪表：

![Offer Strategy Report 预览](docs/report-preview.png)

*一份真实报告的顶部 — Verdict + Assumptions + TL;DR + 两个仪表，右下角是页内的导出 PDF / Markdown 按钮。*

| # | 章节 | 回答什么 |
|---|------|----------|
| — | **TL;DR · 一分钟摘要** | 这到底能不能投？⭐ 1–5 分。 |
| — | **关键指标** | Match Score 仪表 + Interview Probability 仪表。 |
| **1** | **公司背景** | 这家公司谁在掌舷 / 文化信号 / 近 12–24 个月出了什么。 |
| **2** | **本职位产品分析** | 这个 role 管哪个 surface + 4 个核心设计难题 + JD 背后的**真实** scope。 |
| **3** | **JD 深度解读** | 为什么这份 JD 这样写（解码流程精华 + Hidden Signal 词典命中）。 |
| **4** | **JD ↔ 简历 逐条匹配** | Must Have 卡片 + 完整 Match Matrix（3 列：JD 要求 / 简历证据 / 评分+Gap）+ Nice + 10 维 Hidden Signal 雷达。 |
| **5** | **Gap 要提升的** | 2–4 张 Gap 卡，标明严重度（高/中）+ 4 周应对动作。 |
| **6** | **为什么投 / 为什么不投** | 各 3 条。每条“不投”都携 HM probe 应对。 |
| **7** | **薪资 reality check** | JD 带宽 + 市场数据 + 谈判 talking points。 |
| **8** | **Next step** | 职业弧套不套 + 内推 playbook（找谁·DM 模板）+ Portfolio audit（4 周必做的具体动作）。 |
| **9** | **Top 10 面试题预测** | 面试预测预览。完整 Top 20 + behavior 故事 → 交接给 BQ Skill。 |
| **10** | **6 周行动计划** | 按周拆解：投递前 / 投递后 / 面试前。 |

报告内置 **一键 Export PDF**（修复了中文字体在 PDF 里不嵌入的问题，Noto SC 工作中）和 **一键 Export Markdown**（单文件 .md 下载）。规格见 [`frameworks/offer-strategy-report.md`](frameworks/offer-strategy-report.md)，骨架见 [`examples/offer-strategy-template.html`](examples/offer-strategy-template.html)。

---

## 三条规则

1. **先解码，再行动** — 没解码 JD 就直接算匹配 / 做 tailor 是不行的。对错了目标，匹配就是错的。
2. **不杜撰** — 候选人没说过的经历、技能、数字一律不发明。没有真实证据就标 ❌。
3. **一次只走一件事** — 不混跑。解码出来如果还有含糊的地方，先澄清再往下。

---

## 文件结构

```
job-description-skill/
├── SKILL.md                      # 入口 · 路由 · 三条规则
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

## 设计思路

- **JD 反映三层信息** — 公司信号、招聘经理的真实期望、这个 role / product 本身。这个 skill 的工作就是看穿 HR 包装、把这三层拆出来。
- **决策优先于优化** — 大多数候选人在错的 role 上反复优化简历。先决定该不该投，再想怎么改。
- **每个评分都有公式** — 不是玄学。所有 Match Score / Interview Probability 都来自 `frameworks/` 里明写的公式，不同意可以反驳前提。

---

## 配套 skill
- [offer-toolkit-skill](https://github.com/yanliudesign/offer-toolkit-skill) — 三件套（JD · Resume · BQ）
- [resume-builder-skill](https://github.com/yanliudesign/resume-builder-skill) — 简历生成与美化
- [Behavior-question-skill](https://github.com/yanliudesign/Behavior-question-skill) — 行为面试 / 职业故事库

---

## License

MIT — fork it, remix it, ship your own version.

Created by [Dreameryanyan](https://www.linkedin.com/in/yanliudesign/) ·
[LinkedIn](https://www.linkedin.com/in/yanliudesign/) ·
[X](https://x.com/yanliudreamer) ·
[小红书](https://www.xiaohongshu.com/user/profile/5b2afdf311be104ac3c22931)
