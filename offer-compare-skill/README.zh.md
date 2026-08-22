<div align="center">

**中文** · [English](./README.md)

# ⚖️ Offer Compare Skill · Offer 对比决策器

---

**把两份（或多份）offer 变成一条明确、有立场的推荐 — 只要 3 步。**

[![License](https://img.shields.io/badge/LICENSE-MIT-4c8bf5?style=flat-square&labelColor=333)](./LICENSE)
[![Version](https://img.shields.io/badge/VERSION-1.0.0-2ea44f?style=flat-square&labelColor=333)]()
[![Stars](https://img.shields.io/github/stars/yanliudesign/offer-compare-skill?style=flat-square&label=STARS&color=e37f2c&labelColor=333)](https://github.com/yanliudesign/offer-compare-skill/stargazers)

[![Claude Code](https://img.shields.io/badge/Claude_Code-Skill-d97757?style=flat-square&labelColor=1a1a1a&logo=anthropic&logoColor=white)](https://claude.ai/code)
[![Codex](https://img.shields.io/badge/Codex-Skill-2ea44f?style=flat-square&labelColor=1a1a1a)]()
[![OpenCode](https://img.shields.io/badge/OpenCode-Skill-4c8bf5?style=flat-square&labelColor=1a1a1a)]()
[![OpenClaw](https://img.shields.io/badge/OpenClaw-Skill-8b5cf6?style=flat-square&labelColor=1a1a1a)]()
[![Hermes](https://img.shields.io/badge/Hermes-Skill-e879a8?style=flat-square&labelColor=1a1a1a)]()

</div>

> 📦 属于 **[offer-toolkit-skill](https://github.com/yanliudesign/offer-toolkit-skill)** 求职工具包 — 装工具包等于一次性拿到 Search · JD · Resume · BQ · Compare · Negotiate 六条子 skill。

一个专门做 offer 对比决策的 agent skill。模拟一位**有立场、会得罪人**的 Senior Career Decision Advisor：把两份（或多份）offer 扔进来，返回一份 HTML 决策报告——诚实的 4 年 TC 区间（所有假设显式列出）、7 维打分并排（Comp · Growth · AI 敞口 · 公司强度 · 团队风险 · 晋升速度 · 生活方式）、5 条大多数人漏掉的隐藏信号（front-loaded vs long-term upside · resume value · switch-out 难度 · 不确定性）、每份 offer 4-6 条 risk，最后——最重要的——**一条明确推荐**（禁止"都不错，看你自己"），并附 "If you are X → A / If you are Y → B" 分叉判定给另一类人。这**不是**并排放两列数字，是**一个明确的选择**。

---

## 整个 skill 只有 3 步

用任何模糊的话调用（"帮我比一下两个 offer" / "两份 offer 该选哪个" / "compare these offers"）都会走同一条路径：

1. **贴两份 offer** — 每份的 Company / Role / Level / Location / TC breakdown（Base + Bonus + RSU 含 4 年 vest schedule + Sign-on）。缺字段一次追问一批，绝不挤牙膏。
2. **补 priorities & 当前处境**（optional 但强烈建议）— 挑 2-3 个优先级（💰 钱 · 📈 成长 · 🤖 AI · 🏢 稳定 · 🌍 生活方式 · 🚀 晋升 · 🎯 resume 增值 · 🔁 未来跳槽），再告诉我 visa / burnout / 家庭 / 目前 base / deadline。
3. **HTML 决策报告自动弹出** — 单文件报告生成到 `~/Desktop/Claude skills/offer-compare-<A>-vs-<B>-<YYYYMM>.html`，自动在浏览器打开。里面包含：Verdict、Assumptions 块、§1 Offer Breakdown、§2 Dimension Compare（7 维）、§3 Hidden Signals（5 条）、§4 Risk Analysis、§5 Recommendation。内置 EN / 中文 双语切换 + Export PDF / Markdown。

然后循环：改一个假设 / 加一条 priority → skill 重新生成。全部缓存到 `offer-bank/`，下次说"上次那个 A vs B"直接查库，不用重贴。

---

## Decision Report · 5 节报告框架

Wizard 跑完的默认交付物是一份单文件 HTML 报告，存到 `~/Desktop/Claude skills/offer-compare-<A>-vs-<B>-<YYYYMM>.html`。固定 5 节骨架 + Verdict + Assumptions 预头：

| # | 章节 | 回答什么 |
|---|------|----------|
| — | **Verdict** | 一句话推荐（**A** / **B** / **两个都拒**）+ ⭐ 决心指数。**禁止中性**。 |
| — | **Assumptions** | 所有假设显式列出（RSU vest schedule · 汇率 · bonus target · 股价波动）。任一不对，重跑。 |
| **1** | **Offer Breakdown** | Base / Bonus / RSU / Sign-on / 4 年 TC **区间** / equity risk / 公司 stability，并排表格。 |
| **2** | **Dimension Compare** | 7 维评分：💰 Comp · 📈 Growth · 🤖 AI Exposure · 🏢 Company Strength · 👤 Manager/Team Risk · 🔁 Promo Speed · 🌍 Lifestyle。 |
| **3** | **Hidden Signals** | 5 条大多数人漏掉的信号：front-loaded vs long-term upside · uncertainty · resume value · switch-out 难度。 |
| **4** | **Risk Analysis** | 每份 offer 4-6 条显式 risk，按 equity / role / team / market / life 分类。 |
| **5** | **Recommendation** | 明确推荐 + tradeoff 说明 + "If you are X → A / If you are Y → B" 分叉。 |

报告内置 **EN / 中文** 切换、**Export PDF**、**Export Markdown** 按钮。规格见 [`frameworks/offer-compare-report.md`](frameworks/offer-compare-report.md)，骨架见 [`examples/offer-compare-template.html`](examples/offer-compare-template.html)。

---

## 3 条铁律

1. **禁止中性。** 必须给一条明确推荐，同时用 "If X → A / If Y → B" 兜底另一类人。"都不错，看你自己"是这类工具的最大失败模式。
2. **数字给区间 + 显式假设。** 4 年 TC 永远给 `$X ~ $Y`（RSU refresh 有无 · 股价 ±30% · bonus min/max）。所有假设在顶部 Assumptions 块每条独立列出。单点数字是这类工具最大的可信度杀手。
3. **不编内部情报。** 公司信号（team health / manager style / promo speed）只能从**公开信息 + 用户提供**推断，标"我从 ___ 推断"。用户没给过的数字（base、股价、目前包）标 `[需用户补充]`，**绝不猜**。

---

## 文件结构

```
offer-compare-skill/
├── SKILL.md                              # 入口 · 路由 · 3 步流程 · 3 条铁律
├── prompts/                              # 5 条内部流程
│   ├── offer-breakdown.md                # §1
│   ├── dimension-compare.md              # §2
│   ├── hidden-signals.md                 # §3
│   ├── risk-analysis.md                  # §4
│   └── recommendation.md                 # §5
├── frameworks/                           # 可复用的框架 / 评分尺
│   ├── dimension-rubric.md               # 7 维评分标准 + 权重
│   ├── hidden-signals-dictionary.md      # 5 条隐藏信号的判定规则
│   ├── risk-taxonomy.md                  # 5 大类 risk × 常见 pattern
│   └── offer-compare-report.md           # HTML 报告规格 + 强制 footer
├── examples/                             # 参考骨架（不含个人数据）
│   └── offer-compare-template.html
└── offer-bank/                           # 已比过的决策反查库
    ├── _index.md                         # 索引
    └── _template.md                      # 新决策起手模板
```

---

## 设计思路

- **两份 offer 是一个决策，不是一张表。** 会把"我拿了两份 offer"扔进来的人，多半心里已经有偏向 — 他们要的是一个诚实到愿意说出来的声音，不是躲在中性后面的分析师。这个 skill 的工作就是当那个声音。
- **决定去哪家的维度往往不是 comp。** Comp 支配了表格，但**真正决定**的维度往往是 AI 敞口、resume 增值、或跳槽难度。§2 和 §3 存在的意义就是把这些浮出来。
- **不带区间的 4 年 TC 就是撒谎。** 只是 RSU refresh 假设有无，就能让 TC 摆动 30-40%。给区间才能把 tradeoff 摊开。
- **每份 offer 都有 hidden risk，两份都有。** §4 必须把两份都写满 — 包括被推荐的那份。否则 §5 就成了推销文，不是决策。

---

## 配套 skill

跟这些串起来，覆盖完整求职链路：

- [offer-toolkit-skill](https://github.com/yanliudesign/offer-toolkit-skill) — 六件套（Search · JD · Resume · BQ · Compare · Negotiate）
- [job-description-skill](https://github.com/yanliudesign/job-description-skill) — JD 解码器 + should-I-apply
- [resume-builder-skill](https://github.com/yanliudesign/resume-builder-skill) — 简历生成与美化（11 套打印级模板）
- [Behavior-question-skill](https://github.com/yanliudesign/Behavior-question-skill) — 行为面试 / 职业故事库
- [salary-negotiation](https://github.com/yanliudesign/salary-negotiation) — 谈这里选出来的那份 offer

```
看到心动岗位 → JD Skill（解码 · 匹配 · should-I-apply）
                     ↓ 决定投
                 Resume Skill（tailor + 美化）
                     ↓ 拿到面试
                 BQ Skill（挖故事 · 模拟面试）
                     ↓ 拿到 offer（可能不止一份）
             Offer Compare（本 skill — 明确挑一个）
                     ↓ 决定去哪家
             Salary Skill（诊断 · 脚本 · counter · 签）
```

---

## License

MIT 协议 — 随便 fork、改造、发一个你自己的版本。

Created by [Dreameryanyan](https://www.linkedin.com/in/yanliudesign/) · [LinkedIn](https://www.linkedin.com/in/yanliudesign/) · [X](https://x.com/yanliudreamer) · [小红书](https://www.xiaohongshu.com/user/profile/5b2afdf311be104ac3c22931)
