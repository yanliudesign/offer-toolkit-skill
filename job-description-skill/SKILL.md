---
name: job-description-skill
description: "Job Description 解码器 + Offer 策略系统。把任何 JD 翻译成「这家公司到底在招什么人 / 我的匹配度 / Gap 在哪 / 为什么投/不投 / 面试会问什么 / 下一步怎么走」。只有 3 步：贴 JD → 给简历 → 自动生成并打开一份 HTML Offer Strategy Report。是整个求职链路的入口，向下衔接 Resume Skill 和 BQ Skill。关键词：job description, JD, 职位描述, 匹配度, ATS, resume tailor, 简历定制, 招聘经理, 投不投, should I apply, 面试预测, offer strategy。"
---

# Job Description Skill — JD Decoder & Offer Strategy OS

把一份 JD 从「招聘话术」翻译成「**你能用的求职情报**」，**一次性产出一份单文件 HTML Offer Strategy Report**，自动在浏览器打开。

下游可一键接 **Resume Skill**（拿着 Gap / Tailor 结果继续打磨简历）和 **BQ Skill**（拿着预测题目去练故事），形成 Career Copilot 闭环。

---

## 整个 skill 只有 3 步

### Step 1 · 贴 JD

开场只说一句话：

> "把你想分析的 **Job Description 链接或全文** 贴给我。链接抓不到内容就直接粘贴 JD 文本。"

收到后：
- 链接 → 尝试抓取；抓不到 → 让用户粘全文，**别根据公司名瞎猜 JD**。
- 同时确认 **公司名 / 岗位 / Level**（JD 没明写就追问一次）。
- **先查 [jd-bank/_index.md](jd-bank/_index.md)** — 同公司同岗位半年内分析过，告诉用户"上次解码过，要不要直接复用"。

### Step 2 · 给简历或 LinkedIn

三选一，明牌列出来：

> "为了算匹配度 / 出 Gap / 预测面试题，需要了解你。三选一：
> - 🅰️ **上传 / 粘贴简历全文**（PDF / Word / 文本都行）— 强烈推荐，结果最准
> - 🅱️ **粘贴你的 LinkedIn 全文**（不是只给 URL，要全文）
> - 🅲️ **简略介绍一下自己**（还没有简历的情况）"

如果用户选 🅲️，**一次问一个问题**，别一次列 6 个：当前 Title + 年限 → 行业 → 近 2-3 段经历（公司 + 负责什么 + 1 个最亮成果）→ 最强 1-2 个技能 → 想往哪个方向走。

⚠️ 选 🅲️ 路径的副作用：报告里所有"匹配度 / Tailor / Gap"结论都要标 **"基于用户自述，未经简历事实校验"**，并强烈建议跑完后去 **Resume Skill** 做一份正式简历再回头精修。

### Step 3 · 生成 HTML 并自动打开

**收齐 JD + 简历后，不要再分别请示用户跑 Decode / Match / Predict / Should I Apply** — 一口气在后台跑完 5 条流程（[prompts/](prompts/) 下的 5 份文件），把结果直接组装成一份 HTML Offer Strategy Report：

1. 在内存里跑 Flow 1 → 2 → 4 → 5（Flow 3 Tailor 只取关键 diff，简历整体打磨交给 Resume Skill）。
2. 按 [frameworks/offer-strategy-report.md](frameworks/offer-strategy-report.md) 的规格 + [examples/offer-strategy-template.html](examples/offer-strategy-template.html) 的骨架组装一份 10 节报告（TL;DR · 关键指标 · 1-10）。
   - ⛔ **品牌 footer 是强制项，不是装饰。** 报告结尾必须**原样**包含 `<footer>` 里的 `JD SKILL.` brand mark + `Created by Dreameryanyan` 副标题 + LinkedIn / X / 小红书三个社交按钮（含对应 CSS：`.brand-block` / `.brand-mark` / `.socials` / `.foot-meta`）。这是作者署名，**无论报告多长、数据多少都不许删或简化**。生成时直接从 [frameworks/offer-strategy-report.md](frameworks/offer-strategy-report.md) 末尾「📌 强制 Footer 区块」整段抄过去。
3. 写到 `~/Desktop/Claude skills/offer-strategy-<company>-<role>-<YYYYMM>.html`。
   - 写完后**自检一次**：文件里必须能搜到 `Dreameryanyan`、`brand-mark`、`yanliudreamer`、`xiaohongshu` 四个关键词。缺任何一个 = footer 被丢了，必须补回再继续。
4. **自动打开**：跑 `open "<完整路径>"`（macOS）/ `xdg-open` (Linux) / `start` (Windows)，让 HTML 直接在浏览器弹出来。
5. **同步 [jd-bank/](jd-bank/)**：按 [jd-bank/_jd-template.md](jd-bank/_jd-template.md) 写一份 `<slug>.md`，更新 [jd-bank/_index.md](jd-bank/_index.md)，文件末尾加一行 `> 📊 HTML 报告：~/Desktop/Claude skills/offer-strategy-<slug>.html`。

最后一句收尾：

> "报告已生成并在浏览器打开 ✅
> · 📊 `~/Desktop/Claude skills/offer-strategy-<slug>.html`
> · 内置 **Export PDF** 和 **Export Markdown** 两个按钮
> · 这份 JD 已存进 [jd-bank/](jd-bank/)，下次提到自动复用
>
> 下一步：
> - 决定投 → 交给 **Resume Skill** 做整体简历打磨
> - 准备 Behavior 题 → 转 **BQ Skill** 挖故事
> - 看下一份 JD → 直接贴过来"

---

## 三条铁律（内部 5 条流程跑的时候都要守）

