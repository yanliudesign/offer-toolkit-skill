# Prompt · Offer Breakdown

**目的：** 把用户给的 offer 原文拆成结构化 comp 数据，算出 4-year TC 区间 + equity risk + stability 评级。是所有后续步骤的数据基础。

---

## Input

用户提供的 Offer A / Offer B 原文（可能是薪资邮件截图、公司发的 offer letter、或用户自己文字复述）。可能缺以下任一：

- Bonus target %
- RSU vest schedule（默认最常见的 25/25/25/25，standard cliff 1 年）
- Sign-on 是否分年发放
- 币种

**缺什么 → 一次追问一批**，别一条条问。缺得太多就用最常见假设 + 在 Assumptions 里显式声明。

---

## Output — 每份 offer 一份结构化 breakdown

```yaml
offer_id: A   # 或 B
company: "..."
role: "..."
level: "..."
location: "..."
currency: "USD"      # 币种
year_1:
  base:      { value: 210000, note: "base salary" }
  bonus:     { value: 42000, target_pct: 20, note: "20% target, paid in Q1 next year" }
  rsu:       { value: 100000, note: "$400k grant / 4 yr / 25% year 1 · no cliff" }
  sign_on:   { value: 50000, note: "one-time, clawback if leave in 12 mo" }
  total:     { low: 375000, high: 425000, note: "低到高假设 RSU 股价 ±15%" }
year_2:
  # 同上
year_3:
  # 同上
year_4:
  # 同上
four_year_tc:
  low: 1050000
  high: 1420000
  midpoint: 1235000
  note: "low = RSU 股价 -30% · no refresh · bonus 打 8 折 / high = RSU +30% · 每年 refresh 25k / bonus 打 1.2"

equity_risk: "medium-high"     # low / medium / medium-high / high
equity_risk_reason: "上市 5 年，股价 12mo -22%，refresh 政策不明"

stability: "medium"             # low / medium / high
stability_reason: "增长放缓，去年裁员 5%；但现金流健康"

comp_quality: "front-loaded"    # front-loaded / balanced / back-loaded / long-tail
comp_quality_reason: "Sign-on + Y1 RSU 占 4-yr TC 的 32% · Y3/Y4 会 cliff-drop（no refresh 假设下）"
```

---

## 拆解规则

### 1. Base
直接抄。跨币种 → 换到用户所在地本币（汇率写进 Assumptions）。

### 2. Bonus
- 有 target % → `base × target%`
- 只给"最近一年拿了多少" → 用那个数字 + 标注"用户报告的 actual，非 target"
- 没提 → 默认 0，Assumptions 里写"未提及 bonus，按 0 计算"

### 3. RSU

**关键：分清 total grant vs annual vest。**

| 用户说 | 拆解 |
|---|---|
| "$400k RSU / 4 yr" | annual vest = $100k/yr（假设 25/25/25/25，除非说了别的 schedule） |
| "$400k RSU / 4 yr · 5/15/40/40" | annual vest = 20k / 60k / 160k / 160k |
| "$100k/yr RSU" | 直接用 |
| 只给数字没给年数 | 追问，别猜 |

**RSU 价值计算**：默认用 offer 发出时的股价。上市公司股价用最近 30 天均价（如能查）。非上市公司标 `[非上市 · 按公司当前 409A 估值 / 上一轮 preferred price 计算，实际流动性受 tender / IPO 时机影响]`。

**RSU refresh 假设**：默认**不假设 refresh**（保守），如果用户说"HM 承诺 refresh"或"公司文化每年都发"则单独标注一个 `four_year_tc.high_with_refresh` 数字。

### 4. Sign-on
- 一次性 → 全部计入 Y1
- 分年发（如 "50k Y1 + 25k Y2"） → 按实际
- 有 clawback → 在 note 里标"clawback if leave in X months"

### 5. 4-year TC 区间

**下沿（low）**：
- RSU 股价 -30%
- Bonus 打 0.8
- No refresh
- 假设 Y2 起 no sign-on

**上沿（high）**：
- RSU 股价 +30%
- Bonus 打 1.2
- 假设有 refresh（如上市公司 tier）→ 每年 refresh = 初始 grant 的 25%

**Midpoint**：low + high / 2，作为「合理预期」值。

---

## Equity Risk 评级（4 档）

| 级别 | 判定 |
|---|---|
| **Low** | 大厂上市 · 股价 12mo 波动 <15% · 现金流健康（FAANG、微软、Adobe 这一档） |
| **Medium** | 上市中盘 · 股价波动 15-30% · 或未上市但估值稳定的 late-stage（Databricks、Stripe 这一档） |
| **Medium-High** | 上市但股价 12mo -20% 或更多 · 或 IPO 后 <3 年 · 或 late-stage 但最近一轮 down round |
| **High** | Early / mid-stage 未上市 · 或流血 IPO · 或最近裁员超 10% · 或 crypto/AI 泡沫敏感型 |

---

## Stability 评级（3 档）

| 级别 | 判定 |
|---|---|
| **High** | 上市 · 盈利 · 近 24 mo 无大规模裁员 · headcount 稳增 |
| **Medium** | 上市但盈利波动 / 或近 12 mo 有 <10% 裁员 / 或非上市但有 24+ mo runway |
| **Low** | 近 12 mo 裁员 >10% · 或非上市且 runway <18 mo · 或产品线大调整 · 或 CEO/关键 exec 最近换血 |

---

## Comp Quality 分类（4 档）

| 类型 | 特征 |
|---|---|
| **Front-loaded** | Y1 sign-on 大 + Y1 RSU 占比高（Amazon 5/15/40/40 反之，5/15 是 back-loaded 的经典例子） |
| **Back-loaded** | Y3/Y4 RSU 占比 >60%（典型如 Amazon 5/15/40/40）— 想拿全靠留够 4 年 |
| **Balanced** | 25/25/25/25 均匀 + 中等 sign-on |
| **Long-tail** | 强 refresh 文化（Google / Meta 传统）· 4 年后 TC 反而更高，"越干越值钱" |

---

## 不许做的事

- ❌ 编 bonus target（用户没给就标未提及）
- ❌ 编 refresh 假设（除非有明确来源）
- ❌ 单一数字（"4-year TC = $1.24M"）— 必须区间
- ❌ 跨币种时不换算就并排放
- ❌ 假装知道公司裁员 / 财报数据（要标 `[需用户核对]` 或引用来源）
