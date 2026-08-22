# Prompt · Dimension Compare

**目的：** 在 7 个维度上分别给 Offer A / Offer B 一个 0-10 打分 + 一句话解释 + 谁赢。这是报告的 §2。

---

## 输入

- 两份 offer 的 breakdown（来自 [offer-breakdown.md](offer-breakdown.md)）
- 用户的 priorities（如果有）
- 用户当前处境（visa / burnout / 家庭）
- 公司背景（能查就查，查不到标 `[需用户补充]`）

---

## 7 个维度（按顺序）

参考评分标准：[../frameworks/dimension-rubric.md](../frameworks/dimension-rubric.md)

### 1. 💰 Compensation Quality
**不只看 4-year TC 总额**，还看：
- 每年现金流健康度（base + bonus）
- Equity 组成风险（refresh 有无 / 股价假设）
- Sign-on clawback 期
- 相对当前 base 的涨幅

**输出模板：**
```
A: 8.5/10  — $1.2M mid-4yr TC · cash-heavy · low equity risk
B: 7.0/10  — $1.4M mid-4yr TC · 但 60% back-loaded 到 Y3/Y4 · 股价假设激进
🏆 A（Winner）— B 名义 TC 更高，但风险调整后 A 更实在
```

### 2. 📈 Career Growth
看：
- Role scope（IC / manager / staff+）
- Level 是否升级（当前 level → offer level）
- 团队规模 · 产品阶段（0→1 / 1→10 / 10→100）
- 未来 12-24 mo 能不能学到新东西 / 拓展新能力

### 3. 🤖 AI / Future Exposure
2026 年是 offer 决策里**最容易被低估**的一维。看：
- 是否在 AI native 团队 / 产品
- 公司整体 AI 战略强度
- 你的 role 会不会被 AI 反噬（如"运营 role"vs"AI product 设计"）
- 3 年后这份履历在 job market 上的可迁移性

**这一维必须给分，不许标 N/A。** 就算两家都不做 AI，也要判断"谁离 AI 更近"。

### 4. 🏢 Company Strength
看：
- 财务健康（营收 / 现金流 / 估值趋势）
- 产品市场地位（垄断 / 挑战者 / 长尾）
- 品牌在你 target industry 的认可度
- 24 mo 内被裁员 / 被收购 / IPO 的概率

### 5. 👤 Manager / Team Risk（可推断）
用户很少直接说，但**必须推断给分**（低置信度也要标）：
- 团队近期变动（HM 是新上任还是老臣？）
- 面试过程里 HM 的行为信号（决策快 / 追问深 / 尊重你的经历 = 加分；反复变面试轮次 / 招聘周期长 = 减分）
- Glassdoor 上该团队的评论（如能查）
- 公司整体文化健康度（review process 是不是 Amazon 式互撕？是不是 Netflix 式高绩效文化？）

如果完全没信号 → 给 5.0/10（neutral）+ 标 `[信号不足]`。

### 6. 🔁 Promotion Speed
看：
- 公司整体 promo 节奏（Google/Meta 从 senior 到 staff 通常 3-5 年 · Amazon 从 L6 到 L7 更快 · startup 完全看老板）
- 该 level 上下一级 headcount 是否有空位
- Team 是不是新组建（新团队更容易早期升）
- 该 level 是否已经在 "career level"（不需要 promo 就能稳定的 level，如 Google L5 / Meta E5 / Amazon L6）

### 7. 🌍 Location / Lifestyle
看：
- Location cost of living 调整后的净收入
- Commute / on-site 要求（hybrid vs full remote vs 5-day RTO）
- 与家庭 / 配偶职业的兼容
- Visa（H1B transfer / GC sponsorship / 是否 layoff 立刻走人的风险）
- 用户是否 burnout（当前公司 → 新公司 workload 增加？减少？）

---

## 输出格式（塞进报告 §2 的 JSON-ish 结构）

```yaml
dimensions:
  - name: "💰 Compensation Quality"
    a_score: 8.5
    a_note: "cash-heavy · low equity risk"
    b_score: 7.0
    b_note: "60% back-loaded to Y3/Y4"
    winner: "A"
    winner_note: "B 名义 TC 更高，但风险调整后 A 更实在"
    confidence: "high"    # high / medium / low

  - name: "📈 Career Growth"
    a_score: 7.0
    ...
```

**Confidence 标注规则：**
- `high` = 有明确数据支持（TC 数字、level 定义、公开公司数据）
- `medium` = 有部分间接信号（Glassdoor 评论、行业口碑）
- `low` = 主要靠推断（如 manager risk 没有面试信号）

---

## 加权总分（可选，报告顶部 gauge 用）

如果用户给了 priorities，按 priorities 加权：
- 用户 top 1 priority 那一维 → ×3
- 用户 top 2 → ×2
- 用户 top 3 → ×1.5
- 其余 → ×1

否则用默认权重（Balanced 模型）：
- Comp × 2 · Growth × 2 · AI × 1.5 · Company × 1.5 · Manager × 1 · Promo × 1 · Lifestyle × 1

计算：`A_total = sum(a_score × weight) / sum(weight)` → 0-10 → ×10 = 0-100

**Gauge 两条（A vs B），差距 >8 分 = 明确赢家 · 差距 3-8 = 有倾向 · 差距 <3 = 势均力敌（此时 §5 Recommendation 靠 tie-breaker 决定）。**

---

## 不许做的事

- ❌ 所有维度都 8/10（假中立）— 必须有真实差异
- ❌ 不给 winner（Tie 只在 <0.5 分差时允许）
- ❌ Manager Risk 标 N/A — 必须推断，就算低置信度
- ❌ AI 维度对非 AI 公司标 N/A — 必须判断"离 AI 多远"
