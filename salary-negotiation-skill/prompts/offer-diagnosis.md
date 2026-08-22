# Offer Diagnosis

**目标：** 把用户手里的 offer letter 拆成 4 个组件（Base / RSU / Sign-on / Bonus），逐个对标市场，每一项标 **LOW / MEDIUM / HIGH leverage**。后面 5 条流程都依赖这里的 leverage 标签。

**铁律**
- 一次只问一个缺失的数字。
- 所有 comp band / market data 必须能追溯到 Levels.fyi / Blind / 用户提供的其他 offer。查不到就写 `[需 Levels.fyi 上查一下]`，绝不瞎报。
- 数字全部给区间，不给单点。

---

## Step 0 · 先查库

读 `deal-bank/_index.md`：
- **同公司 + 同 Level + 3 个月内** → 直接调出之前的诊断作为对照，问用户"上次我给过这家的诊断，要不要用作 anchor？"
- **同公司不同 Level** → 复用公司的 comp band 判断，Level 换算即可。
- **没分析过** → 进 Step 1。

---

## Step 1 · 收齐 4 个组件

必要字段（缺任何一个都追问）：

| 字段 | 例子 | 备注 |
|---|---|---|
| Company | Meta | 用于查 Levels.fyi |
| Role | Senior Product Designer | |
| Level | IC5 / L5 / Senior | 公司内部 leveling |
| Location | Menlo Park, CA | 决定地域倍数（SF/NYC = 1.0，Austin = 0.9，Remote 视公司政策） |
| **Base** | $210,000 | 年薪 |
| **RSU total** | $600,000 | **总额**，非年化 |
| **RSU years** | 4 | 归属年限 |
| **RSU curve** | 25/25/25/25 or 10/20/30/40 or 4/4/4/4 monthly | 归属曲线（前重 / 平均 / 后重 差别巨大）|
| **RSU ref price** | $500 grant-date | 用什么股价折算的（决定 upside/downside） |
| **Sign-on** | $50,000 | 一次性；有的公司分 2 年发 |
| **Sign-on clawback** | 12/24 months | 提前离职要退还的窗口 |
| **Annual bonus target** | 15% | % of base |
| **Bonus guaranteed?** | Year 1 guaranteed / performance-based | 第一年是否保底 |
| **Refresh policy** | Annual refresh ~30% of initial grant | 有无年度补股（很多人忽略这条）|
| **Relocation** | $15k lump sum / not offered | |
| **Deadline** | Aug 15 | Recruiter 口头 vs 邮件写的 |

**没有 offer letter PDF 不算数**。让用户回 recruiter 要正式 offer letter。

---

## Step 2 · 计算 TC（Total Comp）Year 1 / 4-year Avg

**Year 1 TC** = Base + (RSU_total × Year1_pct) + Sign-on + (Base × Bonus_target)

**4-year avg TC** = Base + (RSU_total ÷ 4) + (Sign-on ÷ 4) + (Base × Bonus_target)

写清楚两个数，因为 recruiter 会说"你 Year 1 是 X"来 anchor，但真实长期是 4-year avg。

**RSU 曲线的陷阱**：
- 4/4/4/4 (monthly, evenly) → 平均分布，最公平
- 25/25/25/25 (annual) → 第一年 25% at year mark，前 11 个月没股
- 10/20/30/40 (back-loaded, Amazon) → **第一年只有 10%**，Year 2 之前必须靠 sign-on 补差；Year 3-4 才是大头，锁人 = 高
- 33/33/34 (3-year, Meta 有些 grant) → 短周期，refresh 依赖度更高

---

## Step 3 · 4 组件逐项诊断

对每一项输出以下 5 行：

```
━━ [组件名] ━━
Offer 数字：X
市场对标：P25 = A / P50 = B / P75 = C（来源：Levels.fyi <公司> <level> <location>，或标 [需查]）
位置判断：Below P50 / At P50 / At P75 / Above P75
Leverage：LOW / MEDIUM / HIGH（判定依据：见下方 heuristics）
诊断一句话：一句话说这项能不能谈 / 谈多少
```

### Base Salary

**Leverage heuristics：**
- **HIGH**：offer 低于 P50，或用户有同/更高 level 的竞争 offer → 招聘官"知道自己低了"
- **MEDIUM**：offer 在 P50-P75，或用户没有 competing offer 但公司急招（HC 老板催过）
- **LOW**：offer 已在 P75 以上（招聘官会说"这已经是我们的上限"），或 Level down-graded 谈不动

