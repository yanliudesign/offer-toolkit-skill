<div align="center">

**中文** · [English](./README.md)

# 💰 Salary Negotiation Skill · 薪资谈判 Skill

---

**把任何一份 offer letter 翻译成一份可执行的谈判 playbook — 只要 3 步。**

[![License](https://img.shields.io/badge/LICENSE-MIT-4c8bf5?style=flat-square&labelColor=333)](./LICENSE)
[![Version](https://img.shields.io/badge/VERSION-1.0.0-2ea44f?style=flat-square&labelColor=333)]()
[![Stars](https://img.shields.io/github/stars/yanliudesign/salary-negotiation?style=flat-square&label=STARS&color=e37f2c&labelColor=333)](https://github.com/yanliudesign/salary-negotiation/stargazers)

[![Claude Code](https://img.shields.io/badge/Claude_Code-Skill-d97757?style=flat-square&labelColor=1a1a1a&logo=anthropic&logoColor=white)](https://claude.ai/code)
[![Codex](https://img.shields.io/badge/Codex-Skill-2ea44f?style=flat-square&labelColor=1a1a1a)]()
[![OpenCode](https://img.shields.io/badge/OpenCode-Skill-4c8bf5?style=flat-square&labelColor=1a1a1a)]()
[![OpenClaw](https://img.shields.io/badge/OpenClaw-Skill-8b5cf6?style=flat-square&labelColor=1a1a1a)]()
[![Hermes](https://img.shields.io/badge/Hermes-Skill-e879a8?style=flat-square&labelColor=1a1a1a)]()

</div>

> 📦 属于 **[offer-toolkit-skill](https://github.com/yanliudesign/offer-toolkit-skill)** 求职工具包 — 装工具包等于一次性拿到 Search · JD · Resume · BQ · Compare · Negotiate 六条子 skill。

一个专门做薪资谈判的 agent skill。模拟前 FAANG 招聘官 + 薪酬策略师，把任何一份 offer letter 翻译成一份可执行的谈判 playbook：哪几项有真正的杠杆、你实际有多少筹码（以及没有的部分）、先谈什么、电话和邮件到底怎么说、招聘官会怎么反弹每种反弹怎么打两轮、以及最重要的三条 stop-line（SIGN / WALK / FREEZE）——防止谈到最后 offer 消失。这**不是**"祝你好运，加油谈"式的通用建议，是真实谈判动力学的模拟。

---

## 整个 skill 只有 3 步

用任何模糊的话调用（"帮我谈谈这份 offer" / "谈薪" / "help me negotiate"）都会走同一条路径：

1. **贴 offer 细节** — 公司 / 岗位 / Level / Base / RSU（total + 归属曲线 + ref price）/ Sign-on / Bonus / 地点 / Deadline。
2. **答 5 个 context 问题** — 竞争 offer / deadline 弹性 / seniority 信号 / 风险偏好 / 最看重的 2 项（Cash · Equity · Title · Location · WLB，只选 2）。
3. **HTML playbook 自动弹出** — 单文件 Negotiation Playbook 生成到 `~/Desktop/Claude skills/salary-negotiation-<slug>.html`，自动在浏览器打开。里面包含：TL;DR 结论、诊断、杠杆图、按优先级排序的 ask 表、电话 + 邮件脚本、3 种反弹 × 每种 2 轮的 counter-simulation，以及 3 条 stop-line。

然后循环：把 recruiter 的真实回话贴回来 → skill 更新第 2 轮 counter-simulation。

---

## Negotiation Playbook · 6 节报告框架

Wizard 跑完的默认交付物是一份单文件 HTML 报告，存到 `~/Desktop/Claude skills/salary-negotiation-<slug>.html`。固定 6 节骨架 + TL;DR 预头 + 关键指标：

| # | 章节 | 回答什么 |
|---|------|----------|
| — | **TL;DR · 一分钟结论** | 签 / 反 / 走。一句话按优先级排序的 ask。 |
| — | **关键指标** | TC vs 市场 P50/P75 · 杠杆汇总 · deadline 倒计时。 |
| **1** | **Offer 诊断** | Base / RSU / Sign-on / Bonus 每项对标市场，标 **LOW / MEDIUM / HIGH** 杠杆。所有数字必须能追溯到 Levels.fyi / Blind / 用户提供的 offer。 |
| **2** | **杠杆图** | 你的力量（竞争 offer · 时机 · 稀缺性）· 招聘官的力量（预算 · level 上限 · pool）· 你的 blind spots。 |
| **3** | **策略** | Modality A/B/C/D（激进双开 / 单点集中 / 收尾轻抗 / 直接签）+ 按优先级排序的 ask 表，每项标目标 / 底线。 |
| **4** | **脚本** | 📞 电话脚本（Beat 1–4，中英对照，一字不改可念）+ 📧 邮件版本 + recruiter 的 3 种首次回话。 |
| **5** | **Counter Simulation** | 3 种 pushback × 每种 2 轮（"这是最好的了" / "预算固定" / "会考虑其他候选人"）+ 每轮的 stop-signal。多数负面结局发生在第 2 轮而不是第 1 轮。 |
| **6** | **最终建议** | 要什么 / 别推什么 / **3 条 stop-line**（SIGN / WALK / FREEZE），数字明确 + 紧急协议（rescind 风险 / exploding offer / deadline 挤压）。 |

报告内置 **Export PDF** 和 **Copy Scripts** 按钮。规格见 [`frameworks/negotiation-report.md`](frameworks/negotiation-report.md)，骨架见 [`examples/negotiation-report-template.html`](examples/negotiation-report-template.html)。

---

## 5 条铁律

1. **绝不虚构 comp 数据。** 所有 P50/P75 必须能追溯到 Levels.fyi / Blind / 用户提供的 offer。查不到就标 `[需查]`。
2. **数字给区间，不给单点。** "$220–230K" 不是 "$225K"。
3. **每一句脚本必须一字不改可念。** 禁止 "you might say something like…"。
4. **Counter Simulation 每种 pushback 必须走 2 轮。** 多数负面结局发生在第 2 轮。
5. **必须写 stop-line。** SIGN / WALK / FREEZE，数字明确。没有 stop-line = 谈判无限循环 = offer 消失。

---

## 文件结构

```
salary-negotiation-skill/
├── SKILL.md                         # 入口 · 路由 · 3 步流程 · 5 条铁律
├── prompts/                         # 6 条内部流程
│   ├── offer-diagnosis.md           # §1
│   ├── leverage-map.md              # §2
│   ├── negotiation-strategy.md      # §3
│   ├── script-generator.md          # §4
│   ├── counter-simulation.md        # §5
│   └── final-recommendation.md      # §6
├── frameworks/                      # 可复用的框架 / 评分尺
│   ├── comp-benchmarks.md           # 市场数据查询方法（Levels.fyi · Blind…）
│   ├── leverage-heuristics.md       # 各组件 LOW/MED/HIGH 判定规则
│   ├── negotiation-tactics.md       # Anchoring · silence · reframe · brackets · 24-hour rule
│   ├── recruiter-playbook.md        # 招聘官 20 种话术 × 20 种应对
│   └── negotiation-report.md        # HTML 报告规格 + 强制 footer
├── examples/                        # 参考骨架（不含个人数据）
│   └── negotiation-report-template.html
└── deal-bank/                       # 已谈判过的 deal 反查库（本地不进 git）
    ├── _index.md                    # 索引
    └── _deal-template.md            # 新 deal 起手模板
```

---

## 设计思路

- **一份 offer 是初稿，不是终稿。** 招聘官对多数 senior offer 都预期到 counter。真正的问题是**你到底有多少杠杆**——这就是 §1 和 §2 存在的意义：把它诚实地算出来。
- **杠杆是逐项不同的。** Base 比 RSU 难动，RSU refresher 比 sign-on 难动，sign-on 比 bonus 灵活。§3 按这个顺序排。
- **每种反弹都有对应剧本。** "这是最好的了" / "预算固定" / "会再看看候选池"——这些不是针对你，是模板化的招式。§5 给你每种招式的对应打法，每种打两轮。
- **失败模式不是要得太多，而是谈得没完。** 每份 playbook 都以 stop-line 收尾：什么时候签、什么时候走、什么时候冻结对话。

---

## 配套 skill

串起完整链路 — Search → JD → Resume → BQ 拿到 offer，需要时先比较，再回这里 close：

- [offer-toolkit-skill](https://github.com/yanliudesign/offer-toolkit-skill) — 六件套（Search · JD · Resume · BQ · Compare · Negotiate）
- [job-description-skill](https://github.com/yanliudesign/job-description-skill) — JD 解码器 + should-I-apply
- [resume-builder-skill](https://github.com/yanliudesign/resume-builder-skill) — 简历生成与美化（11 套打印级模板）
- [Behavior-question-skill](https://github.com/yanliudesign/Behavior-question-skill) — 行为面试 / 职业故事库
- [offer-compare-skill](https://github.com/yanliudesign/offer-compare-skill) — 多份 offer 先比较，再谈选中的一份

```
看到心动岗位 → JD Skill（解码 · 匹配 · should-I-apply）
                     ↓ 决定投
                 Resume Skill（tailor + 美化）
                     ↓ 拿到面试
                 BQ Skill（挖故事 · 模拟面试）
                         ↓ 拿到 offer（可能不止一份）
                      多份 offer → Offer Compare（明确选一个）
                         ↓
                     Salary Skill（诊断 · 脚本 · counter · 签）
```

---

## License

MIT 协议 — 随便 fork、改造、发一个你自己的版本。

Created by [Dreameryanyan](https://www.linkedin.com/in/yanliudesign/) · [LinkedIn](https://www.linkedin.com/in/yanliudesign/) · [X](https://x.com/yanliudreamer) · [小红书](https://www.xiaohongshu.com/notification)