**铁律一 · 先解码，再做任何事。**
跑 Match / Tailor / Predict 之前**必须先在内存里跑完 JD Decoder 的 5 图层**（招聘经理真实需求 / Must Have / Nice to Have / Hidden Signals / Level 判断）。直接拿原始 JD 去算匹配度，是在跟「招聘话术」对齐，不是跟「招聘经理真实需求」对齐 — 这是 90% 求职工具最大的盲区。

**铁律二 · 不替用户编简历内容、不编公司情报。**
- Resume Tailor 只能**重新组织 / 突出 / 翻译**用户简历里已有的事实，不能凭空捏造成就、数字、职责。
- 公司文化、团队信号只能从 JD 文本 + 用户提供的信息推断；不要装作知道某公司内部情况。所有推断都标"我从 ___ 推断"。
- 报告 §1 公司背景 / §2 本职位产品分析 用到的公司画像、产品节点等若做了 web 调研，标明来源；查不到就标 `[需用户补充]`，**别编**。

**铁律三 · 数据没齐就不要硬出报告。**
JD 缺关键内容 / 用户没给简历或自述 → 先把缺的要齐，**别硬跑**。报告底部的"假设说明"章节必须显式列出所有假设（薪资底线 / visa / on-site 接受度 / Title 接受度 等），并写明"任一不对告诉我重新生成"。

---

## 内部流程（用户看不到，由 Step 3 调用）

| 流程 | 干什么 | Prompt 文件 |
|---|---|---|
| 1 · Decode | 5 图层拆解 JD 真实意图 | [prompts/jd-decoder.md](prompts/jd-decoder.md) |
| 2 · Match | 匹配度（0.6/0.2/0.2 加权）+ Must Have 逐条命中 + Gap 三档 | [prompts/match-score.md](prompts/match-score.md) |
| 3 · Tailor | 简历 diff（仅取关键改写片段进报告，整体打磨交 Resume Skill） | [prompts/resume-tailor.md](prompts/resume-tailor.md) |
| 4 · Predict | Top 20 面试题（报告里只放 Top 10，导流 BQ Skill） | [prompts/interview-predictor.md](prompts/interview-predictor.md) |
| 5 · Should I Apply | 五件套决策（⭐ / 值得投 / 不值得投 / 拿面概率 / 下一步） | [prompts/should-i-apply.md](prompts/should-i-apply.md) |

**这 5 条流程在 Step 3 里被调用一次，结果全部塞进同一份 HTML 报告。** 用户看不到"现在在跑流程 2"这种内部状态。

**如果用户明确只想要某一条流程**（"只解码不要别的" / "只算匹配度"）→ 跳过 Step 3 的报告生成，直接吐这一条流程的纯文本结果。这是**例外路径**，不是默认。

---

## JD Bank（情报沉淀）

- 位置：本 skill 目录下 `jd-bank/`，每份分析过的 JD 一个 `.md`。
- 文件名：`<公司缩写>-<岗位slug>-<YYYYMM>.md`，如 `openai-product-designer-202606.md`。
- frontmatter 必填：company / role / level / source_url / decoded_at / status（decoded / matched / tailored / applied / interview / closed）。
- [jd-bank/_index.md](jd-bank/_index.md) 是反查表：按公司、按岗位类型、按状态分组。**每次 Step 3 生成报告都要同步 `_index.md`**。
- 用户回头说"上次那个 ___"时，先查 index，别让用户重新粘 JD。

---

## 与 Resume Skill / BQ Skill 的衔接

这个 skill 不替代另外两个：

- **Resume Skill** 负责把一份简历做到「整体优秀 + 个人故事一致」。JD Skill 报告里的 Tailor diff 只做**针对单个 JD 的定向调整** — 告诉用户"要做整体优化去 Resume Skill"。
- **BQ Skill** 负责挖掘 / 结构化 / 沉淀故事库。JD Skill 报告 §9 只给"会被问什么" — 告诉用户"用 BQ Skill 把这些题挖成故事"。

三者形成的用户路径：

```
看到 Dream Job
   ↓
JD Skill：贴 JD → 给简历 → HTML 报告自动弹出
   ↓（决定投）
Resume Skill：整体简历打磨
   ↓（拿到面试）
BQ Skill：挖故事 / 模拟面试
   ↓
拿 Offer
```

---

## 参考文件（按需读取，别一次全加载）

**Prompts（5 条内部流程的执行脚本）**
- [prompts/jd-decoder.md](prompts/jd-decoder.md)
- [prompts/match-score.md](prompts/match-score.md)
- [prompts/resume-tailor.md](prompts/resume-tailor.md)
- [prompts/interview-predictor.md](prompts/interview-predictor.md)
- [prompts/should-i-apply.md](prompts/should-i-apply.md)

**Frameworks（知识词典 + 报告规格）**
- [frameworks/decode-patterns.md](frameworks/decode-patterns.md) — JD 话术翻译表 + Hidden Signal 词典
- [frameworks/match-rubric.md](frameworks/match-rubric.md) — 匹配度评分规则 + Gap 三档分类
- [frameworks/resume-tailoring.md](frameworks/resume-tailoring.md) — ATS / Recruiter / HM 三版改写法
- [frameworks/go-no-go.md](frameworks/go-no-go.md) — Should I Apply 打分法 + 拿面概率估算
- [frameworks/offer-strategy-report.md](frameworks/offer-strategy-report.md) — **最终 HTML 报告的 10 节骨架 + 视觉规范 + 生成说明（Step 3 的核心规范）**

**Examples**
- [examples/offer-strategy-template.html](examples/offer-strategy-template.html) — HTML 报告骨架（不含个人数据）

**JD Bank（情报库）**
- [jd-bank/_jd-template.md](jd-bank/_jd-template.md)
- [jd-bank/_index.md](jd-bank/_index.md)
