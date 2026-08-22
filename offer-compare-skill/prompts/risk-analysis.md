# Prompt · Risk Analysis

**目的：** 为每份 offer 显式列 4-6 条 risk，按严重度分级，附"如何 mitigate"或"接受这个 risk 意味着什么"。这是报告的 §4。

---

## 5 大类 risk（每类都必须扫一遍）

分类词典详见：[../frameworks/risk-taxonomy.md](../frameworks/risk-taxonomy.md)

### 1. Equity Risk（股权 / 现金 相关）
- RSU 股价大幅下跌
- Refresh 政策不清 / 承诺口头未落纸
- 期权行权价高于公允价值
- Cliff（1 年内离职 sign-on 要退）
- Vest schedule 陷阱（5/15/40/40 back-loaded）

### 2. Role Risk（岗位真实性 相关）
- JD 写的是 Y，实际做的是 X（面试时问不出来）
- Scope shrink（说 head of X，进去发现只是 individual contributor）
- Reorg 后 role 消失
- Manager 期望和你能力错配
- 该 role 前任是被裁的（先问一句"这个坑上一个人为什么走"）

### 3. Team / Manager Risk
- 新组建团队缺 support（缺 design ops / 缺 PM / 缺 eng bandwidth）
- Manager 空降 <6 mo（自己都在找立足点，帮不上你）
- 团队近期有 attrition wave（同期入职 5 人半年内走 3 人）
- Skip-level 不稳定（VP 快离职）
- Culture toxic（Blind / Glassdoor 有一致投诉）

### 4. Market / Company Risk
- 公司近 12 mo 裁员 >10% 且传言未止
- 产品线可能被砍（该产品 revenue contribution 低 & 有 EOL 传闻）
- 竞品挤压严重（market share -X% YoY）
- Runway <18 mo（早期公司）
- 被收购风险（大公司收 → 你 role 可能被合并掉）

### 5. Life / Personal Risk
- Visa 依赖（H1B transfer 万一被裁 60 天窗口）
- Relocation 成本 / 家庭破坏
- Commute / RTO 政策变化风险
- Burnout 继续加剧（新公司 workload 更重）
- Comp cut vs 当前包（比当前 base 低 → 影响长期薪酬曲线）

---

## 输出格式（每份 offer 一份）

```yaml
offer_A_risks:
  - name: "RSU 股价下行 30%"
    category: "Equity"
    severity: "high"     # high / medium / low
    reason: "上市 5 年 · 股价 12mo -22% · 无 refresh 承诺 · 用户 4-yr TC 的 55% 来自 RSU"
    if_realized: "4-yr TC 从 mid $1.24M 掉到 low $1.05M，Y3-Y4 打八折"
    mitigation: "谈判争取: (a) sign-on 加 25k (b) 明确书面 refresh 政策 (c) 争取 stock refresh minimum guarantee"

  - name: "新组建团队 · Manager 空降 4 mo"
    category: "Team"
    severity: "medium"
    reason: "面试第 3 轮提到 team 刚组建 · HM 是从 Google 挖来的 · 你的 skip-level 上任才 6 个月"
    if_realized: "前 12 mo 大量时间用于建 process 而非交付 · promo timeline 拖长 6 mo+"
    mitigation: "onboarding 前 30 天主动跟 HM 对齐 Q1 top-3 priorities · 争取给自己 6mo goal 而非 3mo"

  # 共 4-6 条
```

**严重度分级：**
- **High** — 概率 >30% 且 outcome 会实质影响你在这家干下去的决定
- **Medium** — 概率 10-30% 或 outcome 可通过 mitigation 显著降低
- **Low** — 概率 <10% 但值得知晓（"你决定接了应该心里有数"）

---

## 覆盖度 checklist

生成 risks 之前跑一遍：

- [ ] 5 大类每类**至少扫过**（不代表每类都出 risk，但每类都要在你脑子里跑一遍）
- [ ] Offer A 出 4-6 条 · Offer B 出 4-6 条（对等）
- [ ] 每份 offer 至少 1 条 high severity（除非真的没有 — 那也要显式说"未发现 high risk"）
- [ ] 每条 risk 都有 mitigation 或"接受它意味着什么"（不能只列 risk 不给出路）

---

## 不许做的事

- ❌ 只列一份 offer 的 risk（必须两份都列）
- ❌ 所有 risk 都 medium（真中立不存在，敢排 high / low）
- ❌ 只列 risk 不给 mitigation
- ❌ Personal risk 装作看不见（visa / 家庭 / burnout 只要用户提到就必须进这一节）
- ❌ 编"该公司近期传闻要裁员"— 除非有公开新闻，否则标 `[基于用户报告 / 未验证]`
