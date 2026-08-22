# Leverage Map

**目标：** 在 Offer Diagnosis 之后，画一张明确的**权力图** — 我有什么牌 / 招聘官有什么牌 / 双方各自的弱点。谈判是权力的博弈，不是"礼貌请求"。

**铁律**
- 每一条 leverage 都要写清"这为什么算 leverage"（招聘官会因为它做出什么决定）。
- 弱点部分不许温柔，弱点不敢承认 = 谈判中被打死。
- 用户情绪化时（"我怕失去 offer"），把"怕"翻译成"你实际的 BATNA 是什么"。

---

## Step 1 · 用户的 Leverage（我的牌）

对下面 8 项逐条打分（有 / 无 / 待验证），每条对应一个 leverage 增益：

| # | 项目 | 有没有 | leverage 增益 |
|---|---|---|---|
| 1 | **Competing offer（书面）** | 是 / 否 / 口头 | 最强杠杆。书面 = +20% ask 空间 |
| 2 | **Competing offer（in-process，已到 onsite/final round）** | 是 / 否 | 中等杠杆。可用作 "timeline pressure" 但招聘官会怀疑 |
| 3 | **Current comp 高**（当前包不比 offer 差多少） | 是 / 否 | 强杠杆。"我为什么要跳？" 是最有力的沉默 |
| 4 | **Non-fungible skills**（这家公司团队没有的能力/背景） | 是 / 否 | 中等。特别是 AI / 特定 domain expert / 特定行业经验 |
| 5 | **Personal referral / warm intro from hiring manager** | 是 / 否 | 弱-中等。HM 已经 emotionally invested |
| 6 | **JD 里的 "must have" 全命中**（你就是他们要的那个人） | 是 / 否 | 中等。招聘官已在预算书里 justify 过你 |
| 7 | **Public visibility**（作品被业界引用 / 大厂案例主角 / GitHub 明星） | 是 / 否 | 弱-中等。让 recruiter 不敢让你 walk |
| 8 | **Time**（deadline 是他们急，不是我急） | 是 / 否 | 强杠杆。招聘官有招聘季度 KPI |

**输出格式**：只列**有**的那几项，每条 1 行说明"这为什么让招聘官加钱"。**别列没有的**（那是弱点部分的事）。

例：
```
✅ 你手里有 Google L5 书面 offer（TC $520K）— 招聘官必须匹配到接近这个数才能 close，否则你 walk 掉他损失一整轮招聘周期
✅ Q3 season end 8 月 30 日是他们的 quota deadline — 你现在按住不签他就交不了差
✅ JD 里 4 个 must have 你全命中（AI + 0-1 + IC5+ + IPO 期 startup 经历）— HM 已经在预算书里为你破了一级 band，撤回成本高
```

---

## Step 2 · 招聘官的 Leverage（他的牌）

同样逐条：

| # | 项目 | 有没有 | leverage 说明 |
|---|---|---|---|
| 1 | **你没有其他 offer** | 是 / 否 | 你的 BATNA = 现职（如果你还在职）or 待业（如果失业） |
| 2 | **你已经辞了现职 / 待业超过 3 个月** | 是 / 否 | 你的 leverage 直接归零，招聘官闻得出 |
| 3 | **你签了 down-level（比现职低 / 比预期低）** | 是 / 否 | 说明你自己也承认 "market doesn't value me at previous level" |
| 4 | **你的 visa / 身份依赖 offer** | 是 / 否 | 招聘官会 gently 提醒："我们可以帮你 sponsor…" |
| 5 | **你的 timeline 比他紧**（比如现职最后一天倒数） | 是 / 否 | 招聘官会等你自己 blink |
| 6 | **他有 backup 候选人在 finalist stage** | 是 / 否 | 他会说 "we may need to reconsider the pool" |
| 7 | **公司近期裁员 / hiring freeze rumor** | 是 / 否 | Recruiter 会说 "we're being conservative this cycle" |
| 8 | **Offer 已经"破例"过一次**（如 up-level / relocation exception） | 是 / 否 | 每次破例都消耗招聘官在内部 approver 那的信用 |

**输出格式**：只列**他有**的那几项。

例：
```
⚠️ 你 60 天内会失去现职（H1B 60-day grace period）— 招聘官知道，可能会用 "we can move fast on paperwork if you sign this week"
⚠️ 你在 offer 讨论里已经透露过 "salary is not my #1 concern" — 他会记下来
⚠️ 他手里有 2 号候选人在 offer stage — 但这条通常是 bluff（下方 counter-simulation 会拆解）
```

---

## Step 3 · 三个弱点（我的 blind spots）

**用户经常不敢承认的弱点，你要点出来。** 每条给一个 mitigation。

常见弱点：

1. **单一 offer**（"我只有这一份")
   → Mitigation：**永远不告诉 recruiter 你只有这一份**。你可以说 "I'm evaluating a couple of things, but this is my top choice." — 真话（因为 "a couple of things" 包括"继续现职"和"其他面试")

2. **心里价位偏低**（"能达到 X 我就签")
   → Mitigation：**你的心理价位对招聘官保密**。任何时候被问 "what number would make you sign?"，答 "I'm looking at overall competitive package, let's discuss the components." 永远不给单点数字。

3. **已经在情绪上"想要"这份 offer**（爱上这家公司了）
   → Mitigation：**招聘官闻得出兴奋**。你可以真心喜欢这份 offer，但 tone 保持 professional interested，别 gush。想清楚 walk-away line（见 §6 final recommendation）。

4. **透露过 current comp**（recruiter 阶段说了当前包）
   → Mitigation：现在很多州立法禁止问 current comp（CA, NY, WA, MA…）。如果你之前告诉过，现在你可以说 "since our initial conversation, I've been looking at total comp more holistically" 来 reset anchor。

5. **Level 已被 down-graded**（原来面 Staff 结果 offer 是 Senior）
   → Mitigation：**明确 push back on level 前 push comp**。谈判信用一次只花一处。除非 down-level 的 comp 差距 > 20%，否则先接受 level、把 comp 谈起来，进公司后靠 promotion 追。

6. **Visa 依赖**
   → Mitigation：不隐瞒，但也不主动提。谈判时把它拿出来当 "additional cost of change"："I'm currently on H1B, and switching involves…" — 变成对方需要 accommodate 的东西，而不是你需要 apologize 的东西。

**每份诊断挑最相关的 2-3 个写。**

---

## Step 4 · Power Balance Verdict

一句话总结整个 leverage map：

**格式**：
> **[YOU] have [HIGH/MED/LOW] leverage; [RECRUITER] has [HIGH/MED/LOW] leverage. Net: [YOU] can push [aggressively / moderately / minimally].**

例：
> **你有 HIGH leverage（书面竞争 offer + Q3 deadline + 你就是 HM 要的人）；招聘官有 LOW-MED leverage（唯一 counter 是 timeline pressure）。Net：可以激进 push，双开 base + RSU，target 加 15-25% TC。**

例：
> **你有 LOW leverage（无 competing offer + 待业 4 个月 + 心理价位已透露）；招聘官有 HIGH leverage（他能 walk 你不敢）。Net：只小改一项（sign-on 加 $15-25K），别开双线，保住 offer 是首要目标。**

---

## Step 5 · 导流

> "Leverage Map 完成。Power Balance: **[verdict]**。
> 下一步定 **谈判排序 + 每项的 ask 区间**。走。"
