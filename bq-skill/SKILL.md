---
name: bq-skill
description: "Behavioral Question / Career Story OS。帮求职者挖掘真实经历、用 STAR/CAR 结构化、映射能力标签、构建可复用的中英双语故事库（Story Bank）；并能接入 JD + 简历，针对具体岗位生成 Top 20 BQ 选题 + 基于真实经历的 STAR 准备模板（HTML 报告）。不是背答案，而是建立可复用的职业叙事体系，让任何行为面试题都能自然作答。关键词：behavioral question, BQ, 行为面试, STAR, 故事库, Amazon LP, 职业故事, tell me about a time, 面试准备, JD 面试题预测, top 20 题。"
---

# BQ Skill — Career Story OS

把"会回答某道 BQ"升级成"拥有一套可复用的职业故事库"。核心循环：

```
挖掘 (Mine) → 结构化 (Structure) → 打标 (Map) → 沉淀 (Save) → 复用 (Reuse)
```

**第一原则：先查库，再开工。** 任何 BQ 进来，先看 `story-bank/_index.md` 有没有能命中的故事；能复用就复用/微调，不能再触发新一轮挖掘。这就是"越用越懂用户"。

**第二原则：一次只问一个问题。** 挖掘是对话，不是问卷。问一个 → 等回答 → 顺着答案追问。永远不要一次抛一串问题。

**第三原则：不替用户编故事。** 所有素材必须来自用户真实经历。可以引导、可以追问、可以帮他把模糊的说清楚，但绝不杜撰 Task / Action / Result。量化数字一律向用户求证。

---

## 路由：用户进来时先判断意图

| 用户说的话 | 走哪条流程 |
|---|---|
| "帮我准备面试" / "我要建故事库" / 给一段经历 | **挖掘新故事** → `prompts/story-mining.md` |
| 贴出一道具体 BQ（"Tell me about a time…"） | **回答一道题**（先查库，下方流程） |
| "我这个故事讲得好吗" / 贴出已有答案 | **打磨已有故事** → `prompts/structuring.md` |
| "模拟面试" / "出几道题考我" | **模拟面试**（v1 轻量版，下方） |
| 给了 **JD + 简历** / "针对这个岗位帮我准备 BQ" / "这家会问什么、我怎么答" | **JD 驱动的 BQ 选题 + 准备** → `prompts/jd-driven-prep.md` |
| "看看我的故事库" / "我有哪些故事" | 读 `story-bank/_index.md` 汇报 |

判断不了就问一句："你是想**挖新故事建库**，还是**针对某道具体题目**准备？"

---

## 挖掘新故事

完整执行 `prompts/story-mining.md` 里的四层追问引擎：

1. **破冰层** — 专治"我没什么亮点"。用反事实提问 + 四象限时间锚点扫描，先捞出 3–5 个候选事件。
2. **深挖层** — 对选中的事件，逐个补全 STAR，重点逼出最常缺的 **T（你具体做了什么，而非团队）** 和 **R（量化结果）**。
3. **打标层** — 挖完映射能力标签（`frameworks/competency-tags.md`）+ 判断能打哪些公司维度（`frameworks/company-profiles.md`）。
4. **沉淀层** — 按 `story-bank/_story-template.md` 写成一个故事文件，并更新 `_index.md`。

一次会话聚焦挖 **1 个故事的完整闭环**就够了，挖深比挖多重要。挖完问用户要不要继续下一个。

---

## 回答一道具体 BQ

1. **解析题目**：这道题在考什么能力？（参考 `frameworks/competency-tags.md` 反查）
2. **查库**：读 `story-bank/_index.md`，找 tags / competencies 命中的故事。
   - 命中 → 取出故事，按这道题的角度重新组织开场和落点（同一个故事可以打多道题，框架见 `frameworks/star-car.md`）。
   - 未命中 → 转「挖新故事」 现场挖一个，挖完再回答。
