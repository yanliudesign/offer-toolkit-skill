---
name: offer-toolkit-skill
description: "求职工具包。把「看到心动岗位 → 拿到 offer」拆成三个独立子 skill：① Job Description Skill 解码 JD 并出一份 Offer Strategy Report（该不该投 / 匹配度 / 面试题预测），② Resume Skill 把简历结构化并渲染成 11 套打印级模板，③ BQ Skill 挖掘真实经历、STAR 化，建可复用的行为面试故事库。任何求职相关请求（该不该投、改简历、准备行为面试、看 JD、Tell me about a time…）都从这里进，再路由到对应子 skill。关键词：求职, offer, career, job hunt, JD, job description, 简历, resume, CV, 行为面试, behavioral interview, BQ, STAR, tell me about a time, 面试准备。"
---

# Offer Toolkit

一整套求职 skill 的聚合入口。三条子 skill 各自独立可用，也可以组成完整的求职链路：

```
看到心动岗位 → [Job Description Skill] 解码 JD · 出 Offer Strategy Report
                    ↓ 决定投
              [Resume Skill] tailor + 美化 · 11 套模板 · 单文件 HTML
                    ↓ 拿到面试
              [BQ Skill] 挖故事 · 建故事库 · STAR 化 · 模拟面试
```

**顶层原则（三条子 skill 共用）：**

1. **绝不杜撰。** 所有经历、职责、数字都必须来自用户真实提供的内容。可以引导、追问、把弱的改强，绝不编公司、职位、成果、量化数字。
2. **一次只问一个问题。** 挖掘 / 建简历 / 准备 BQ 都是对话，不是问卷。
3. **先结构化，再产出。** 无论是简历还是故事，先落到标准数据模型，确认无误再渲染 HTML / 生成答案。

---

## 路由：用户进来先判断意图

| 用户说的话 | 走哪个子 skill |
|---|---|
| 贴出一份 JD / "这个岗位我该不该投" / "帮我看看这份工作" / "match score" / "面试会问什么" | → [`job-description-skill/`](job-description-skill/SKILL.md) |
| "帮我美化简历" / "改简历" / 上传 PDF/docx / "我没有简历帮我做一份" / "换个模板" / LinkedIn 导入 | → [`resume-skill/`](resume-skill/SKILL.md) |
| "帮我准备 behavioral 面试" / "Tell me about a time…" / "帮我挖一个面试故事" / "STAR 怎么写" / "建我的故事库" / "Amazon LP 怎么准备" | → [`bq-skill/`](bq-skill/SKILL.md) |
| 一次交出 JD + 简历，想要"全套准备好" | → 先跑 `job-description-skill/`（生成 Offer Strategy Report，内含 Top 10 面试题） → 用户说"投" → 转 `resume-skill/` tailor → "拿到面试" → 转 `bq-skill/` JD-driven prep（JD-driven Top 20 + STAR 模板） |

判断不了就问一句：

> "你现在在求职链路的哪一步？
> · 看到一个心动岗位，还没决定要不要投 → **JD Skill**
> · 已经决定投，需要一份简历 → **Resume Skill**
> · 已经拿到面试，要准备行为面试题 → **BQ Skill**"

---

## 三个子 skill 各自的入口

每个子目录都是一份完整的 skill（各自有 `SKILL.md` + 独立 README）。可以聚合装，也可以只装其中一个。

### 1 · [Job Description Skill](job-description-skill/SKILL.md) — 求职链路的入口

把任何 JD 翻译成一份 10 节的 **Offer Strategy Report**（HTML 单文件，自动打开浏览器）：TL;DR 结论 · Match Score · Interview Probability · 公司背景 · JD 深度解码 · JD ↔ 简历逐条比对 · Gap 与补救 · 为什么投/不投 · 薪资 · 下一步 · Top 10 面试题 · 6 周行动计划。

三步：贴 JD → 给简历 → 自动生成 HTML 报告并打开。

### 2 · [Resume Skill](resume-skill/SKILL.md) — 简历生成与美化

把"我需要一份好看的简历"变成稳定流程：所有素材先汇入 `schema/resume-data.md` 定义的标准数据结构，再套模板渲染。换模板只是换皮，内容不丢。

三条入口：美化已有简历 / LinkedIn 导入 / 对话式建简历。
11 套打印级模板：Classic-ATS · Ledger · Tech Compact · Modern Sidebar · Pillar · Elegant Serif · Atelier · Timeline · Swiss · Executive · Color-block。
每次渲染同时输出**锁定版**（直接 Cmd+P 存 PDF）和**可编辑版**（浏览器里点字微调 + 浮动工具条）。

### 3 · [BQ Skill](bq-skill/SKILL.md) — 行为面试故事库

不是背答案，而是**建一套可复用的职业故事库**。流程：挖掘 → 结构化 → 打标 → 存库 → 复用。

能做的事：
- 挖新故事（四层追问引擎，专治"我没什么亮点"）
- 回答一道具体 BQ（先查库，命中就复用）
- 打磨已有答案（诊断 STAR 结构 + 改写）
- 模拟面试（一次一道，按目标公司风格）
- JD 驱动的 Top 20 BQ 选题 + STAR 模板 + HTML 报告（对接 job-description-skill）

---

## 安装

### Claude 用户

把整个 `offer-toolkit-skill/` 目录放进你的 skill 目录（例如 `~/.claude/skills/` 或 VS Code 的 prompts 目录），三条子 skill 会一起被发现。

**只想装其中一个？** 直接把对应子目录（如 `resume-skill/`）单独复制过去也可以，每个子 skill 都是自包含的。

### 手动调用

- 顶层调度：说"我要找工作 / 求职 / offer" → 走这份 SKILL.md 的路由
- 直接进子 skill：说"帮我美化简历" / "解码这份 JD" / "帮我准备 BQ" → 直接命中对应子 skill

---

## License

MIT — fork, remix, ship your own version.

Created by [Dreameryanyan](https://www.linkedin.com/in/yanliudesign/) · [LinkedIn](https://www.linkedin.com/in/yanliudesign/) · [X](https://x.com/yanliudreamer) · [小红书](https://www.xiaohongshu.com/notification)
