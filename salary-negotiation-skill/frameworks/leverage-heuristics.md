# Leverage Heuristics

判定 offer 每个组件的 leverage tier — **LOW / MEDIUM / HIGH** — 的规则手册。

在 [`../prompts/offer-diagnosis.md`](../prompts/offer-diagnosis.md) Step 3 逐项打标签时按这个查。

---

## 通用规则

**Leverage = 招聘官在这一项上有多少空间 × 你的推动力**

3 个维度联合决定：

| 维度 | 高 leverage | 低 leverage |
|---|---|---|
| **市场位置** | Offer 低于 P50 | Offer 高于 P75 |
| **你手中的替代** | 有书面 competing offer / 现职稳定 | 无 offer / 待业 3+ 月 |
| **招聘官内部约束** | 该组件不在硬 band 里 | 该组件是 policy 死数 |

**3 个都高 = HIGH。1 个高 2 个低 = MEDIUM 或 LOW（视组件而定）。全低 = LOW。**

---

## 逐组件 leverage 判定表

### Base Salary

| 场景 | Leverage | 说明 |
|---|---|---|
| 低于 P50 + 有 competing offer | HIGH | 招聘官知道自己低，且怕失去你 |
| 低于 P50 + 无 competing offer | MEDIUM | 数据在你这边但没杠杆 |
| P50-P75 + 有 competing offer | MEDIUM | 主要靠 competing offer 换空间 |
| P50-P75 + 无 competing offer | LOW-MED | 只能靠 justification 强推 |
| 大于 P75 | LOW | 已到 band 顶，硬推=消耗信用 |
| Level 已 down-graded | LOW | 招聘官会说 "you're already at top of the lower band" |
| Recruiter 明确说 "base is capped for this level" | LOW（立刻） | 别再 push base，pivot 到 RSU |

**特殊：Netflix / 某些 hedge fund** — base 是唯一 comp。此时"base low leverage"规则不适用，base 就是主战场。

---

### RSU (Equity)

| 场景 | Leverage | 说明 |
|---|---|---|
| 4-yr avg 低于 P50 | HIGH | 且大多数公司 RSU approver ≠ base approver，弹性大 |
| Base 已 capped + RSU 未到 P75 | HIGH | Recruiter 天然会想"我从 RSU 补" |
| 私营公司 + illiquidity discount 未 factor | MEDIUM | 你可以 argue "at 30% discount, effective TC is X" |
| 公司股价近期跌 30%+ | MEDIUM | Recruiter 会说 "we're being conservative" 但 approver 有时给"股数补偿" |
| Grant 已 include refresh commitment | LOW | 前置 refresh = 招聘官已经 pre-loaded 你的 TC 预期 |
| 大于 P75 | LOW | 硬推 = "reconsider pool" 风险 |

**特殊：Amazon** — RSU 极 back-loaded（5/15/40/40），Y1/Y2 sign-on 通常是主战场，RSU 本身谈判空间较小（Amazon 的 comp model 依赖 back-loaded stock）。

---

### Sign-on Bonus

| 场景 | Leverage | 说明 |
|---|---|---|
| Base + RSU 都在 band cap | HIGH | Sign-on 是最后一块 dumping ground，approver 通常低（recruiter 有 discretion） |
| 用户放弃 unvested equity（真的） | HIGH | 最强天然理由，几乎所有大厂 accept |
| Relocation 未 cover 全部 | MEDIUM | "relocation actual cost exceeds lump sum by $X" 好使 |
| 已经给过一次 sign-on | LOW | 二次 push = greedy signal |
| 公司政策不给 sign-on（罕见） | 零 | Netflix 等 |
| Clawback 24 个月 + 你不确定长留 | LOW（你自己的判断） | 别硬要，clawback = 锁 |

**特殊：中国大厂** — sign-on 概念弱，谈的是"签字奖"和"补前公司未 vested 期权"。

---

### Annual Bonus

| 场景 | Leverage | 说明 |
|---|---|---|
| Year 1 not guaranteed（default） | MEDIUM | "Guarantee Year 1 at target" 是标准要求，大厂通常 accept |
| Bonus target % 谈判 | LOW（几乎不） | Target % 挂 Level，不谈；除非同时 push Level |
| Sign 到中年（如 8 月）Y1 pro-rated | HIGH | "Pro-rated will disadvantage me, please guarantee 100%" 好使 |
| 从年度 target 20% 改成 30% | 零 | Level 挂钩，不谈 |

**别浪费谈判信用在 bonus % 上。** 除非 Year 1 not guaranteed，几乎不值得单独提。

---

## 特殊 leverage 类型（非现金）

### Refresh Commitment
- 招聘官承诺 "you'll be eligible for refresh grant at year 1, targeting X% of initial grant"
- **不能进 offer letter**（policy 不允许），但可以进邮件 confirm
- 招聘官很爱给这个 —— 花不到他的现金预算
- **报告应该建议**：Modality A/B 谈判中，如果 recruiter 拒了 base / RSU 加价，主动要 "written refresh commitment in email confirmation"

### Early Performance Review
- "6-month review instead of 12-month"
- 加速 promotion / merit increase 节奏
- Recruiter discretion 内，通常给
- **报告应该建议**：非 competing offer 情况下的 golden request

### Start Date Flexibility
- 早 start = 你自己让步
- 晚 start（3-4 周内）= 你的杠杆（recruiter Q3 KPI 压力）
- 晚 start（8+ 周）= recruiter 通常拒（headcount 会被 clawback）

### Interview Feedback Loop
- 少见但强：让 recruiter 分享 "onsite feedback quotes"
- 有些 recruiter 会给部分原话，你可以拿来 anchor："The panel loved my <specific area>, which is the exact skill this role needs — I think that value warrants closer to $X"
- **报告应该建议**：Modality A 谈判中的补充 justification

---

## 综合 verdict formula（Overall Leverage）

**每组件的 leverage tier 加权**：

- Base HIGH = 3, MED = 2, LOW = 1
- RSU HIGH = 3, MED = 2, LOW = 1
- Sign-on HIGH = 2, MED = 1.5, LOW = 1（权重稍低，因为它是补齐工具不是主战场）
- Bonus HIGH = 1, MED = 0.5, LOW = 0（几乎不影响 overall）

**总分**：
- **8+** → Overall HIGH → Modality A（双开激进）
- **6-7** → Overall MEDIUM → Modality B（单点集中）
- **4-5** → Overall LOW → Modality C（收尾轻抗）
- **3 or below** → Overall MINIMAL → Modality D（不谈，直接签）

**但**：**如果用户有书面 competing offer 且 competing offer TC 高 10%+**，总分 +2（自动升级至少一档）。

**但但**：**如果用户 待业 3+ 月 或 visa 60 天窗口**，总分 -2（自动降级至少一档，保守打）。
