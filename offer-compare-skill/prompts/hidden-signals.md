# Prompt · Hidden Signals

**目的：** 除了明面上的 comp 和 dimensions，抽出 5 条"招聘话术不会告诉你但决策时最重要"的隐藏信号。这是报告的 §3，也是市面工具最缺的一环。

---

## 5 条固定信号（必须每条都判定，不许漏）

判定规则详见：[../frameworks/hidden-signals-dictionary.md](../frameworks/hidden-signals-dictionary.md)

### Signal 1 · 谁更 Front-loaded

**含义：** 拿钱拿在前面（Y1-Y2 权重高），后面 cliff-drop。

**判定：**
- Y1 comp / 4-yr avg > 1.2 → front-loaded
- Sign-on 占 4-yr TC > 8% → front-loaded 信号
- RSU vest 5/15/40/40 → 反而是 back-loaded 陷阱（Y1 只拿 5%）

**输出：** "Offer A 更 front-loaded — Y1 拿 $XYZ，占 4-yr TC 的 XX%。适合你如果……不适合如果……"

### Signal 2 · 谁有 Long-term Upside

**含义：** 4 年后越干越值钱（refresh 强 / 股价预期 / 公司增长曲线）。

**判定：**
- 强 refresh 文化（用户能确认 HM 承诺 或 公司公开政策）→ 强 long-term
- 上市股价 12mo +20%+ 且基本面健康 → 中 long-term
- Pre-IPO 且 IPO 概率高（24mo 内）→ 强 long-term（但高波动）
- 传统大厂 no-refresh + 股价 flat → 无 long-term

**输出：** "Offer B 有更明显 long-term upside — 因为 …… 但代价是 前 2 年 comp 少 XX%"

### Signal 3 · 谁更 Uncertain（不确定性）

**含义：** 数字之外的不确定性总和 — 团队新组建？产品 pivot？裁员传闻？RSU 股价波动？

**判定维度（每条 ±1）：**
- Equity risk = high 或 medium-high → +2
- Stability = low → +2
- Team 是新组建（<12 mo） → +1
- Product 在 pivot 或 major rewrite → +1
- Manager 是外部空降 <6 mo → +1
- 近 12 mo 有裁员 → +1
- Level 是"挑战性 level"（比当前高一级） → +1

总分 0-2 = Low uncertainty · 3-4 = Medium · 5+ = High

**输出：** "Offer A 不确定性更高 — 因为 A / B / C 三条信号叠加"

### Signal 4 · 谁更 Better for Resume（未来简历上写哪家更值钱）

**含义：** 5 年后如果又要跳槽，简历上写"曾在 X 做过 Y"哪家更帮你。

**判定：**
- 公司品牌 in target industry 的认可度（FAANG > tier2 · AI-native unicorn > 传统 mid-cap）
- Role 的稀缺性（"Head of AI Design at YC startup" > "Senior Designer at big co"）
- Product 的名气（做过 ChatGPT 界面 > 做过内部 admin tool）
- 该公司近期是否是 hot topic（media 关注度 = 简历 signal）
- 该职位是否会给你 title 升级（比如从 Senior → Staff）

**输出：** "Offer B 在简历上更值钱 — 5 年后你说'曾在 [公司 B] 做过 [产品/role]'比 A 强。原因：……"

### Signal 5 · 谁 Better for Switching Later（跳出去更容易）

**含义：** 3 年后想跳槽，哪家的经历让你更好卖。

**判定（跟 Signal 4 有相关但不完全一样）：**
- Tech stack / tool / methodology 是否有 market 迁移性（learn 一套 propriet 内部工具 vs 学一套 industry standard）
- 团队打过什么架（做过 0→1 vs 做过 optimization）
- Network（同事将来会在哪些公司）
- Recruiter 反向找你的频率（tier1 名字 = 更多 recruiter reach out）
- 是否会 pigeonhole 你（做太久 admin tool → 只能跳 admin tool 的坑）

**输出：** "Offer A 更 好跳出去 — 因为 A stack 通用性强、公司 network 广、不会 pigeonhole"

---

## 输出格式

```yaml
hidden_signals:
  - signal: "Front-loaded"
    winner: "A"
    verdict: "Offer A 明显 front-loaded — Y1 拿 $425k，占 4-yr TC 的 34%。"
    for: "你适合选 A 如果：短期资金压力大 / 对 3 年后跳槽持开放态度 / 不看好公司股价长期"
    against: "选 A 你要接受：Y3-Y4 comp cliff-drop 到 $270k 附近，除非 refresh 兑现"

  - signal: "Long-term Upside"
    winner: "B"
    ...

  # 共 5 条
```

---

## 不许做的事

- ❌ 只判 3 条 signal — 必须 5 条都判
- ❌ 说"两家都差不多" — 每条必须选出一个 winner
- ❌ 编 refresh 政策（用户没确认就假设 no refresh）
- ❌ 编"该公司在 industry 里很有名" — 要基于公开事实
