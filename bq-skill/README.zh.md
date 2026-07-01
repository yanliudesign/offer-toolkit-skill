# BQ Skill — Career Story OS

> 🌐 **中文** · [English](./README.md)

帮求职者把"会回答某道行为面试题"升级成"拥有一套可复用的职业故事库"。

![流程 E 报告 — JD 驱动的 Top 20 选题 + STAR 模板](assets/preview.png)
<sub>流程 E 产出:对着 JD 反推的 Top 20 选题,带 STAR 模板和可改写的范例答案。<i>(Demo 用虚构候选人,无真实个人数据。)</i></sub>

## 核心循环
挖掘 (Mine) → 结构化 (Structure) → 打标 (Map) → 沉淀 (Save) → 复用 (Reuse)

## 目录
```
bq-skill/
├── SKILL.md                      # 入口：意图路由 + 五条流程
├── prompts/
│   ├── story-mining.md           # ★ 四层追问引擎（流程 A）
│   ├── structuring.md            # 诊断+改写已有答案（流程 C）
│   └── jd-driven-prep.md         # ★ JD×简历 → Top 20 选题 + STAR 模板（流程 E）
├── frameworks/
│   ├── star-car.md               # STAR/CAR/SOAR 选择 + 一稿多用
│   ├── competency-tags.md        # 能力标签词典 + BQ 题型反查
│   └── company-profiles.md       # Amazon LP / Meta / Anthropic / OpenAI 风格
├── assets/
│   └── bq-prep-report.md         # 流程 E 的 editorial HTML 报告规范
└── story-bank/                    # 用户资产，每个故事一个 .md
    ├── _index.md                 # 能力标签 → 故事 反查表
    ├── _story-template.md        # 故事模板
    └── convince-team-rewrite.md  # 示例故事（可删）
```

## 与 job-description-skill 挂钩
流程 E 直接复用 [job-description-skill](https://github.com/yanliudesign/job-description-skill) 解码出的
Must Have + Hidden Signals，针对某个具体岗位反推 **Top 20 BQ 选题**，并用简历里的真实经历
为每题搭 STAR 准备模板，输出一份 editorial 风格的 HTML 报告。形成 Career Copilot 闭环：
JD 解码 → 匹配/改简历 → **BQ 选题 + 故事准备**。

## 用法
对 Claude 说"帮我准备 behavioral 面试""帮我挖一个故事建库""贴一道 BQ 帮我答"，或直接 `/bq-skill`。

## 版本
- **v0.6（当前）**：Story Mining 引擎 + 单故事完整闭环 + 双语产出 + 轻量模拟 + **流程 E（JD 驱动 Top 20 选题 + STAR 模板 + editorial HTML 报告，挂钩 job-description-skill）**。
- v1 计划：能力词典/公司档案加深、库检索复用打磨。
- v2 计划：模拟面试加深（按公司出题 + 评分反馈）。

## 待用户注入（护城河）
`prompts/story-mining.md` 的追问话术、`frameworks/competency-tags.md` 的标签词典，
是 coach 经验最该私有化的部分——把你独有的话术和标签喂进去，Skill 会越来越像"你"。
