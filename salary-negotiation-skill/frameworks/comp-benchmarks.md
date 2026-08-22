# Compensation Benchmarks

**这不是一份"comp 数据字典"** — 数据每季度都变，塞死数字是找死。这是一份**如何在 30 分钟内查到某个 role/level 真实 P50/P75**的方法。

**铁律：** 所有报告里的 comp 数字必须**能追溯到 5 个来源之一**，不能"我记得"。

---

## 5 个数据来源（按可信度排）

### 1 · Levels.fyi（首选）
- **URL**: `https://www.levels.fyi/companies/<company>/salaries/<role>`
- **筛选**：Location + Level + 时间窗口（选最近 12 个月）
- **可靠性**：高（大厂 IC 岗位，尤其 SWE / Design / PM）
- **弱点**：小公司 / niche role 样本少；某些公司（如私募 / hedge fund）数据缺
- **报告里怎么标**：`Levels.fyi P50 (Meta L5 Product Designer, SF Bay, 2025 Q1-Q2, n=42)`

### 2 · Blind（补充信号）
- **URL**: `https://www.teamblind.com`
- **用法**：搜"<公司> offer <level>" 看真人晒 offer 帖 —— 尤其看**评论区反驳**"你 lowball 了"这种，反映实际市场
- **可靠性**：中（匿名，可能夸张，但趋势方向可信）
- **弱点**：verified only visible if you have @company email，普通用户看不到 100% 数据
- **报告里怎么标**：`Blind post 2025-06, [Company] E5 offer discussion, n≈15 replies`

### 3 · 用户提供的 competing offer
- **可靠性**：最高（真实数据点）
- **用法**：如果用户手里有 Google $520K / Meta $500K，这是你最硬的 anchor
- **报告里怎么标**：`Competing offer: [Company] [Level] TC $X (user-provided, offer letter verified)`

### 4 · Glassdoor / Payscale（fallback）
- **可靠性**：低-中（老数据 + noise 大）
- **只在**其他来源都没有时用，且**必须标 [low-confidence]**
- **报告里怎么标**：`Glassdoor median (Company X, Role Y, US, low sample)`

### 5 · 行业代理数据
- 咨询公司 comp report：Robert Half / Radford / Croner
- 大多需付费订阅，找不到就跳过
- **不要用 Coursera / LinkedIn Salary Insights** — 数据太粗

---

## 快速对标法（30 分钟内出对标）

1. **确定 leveling equivalent**（跨公司 level 映射）：

| Meta | Google | Amazon | Apple | Microsoft | Netflix | 通俗对标 |
|---|---|---|---|---|---|---|
| E3 | L3 | L4 | ICT2 | 59 | — | New grad |
| E4 | L4 | L5 | ICT3 | 60 | — | Mid |
| E5 | L5 | L6 | ICT4 | 62 | Senior | Senior |
| E6 | L6 | L7 | ICT5 | 64 | — | Staff |
| E7 | L7 | L8 | ICT6 | 65 | Principal | Principal |
| E8 | L8 | L10 | — | 66 | — | Sr Principal |

**注意**：Amazon "SDE II = L5" 但对应 Meta E4 不是 E5（Amazon leveling 偏 inflated）。

2. **确定 comp 结构差异**：

| 公司 | Base 权重 | RSU 权重 | Bonus | Sign-on 惯例 |
|---|---|---|---|---|
| Meta | 高（top of market） | 高（4-yr, 25/25/25/25）| 15-20% | $50-150K senior 常见 |
| Google | 中-高 | 高（4-yr, 33/33/22/12 back-loaded 早期，现改 4/4/4/4）| 15-20% | $30-100K |
| Amazon | 中（低于 Meta base）| 极 back-loaded（5/15/40/40）| 0% | 巨额 sign-on 分 2 年，补 Y1/Y2 vest gap |
| Apple | 中 | 中 | 15% | $50-100K |
| Microsoft | 中 | 中 | 15-20% | $30-80K |
| Netflix | 极高 base | **可选 100% cash or 部分 stock** | 无 | 无 |
| Nvidia | 中 | 高（近期股价拉动 TC 巨大） | 15% | 有 |
| OpenAI/Anthropic | 高 | 高（PPU / RSU）| — | 高 |

**报告里必须注明**：Netflix 特殊（无 RSU 谈判空间，谈 base）；Amazon 特殊（sign-on 是主战场，因为 vest 后重）。

3. **地域调整**：

| 地区 | 相对 SF Bay 倍数 |
|---|---|
| SF Bay Area / NYC | 1.00 |
| Seattle | 0.95 |
| Boston / LA / DC | 0.90 |
| Austin / Denver | 0.85 |
| Remote (Tier 2 city) | 0.85-0.90 |
| Remote (Tier 3 city) | 0.75-0.85 |
| London | 0.75 (currency + tax) |
| Toronto | 0.65-0.75 |
| Bangalore | 0.35-0.45 |
| Beijing / Shanghai | 0.30-0.55（因公司而异） |

**报告里怎么用**：如果 Levels.fyi 只有 SF 数据，你 offer 在 Austin，把 P50 × 0.85 得到 "location-adjusted P50"。

---

## RSU 特殊问题

### Q: RSU 用什么股价折算？

Recruiter 报的 RSU 总额通常是 **grant-date 30-day trailing average**。你要问：
> "What's the reference share price used for the RSU dollar value?"

用这个数字除掉总额 = 股数，然后你可以**自己算最近现价折算**（可能已经涨或跌 20-30%）。

**报告里必须做的事**：
```
Recruiter 报 RSU total: $600K (at ref price $500)
= 1,200 shares
Current price ($540 as of 2025-XX-XX) = $648K equivalent
Δ = +8% latent upside
```

Or negative:
```
Ref price $500, current $420 = 1,200 × $420 = $504K equivalent
Δ = -16%
→ 谈判 leverage：可以说 "The grant is calculated at $500 ref, but at today's price the effective TC is $X — I'd like to see either a share count adjustment or a floor discussion."
```

**这一步是市面工具最少做的事，但对最终 TC 影响最大。**

### Q: 私营公司 RSU / PPU 怎么算？

OpenAI / Anthropic / Databricks / Stripe 类：
- 用最近一轮估值算，但打 **20-40% illiquidity discount**（因为无法立刻卖）
- 问 recruiter："What's the tender offer schedule?" —— 每年有没有回购窗口
- 如果无 tender，equity 视同 "long-lottery ticket"，谈 base 更重要

---

## 报告里数字如何呈现

**永远给区间，不给单点**：

❌ "P50 for Meta E5 Product Designer in SF is $220K base."
✅ "P50 for Meta E5 Product Designer in SF Bay is **$215K–$230K base** (Levels.fyi, n=42, 2025 H1)."

**永远标来源**：

❌ "Market range is $200-240K"
✅ "Market range is $200-240K (Levels.fyi 2025 H1, n=42) + $210-235K (Blind 2025 Q2 discussion, corroborating)"

**Never fabricate**。查不到就写：

```
Component: Base
Market P50: [insufficient data — recommend user check Levels.fyi <link>]
```

**这行看着 unprofessional，其实是** professional signal — 说明你不 bullshit。用户会 respect 这个。
