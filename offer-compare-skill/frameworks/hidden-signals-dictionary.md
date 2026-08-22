# Hidden Signals Dictionary · 隐藏信号判定词典

配合 [../prompts/hidden-signals.md](../prompts/hidden-signals.md) 使用。5 条固定信号 · 每条必判 winner。

---

## Signal 1 · Front-loaded

**问题：** 谁把钱主要放在了前面？

**触发词典：**

| 特征 | Front-loaded 信号强度 |
|---|---|
| Sign-on 占 4-yr TC > 8% | ★★★ |
| RSU vest 25/25/25/25 + no cliff | ★★（相对 back-loaded 已经算 front） |
| Amazon 5/15/40/40 | ★★★（back-loaded 反向信号） |
| Google 25/25/25/25 + refresh | ★☆（front but 有 long tail） |
| Y1 TC / 4-yr avg > 1.20 | ★★★ |
| Y1 TC / 4-yr avg < 0.85 | ★☆（back-loaded 反向） |
| Bonus 有 sign-on bonus（Y1 一次性） | ★★ |
| Startup 大量 option 但 vest cliff 1 年 | ★☆（front-loaded 的现金部分，equity 反向） |

**判定 output 模板：**
> "Offer A 更 front-loaded — Y1 拿 $X，占 4-yr TC 的 XX%。适合你如果：短期现金压力大 / 对 3 年后跳槽持开放。要接受：Y3-Y4 comp cliff-drop 到 $X 附近（除非 refresh 兑现）。"

---

## Signal 2 · Long-term Upside

**问题：** 谁 4 年之后越干越值钱？

**触发词典：**

| 特征 | Long-term upside 强度 |
|---|---|
| 强 refresh 文化（Google / Meta 传统） | ★★★ |
| HM 明确书面承诺 annual refresh minimum | ★★★ |
| 上市公司股价 12mo +30%+ 且基本面健康 | ★★ |
| Pre-IPO late-stage 且 IPO 预期 24mo 内 | ★★★（高波动） |
| Traditional 大厂 no-refresh + 股价 flat | ✗（无 upside） |
| Amazon 4-yr vest 无 refresh 承诺 | ✗ |
| Early startup（option 有 10x upside 但 90% 概率归零） | ★★★（期望值中等，方差极大） |
| Product 处于 hyper-growth 阶段（AI 类目 2024-2026） | ★★（间接：股价随成长走） |

**判定 output 模板：**
> "Offer B 有更明显 long-term upside — 因为 X + Y。代价：前 2 年 comp 少 $Z（vs A）。适合你如果：你相信 [公司 / 行业] 的 3-5 年前景，且现金流没压力。"

---

## Signal 3 · Uncertainty（不确定性）

**问题：** 除了 comp 数字，还有多少"我不知道会发生什么"？

**打分表（每条 +1）：**

| 信号 | 分 |
|---|---|
| Equity risk = high 或 medium-high | +2 |
| Stability = low | +2 |
| Team <12 mo 新组建 | +1 |
| Product 在 pivot 或 major rewrite | +1 |
| Manager 空降 <6 mo | +1 |
| 近 12 mo 有 >5% 裁员 | +1 |
| Level 是挑战性 level（比当前 +1） | +1 |
| Skip-level 快离职 / VP 换血 | +1 |
| 面试轮次异常（8+ 轮或反复延期） | +1 |
| 未上市 & runway 未披露 | +1 |

**总分档：**
- 0-2 = Low uncertainty · 3-4 = Medium · 5+ = High

**判定 output 模板：**
> "Offer A 不确定性更高（评分 6/10）— 主要 3 条信号：X / Y / Z。这意味着：进去前 6 个月你要接受'边建边跑'，不是 well-oiled machine。你不适合选 A 如果：你正处 burnout / 家庭需要稳定 / 短期需要靠 job title 说话。"

---

## Signal 4 · Better for Resume（简历上更值钱）

**问题：** 5 年后如果又要跳槽，"曾在这里做过 X" 哪家更帮你？

**触发词典：**

| 特征 | Resume value |
|---|---|
| FAANG / Big Tech 品牌 | ★★★ |
| Hot unicorn（OpenAI / Anthropic / Stripe / Databricks / Cursor 这档） | ★★★ |
| Tier1 AI startup 且做 core product | ★★★ |
| Fortune 500 但 non-tech | ★★（industry 内值钱 · industry 外一般） |
| Late-stage 但产品无名（"C 轮 SaaS"） | ★ |
| Early startup 但你是 founding member / staff+ | ★★（叙事强） |
| 你的 role 直接做 hot topic 产品（ChatGPT UI / 大模型 infra） | +1 加分 |
| 你的 role 是 admin tool / internal only（不能拿出去 show） | -1 减分 |
| Title 升级（Senior → Staff · Director → VP） | +1 加分 |
| 该公司近期是 media 焦点（正面 or 负面 皆算 signal） | +1 加分 |

**判定 output 模板：**
> "Offer B 在简历上更值钱 — 5 年后你说'曾在 [公司 B] 做过 [role / product]' > A。因为：公司 B 在 AI 圈的品牌 + 你 role 是 core product 一线（不是内部工具）+ title 会升到 Staff。"

---

## Signal 5 · Better for Switching Later（跳出去更容易）

**问题：** 3 年后想跳槽，哪家的经历让你更好卖？

**触发词典：**

| 特征 | Switch-out value |
|---|---|
| Tech stack / methodology 是 industry standard（React · Figma · SwiftUI · standard AB test） | ★★★ |
| 内部专有工具 / 方法（"公司内部一套自研 design system 你花 1 年才学会"） | ★（pigeonhole 风险） |
| 团队打过什么架 = 0→1 产品 / M&A / 大 refactor | ★★★（叙事丰富） |
| 团队只做 maintenance / small A/B tests | ★（叙事贫瘠） |
| 同事 network 广（人跑到各种公司） | ★★★（互相 refer） |
| 同事都是 lifer（20 年在同一家） | ★（network 局限） |
| Recruiter 反向找频率高（该公司 alumni 常被 headhunt） | ★★★ |
| Domain 稀缺（AI / infra / trust safety / creator tools） | ★★★ |
| Domain 饱和（general SaaS 前端） | ★ |

**判定 output 模板：**
> "Offer A 更 好跳出去 — stack 通用（React + Figma + standard tools）· team 打过 0→1 · 该公司 alumni 分散在各 tier1（recruiter 会主动来）· 不会 pigeonhole。B 会给你 pigeonhole risk（做太久内部工具 → 只能跳同类坑）。"

---

## 输出汇总模板（塞进报告 §3）

5 条 signal 用 卡片式 呈现（HTML 里对应 `.signal-card`）：

```
┌─────────────────────────────────────┐
│ Signal 1 · Front-loaded             │
│ 🏆 Winner: A                        │
│ Verdict: A 明显 front-loaded ...    │
│ For you if: 短期资金压力大 ...       │
│ Against: 要接受 Y3-Y4 cliff-drop ... │
└─────────────────────────────────────┘
```

**每条必须给 winner，不允许 tie。** 如果实在极势均，选一个"稍微更接近"的并标 confidence = low。