3. **产出答案**：默认中英双语 —— **英文是面试可直接说的版本**，附**中文要点**供复盘。
4. **顺手沉淀**：如果是现场新挖的，存进库。

---

## 打磨已有故事

执行 `prompts/structuring.md`：诊断用户现有答案的结构问题（常见：Situation 太长、看不出"我"做了什么、没有量化 Result、能力标签不清晰），给出改写。改完可存库。

---

## 模拟面试

1. 问目标公司/岗位，加载 `frameworks/company-profiles.md` 对应风格。
2. 按该公司常考维度出 1 道题，**一次一道**。
3. 用户作答后给反馈：结构（STAR 是否完整）、能力信号是否清晰、量化是否到位、与该公司维度的契合度。
4. 把答得好的故事提示用户存库。

---

## JD 驱动的 BQ 选题 + 准备

针对**某个具体岗位**做定向 BQ 准备。完整执行 `prompts/jd-driven-prep.md`，五步闭环：

```
① 上传 JD → ② 上传简历 → ③ 生成 Top 20 选题（对着 JD）→ ④ 基于你的经历给 STAR 准备模板 → ⑤ 输出 HTML 报告
```

1. **拿 JD** — 优先复用 `../job-description-skill/jd-bank/` 里已解码的 Must Have + Hidden Signals；没有就让用户贴 JD，先过一遍解码。
2. **拿简历全文** — 给每段经历打能力标签，为配对做准备。简历太薄 → 转「挖新故事」 先挖几个故事。
3. **交叉分析 → Top 20 选题** — 四类（Behavior 通用 / 公司价值观定制 / 岗位专业向 / Level 阶段定制）。每题必带「考什么 + **为什么这家会问**（指向 JD 某条 Must Have / Hidden Signal）+ 配哪个故事」。
4. **逐题准备模板** — 默认对 **Top 5 必练**写完整 STAR 模板：S/T 用简历事实填实，**A/R 留占位符**引导用户填真实动作和数字，**绝不杜撰**。标注一稿多用。
5. **缺口清单** — JD 要、简历没素材的题如实列出，导流到「挖新故事」 现场挖。
6. **HTML 报告** — 默认输出到 `~/Desktop/Claude skills/bq-prep-<company>-<role>-<YYYYMM>.html`（视觉规范见 `assets/bq-prep-report.md`）。
7. **回写** — 把 JD↔故事映射写回 job-description-skill 的 jd-bank 文件「Predicted Questions」，形成 Career Coach 闭环。

> 这是 job-description-skill 面试预测流程的下游深化：那边给「会问什么」，这里给「**用你的真实经历怎么答 + 模板**」。

---

## 故事库（Story Bank）

- 位置：本 skill 目录下 `story-bank/`，每个故事一个 `.md`。
- 元数据靠 frontmatter（tags / competencies / company_fit / metrics / framework / status）。
- `_index.md` 是反查表：**能力标签 → 故事文件**，是「答题」 复用的入口。
- 每次新增或修改故事，**务必同步更新 `_index.md`**。

---

## 参考文件（按需读取，别一次全加载）

- `prompts/story-mining.md` — 四层追问引擎（「挖新故事」 核心）
- `prompts/structuring.md` — 结构化诊断与改写（「打磨已有故事」）
- `prompts/jd-driven-prep.md` — JD × 简历 → Top 20 选题 + 准备模板（「JD 驱动准备」，挂钩 job-description-skill）
- `assets/bq-prep-report.md` — 「JD 驱动准备」 的 HTML 报告视觉规范
- `frameworks/star-car.md` — STAR / CAR / SOAR 何时用哪个、同一故事多角度复用
- `frameworks/competency-tags.md` — 能力标签词典 + BQ 题型反查
- `frameworks/company-profiles.md` — Amazon LP / Meta / Anthropic / OpenAI 等评价风格
- `story-bank/_story-template.md` — 故事文件模板
- `story-bank/_index.md` — 故事索引
