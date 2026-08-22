# Prompt · Recommendation

**目的：** 给一条**明确、有立场、不中性**的推荐。这是报告的 §5，也是整个 skill 的 payoff。

---

## 铁律：不许中性

用户拿两份 offer 来找你，**不是要看两列数字并排放**。必须给一条明确推荐：

- **推荐 A** — 明确、加粗、放 Verdict 头条
- **推荐 B** — 同上
- **都拒，回去谈** — 有时候两份都不值得接（例外，但必须敢说）
- **模糊态** — 只在极罕见情况下允许（如两份 comp 差距 <5%、7 维打分差距 <0.5 分、用户 priorities 完全无差异）— 此时必须显式说明"这份决策 tie-breaker 是 lifestyle 因素，需要用户自己判断"

**永远不允许的措辞：**
- ❌ "两家都不错，看你自己选"
- ❌ "取决于你的 priorities"（如果用户已经给了 priorities，你就必须根据 priorities 出结论）
- ❌ "都各有各的好"

---

## 输出结构（必填 4 块）

### Block 1 · 主推荐（一句话 + 3-5 条支撑）

```markdown
## 🎯 我的推荐：**接 Offer B**

三条支撑：

1. **4-yr TC 风险调整后 B 净胜 12%** — A 名义高但 55% RSU + 无 refresh · B 的 cash+bonus 占 62% 稳。
2. **AI Exposure B 明显更强** — B 是 AI-native product / A 是传统 SaaS。3 年后简历上 B 的稀缺性 >> A。
3. **你的 priority #1 是 growth（你自己说的）**，B scope 是 Staff IC + Design Lead，A 是 Senior 平推。

保留意见：
- B 的 uncertainty 更高（team 6 个月新组建），前 6 个月你要接受"边建边跑"的节奏。
- 如果你 P0 是 stability 或家庭需要稳定 → 反过来推 A。
```

### Block 2 · Tradeoff 展开

不许粉饰 — 选 B 意味着放弃什么：

```markdown
## 你选 B 要放弃什么

- **Y1 现金流下降 $18k**（B base -12k, sign-on -6k vs A）— 如果你有房贷压力这不小
- **通勤 4 天/周 on-site**（A 是 hybrid 2 天）— 家里娃学校在 A 那边更近
- **Team ownership 上 A 更清晰** — B 你是 lead，也就是"什么烂摊子都得你收"
```

### Block 3 · "If you are X → A / If you are Y → B" 分叉判定（必填）

这是 skill 的核心 defense mechanism — 就算主推荐错了，用户能在这里找到自己：

```markdown
## 换个角度：如果你是……

> **如果你是 "钱到位、家庭稳定优先" 型** → 反过来选 **A**
>   理由：A 现金流稳、通勤友好、equity risk 低、Y1 净收入实际高。B 的 upside 是 3 年后才兑现，而你现在需要的是"每月稳定进账"。

> **如果你是 "3 年内跳槽 / 想蹭 AI 履历" 型** → 选 **B**
>   理由：B 简历 signal 强、AI 敞口高、team new = 更容易早期升。3 年后你带 B 履历去 tier1 AI 公司比带 A 好谈。

> **如果你是 "burnout 中、需要恢复" 型** → **两家都不接**
>   理由：A 虽然 lifestyle 好但 role 是平推（学不到东西 → 更 burnout） · B workload 会更重。建议你先接 A（因为通勤友好），同时低调看 3 个月，用现在这个 offer window 谈更好的下一份。
```

**规则：**
- 至少 2 条分叉（"选 A 类"、"选 B 类"）
- 允许第 3 条 "都不接" 或 "先接 A 边找" 的 hybrid path
- 分叉的判定条件必须**具体**（"钱到位、家庭稳定优先"，而不是"如果你比较保守"）

### Block 4 · Next 72 hours action

不要抽象 — 具体到"接下来 3 天做什么"：

```markdown
## 接下来 72 小时

1. **回 B recruiter：** 表明高意向 + 提出 3 点 negotiation：
   - Base +$8k
   - Sign-on +$15k（补偿放弃 A 的机会成本）
   - 书面 refresh policy 或 minimum stock refresh guarantee
2. **回 A recruiter：** "非常认真考虑，本周五前会给答复" — 保留谈判筹码
3. **给 B 的 HM 发一句消息：** "接受前想再聊 20 分钟对齐 first 90-day goals" — 一是验证 role scope 是不是 JD 上写的那样，二是看 HM 的反应（爽快聊 = 好信号；推脱 = 红旗）
4. **周五前：** 拿到 B 的谈判结果 · 决定 · 通知两边
```

---

## Verdict 一句话（塞进报告顶部 Verdict block）

```
"接 Offer B。TC 名义 -5% 但 AI exposure、Staff scope、resume signal 三项碾压 A。
主要风险：team 新组建 · Y1 现金流 -18k。你能接受就上。"
```

⭐ 推荐指数（0-5）— 决心多强：
- 5 ⭐ = "闭眼上，别 second guess"
- 4 ⭐ = "强推，但有 1 条 caveat"
- 3 ⭐ = "倾向 X，但另一条也说得通"
- 2 ⭐ = "只是稍微倾向"
- 1 ⭐ = "tie-breaker 决定，可能两家都不理想"

---

## 不许做的事

- ❌ Verdict 里出现"看你自己"
- ❌ 主推荐里三条支撑其中有一条是"两家都类似"
- ❌ Tradeoff 只说好话
- ❌ 分叉判定条件模糊（"如果你更看重成长"这种废话）
- ❌ Next 72 hours 抽象（"跟 recruiter 沟通"）— 必须具体动作
- ❌ 因为用户没给 priorities 就中性化（→ 走 Balanced 默认权重 + 在 Assumptions 里显式说"用户未给 priorities，按 Balanced 权重给出推荐"）
