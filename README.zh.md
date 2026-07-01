# Offer Toolkit — Career Copilot OS

> 🌐 **中文** · [English](./README.md)

> 一整套求职流程的 **Career Copilot skill pack**。三个独立自包含的子 skill 打包成一个仓库——可以整包装，也可以只挑你需要的那个。

```
看到心动岗位 → [Job Description Skill] 解码 JD · 出 Offer Strategy Report
                    ↓ 决定投
              [Resume Skill] tailor + 美化 · 11 套打印级模板 · 单文件 HTML
                    ↓ 拿到面试
              [BQ Skill] 挖故事 · 建故事库 · STAR 化 · 模拟面试
```

---

## 里面有什么

三个子 skill，每一个都能独立使用：

| # | 子 skill | 做什么 | 入口 |
|---|---|---|---|
| 1 | **[Job Description Skill](job-description-skill/)** | 把任何 JD 解码成一份 10 节的 **Offer Strategy Report**（HTML 单文件）：TL;DR 结论、Match Score、Interview Probability、公司背景、JD 与简历逐条比对、Gap 与补救、为什么投/不投、薪资、Top 10 面试题、6 周行动计划。 | [`job-description-skill/SKILL.md`](job-description-skill/SKILL.md) |
| 2 | **[Resume Skill](resume-skill/)** | 美化已有简历 / 从 LinkedIn 导入 / 一问一答从零建简历。所有入口都汇入一份标准化数据结构，再套 **11 套打印级模板**（Classic-ATS、Ledger、Tech Compact、Modern Sidebar、Pillar、Elegant Serif、Atelier、Timeline、Swiss、Executive、Color-block）。每次渲染同时输出锁定的打印版和浏览器里可点字编辑的版本。 | [`resume-skill/SKILL.md`](resume-skill/SKILL.md) |
| 3 | **[BQ Skill](bq-skill/)** | 不是背答案——建一套**可复用的职业故事库**。用四层追问引擎挖掘真实经历，用 STAR/CAR 结构化，映射能力标签，沉淀成中英双语故事，任何行为面试题都能复用。Flow E：JD 驱动的 Top 20 选题 + STAR 模板 + HTML 报告。 | [`bq-skill/SKILL.md`](bq-skill/SKILL.md) |

---

## 三条共用原则

三个子 skill 都守同样的三条铁律：

1. **绝不杜撰。** 所有经历、职责、数字都必须来自用户真实提供的内容。可以引导、追问、把弱的改强，绝不编公司、职位、成果、量化数字。任何数字都向用户求证。
2. **一次只问一个问题。** 挖故事、建简历、准备 BQ 都是对话，不是问卷。
3. **先结构化，再产出。** 无论是简历还是故事，先落到标准数据模型，确认无误再渲染 HTML / 生成答案。

---

## 安装

### 作为 Claude / Copilot skill pack 整体安装

把整个 `offer-toolkit-skill/` 目录放进你的 skill 目录（例如 `~/.claude/skills/` 或 VS Code 的 prompts 目录），三条子 skill 一次性都被发现。

### 只想用其中一个

每个子 skill 都是自包含的。把任意一个子目录（例如 `resume-skill/`）单独复制出去也可以独立跑。

### 触发词

| 用户说 | 路由到 |
|---|---|
| "该不该投这个岗位" / 贴一份 JD / "帮我看看这份工作" | Job Description Skill |
| "帮我美化简历" / "帮我从零做一份" / 上传 PDF / 贴 LinkedIn | Resume Skill |
| "帮我准备 behavioral 面试" / "Tell me about a time…" / "帮我挖一个面试故事" | BQ Skill |
| 模糊的 "帮我找工作" / 一次交出 JD + 简历 | 顶层 [`SKILL.md`](SKILL.md) 路由 → 跑整条链 |

---

## 目录结构

```
offer-toolkit-skill/
├── SKILL.md                        # 顶层路由：意图 → 子 skill
├── README.md / README.zh.md
├── LICENSE                         # MIT
├── job-description-skill/          # ① JD 解码 & Offer Strategy Report
│   ├── SKILL.md · README.md · README.zh.md
│   ├── prompts/                    # decode / match / tailor / predict / go-no-go
│   ├── frameworks/                 # 解码模式、匹配 rubric、报告规格
│   ├── examples/                   # offer-strategy-template.html
│   ├── docs/                       # 报告预览
│   └── jd-bank/                    # 本地 JD 缓存（gitignored）
├── resume-skill/                   # ② 简历生成与美化
│   ├── SKILL.md · README.md · README.zh.md
│   ├── prompts/                    # beautify / linkedin-import / interview / editable-version
│   ├── schema/                     # resume-data.md — 共用数据模型
│   ├── guides/                     # writing-tips.md
│   ├── templates/                  # 11 套打印级 HTML 模板
│   └── docs/                       # 模板预览
└── bq-skill/                       # ③ 行为面试 / 职业故事 OS
    ├── SKILL.md · README.md · README.zh.md
    ├── prompts/                    # story-mining / structuring / jd-driven-prep
    ├── frameworks/                 # STAR/CAR、能力标签、公司画像
    ├── assets/                     # BQ 报告规格 + demo
    └── story-bank/                 # 用户资产 — 一份故事一个 .md
```

---

## 为什么要打包在一起

每个子 skill 原本都是独立仓库，仍在维护：

- [`job-description-skill`](https://github.com/yanliudesign/job-description-skill)
- [`resume-builder-skill`](https://github.com/yanliudesign/resume-builder-skill)
- [`Behavior-question-skill`](https://github.com/yanliudesign/Behavior-question-skill)

这个 toolkit 是**一站式打包版**，为想在一次 clone 里拿到完整 Career Copilot 链路的人准备——再加一层顶层 `SKILL.md`，根据你当前处在求职链的哪一步自动路由。

---

## License

MIT — 随便 fork、随便改、随便 ship 自己的版本。

Created by [Dreameryanyan](https://www.linkedin.com/in/yanliudesign/) ·
[LinkedIn](https://www.linkedin.com/in/yanliudesign/) ·
[X](https://x.com/dreameryanyan) ·
[小红书](https://www.xiaohongshu.com/user/profile/5c1d8d3c000000001202b7fb)
