# Offer Bank Index

反查表：所有历史 offer 决策一览。每次 Step 3 生成报告都同步更新这里。

---

## 快速查询

按候选人 / 决策时间 / 结果快速找到历史决策。

| Slug | Company A × Role | Company B × Role | Level | Candidate | Decided | Recommendation | Status | Report |
|---|---|---|---|---|---|---|---|---|
| [anthropic-vs-linear-staff-pd-202607](./anthropic-vs-linear-staff-pd-202607.md) | Anthropic × Staff PD | Linear × Staff PD | Staff | General case | 2026-07-05 | 🏆 A (Anthropic) · ⭐⭐⭐ | `compared` | `~/Desktop/Claude skills/offer-compare-anthropic-vs-linear-staff-pd-202607.html` |
| [microsoft-stay-vs-linear-staff-pd-202607](./microsoft-stay-vs-linear-staff-pd-202607.md) | MSFT × Principal PD (stay) | Linear × Principal PD (leave) | Principal (parity, v2) | General + user priorities | 2026-07-05 | 🏆 B (Linear) · ⭐⭐⭐ · **v2 flipped from v1's A** | `compared` | `~/Desktop/Claude skills/offer-compare-microsoft-stay-vs-linear-staff-pd-202607.html` |
| [msft-vs-linear-vs-anthropic-pd-202607](./msft-vs-linear-vs-anthropic-pd-202607.md) | MSFT × Principal (stay) | Linear × Principal | Anthropic × Product Designer (~IC5?) · 3-way | General + user priorities | 2026-07-05 | 🏆 B (Linear) · 🥈 Anthropic · 🥉 MSFT · ⭐⭐⭐ | `compared` | `~/Desktop/Claude skills/offer-compare-msft-vs-linear-vs-anthropic-pd-202607.html` |

---

## 结果分类

### 🏆 推荐 A（走了 A）
- [Anthropic vs Linear · Staff PD · 2026-07 · General case](./anthropic-vs-linear-staff-pd-202607.md) — ⭐⭐⭐ · `compared`

### 🏆 推荐 B（走了 B）
- [MSFT (stay) vs Linear · Both Principal · 2026-07 v2 · user priorities](./microsoft-stay-vs-linear-staff-pd-202607.md) — ⭐⭐⭐ · `compared` · **v2 flipped from v1's A because Linear leveled up to Principal + user priorities favored craft/growth**
- [MSFT vs Linear vs Anthropic · 3-way Principal PD · 2026-07](./msft-vs-linear-vs-anthropic-pd-202607.md) — ⭐⭐⭐ · `compared` · **3-way: 🥇 Linear · 🥈 Anthropic · 🥉 MSFT** (Anthropic level ambiguous)

### 🚶 Walk-away（都拒了 / 回去谈）
_(待第一份决策生成)_

### ⏳ Undecided（对比过但用户还没决定）
_(待第一份决策生成)_

---

## Status 说明

| Status | 含义 |
|---|---|
| `compared` | 报告已生成，用户还没决定 |
| `decided` | 用户已决定接哪家（跟 recommendation 一致或不一致都算） |
| `accepted` | 已 verbal accept + 签 offer |
| `declined` | 已明确拒了两边 |
| `stale` | 决策超过 90 天，comp / 公司情况可能已变 |

---

## 复用逻辑

用户下次说 "上次那个 A vs B" / "帮我更新一下之前的对比" → 先查这个 index：
- 有 · <90 天 → 提示"上次决策记录：推荐 X，你选了 Y。要在原报告基础上加新信息重新生成吗？"
- 有 · >90 天 → 提示"上次是 XX 月的决策，comp / 公司情况可能已变，需要你重新提供最新 offer 数字"
- 没有 → 走完整 Step 1-3 流程