**大厂 base 大多有硬带 cap**（同 Level 的 base range 是死的），把力气花在 base 上性价比经常最低 —— **除非** 你在 band 底部。

### RSU (Equity)

**Leverage heuristics：**
- **HIGH**：RSU 明显低于 P50、Base 已在 cap、竞争 offer 有更高 equity → equity 是招聘官"最容易挪预算"的地方
- **MEDIUM**：offer 在 P50 附近，能加 15-30%
- **LOW**：offer 已在 P75、或公司股价近期跌了 recruiter 会说"我们保守 grant 价"

**RSU 是招聘官弹性最大的一项。** Base 卡带宽，RSU 通常有 approver 层级可以"go up a bracket"（+50-100K 总额是常见谈判空间）。

### Sign-on Bonus

**Leverage heuristics：**
- **HIGH**：RSU / Base 都到顶了、竞争 offer 有更高 sign-on、或用户要放弃未 vested 的股（"I'm walking away from $X on the table" 是最强 sign-on 理由）
- **MEDIUM**：正常谈，通常 10-30% 加空间
- **LOW**：已经给过 sign-on（"我们已经加过一次了"），或公司政策不给 sign-on

**Sign-on 是招聘官的"救急预算"，Base 加不了 / RSU 加不了 时的 dumping ground。** 但 clawback 24 个月的话，等于把跳槽窗口锁了两年。

### Annual Bonus

**Leverage heuristics：**
- **HIGH**（罕见）：只有在 Level 谈判连带 bonus target 时才有空间，或者要"Year 1 guaranteed bonus"（Amazon / MSFT 常见给）
- **MEDIUM**：Year 1 guaranteed 通常能要到，但公司政策不同
- **LOW**（最常见）：Bonus target 是 Level 挂钩的死数（IC5 = 15%，Staff = 20%），你不能谈 target %，只能谈"guaranteed vs performance-based"

**大多数情况 bonus 别浪费谈判信用，除非 Year 1 guarantee 缺失。**

---

## Step 4 · 输出 Diagnosis Card

汇总成一张 4 行 diagnostic card（这也是 HTML §1 会用的数据）：

| 组件 | Offer | Market P50 / P75 | Position | Leverage | 一句话 |
|---|---|---|---|---|---|
| Base | $210K | $220K / $240K | Below P50 | **HIGH** | Base 低于市场，是本次谈判第一优先 |
| RSU | $600K/4yr | $650K / $800K | Below P50 | **HIGH** | Equity 也在低位，主战场之一 |
| Sign-on | $50K | $30K–$75K | Median | MEDIUM | 有 15-30% 空间，作为补齐工具 |
| Bonus | 15% target | 15% (Level 挂钩) | Locked | LOW | 别浪费信用，除非 Year 1 not guaranteed |

**总 leverage 判断**（1 行 verdict）：
> **Overall Leverage: HIGH** — 3/4 组件低于市场 + 用户手持另一家同 Level offer → 招聘官有强烈动力 close 你。**建议激进打法**（要 base + RSU 双开）。

或：

> **Overall Leverage: LOW** — Base 已在 cap、无 competing offer、Level 已比对方内部同岗高一级 → 招聘官已经"为你破例"。**建议只小改一项**（sign-on 加 $20K），别 push 二次。

---

## Step 5 · 导流

诊断完毕，进下一步：

> "Offer 诊断完成。整体杠杆判定：**[HIGH/MED/LOW]**。
> 接下来我要出 **Leverage Map**（我方 vs 招聘官力量对比），然后才能定谈判排序。
> 一起继续，还是你想先看 diagnosis card？"

---

## 常见卡点

| 症状 | 处理 |
|---|---|
| 用户不知道 RSU 曲线 | 让他打开 offer letter PDF 搜 "vesting schedule" |
| 用户不知道 RSU 用什么股价折算 | 问 recruiter："What's the reference share price used for the RSU dollar value?" —— 这是标准问题，不敏感 |
| 用户 offer 里没有明确 Level | 追问 recruiter："What internal level / band is this position?" —— 有些公司刻意不写 |
| 竞争 offer 是"口头" | 标记为 [uncorroborated]，Leverage 只算 MEDIUM 而不是 HIGH。真实 leverage 需要 offer letter 才生效 |
| Levels.fyi 上数据太老 | 用最近 6 个月的记录；老数据（>1 年）在市场波动期不可信 |
| 公司太 niche Levels.fyi 无数据 | 用同规模同行业 proxy（"Anthropic 参考 OpenAI + 加 20% 溢价" 是市场共识，可用），并标 [proxy-based estimate] |
