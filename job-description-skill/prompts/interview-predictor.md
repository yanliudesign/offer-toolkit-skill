# Interview Predictor — 流程 4

**目标：** 基于 JD（已解码）输出 Top 20 道大概率会被问的题，分四类，每道题标"为什么会被问"。Behavior 类导流到 BQ Skill。

**铁律**
- 必须先有 Decode 产出。预测题目本质上是把 Must Have / Hidden Signal / 团队画像翻译成可能的提问。
- 不要装作知道某公司"实际面试题题库"。所有预测都说"基于 JD 推断 + 行业惯例"，不要造谣公司具体面试流程。
- 一次给完 20 道，分清楚类别和优先级，不要让用户面对一份平铺的题单。

---

## Step 1 · 收齐输入

1. **JD Decode 产出**（必需）。
2. **公司近期产品 / 业务方向**（可选）—— 用户知道就告诉，不知道就标"行业惯例推断"。
3. **用户对哪个环节最虚**（可选）—— 影响题目优先级排序。

---

## Step 2 · 按四类生成

每类 5 道左右，**每道题必须标来源**（对应 JD 哪条 / 哪个 Hidden Signal）。

### 类别 1 · Behavior（行为题）

由 Hidden Signals 和 Must Have 里的"软能力"推断。常见模板：

- Hidden Signal 含 `ambiguity` → "Tell me about a time you had to make a decision with incomplete information."
- Hidden Signal 含 `ownership` → "Tell me about a time you took ownership of something outside your role."
- Hidden Signal 含 `influence` → "Tell me about a time you influenced a decision without authority."
- Must Have 含 `stakeholder management` → "Walk me through a project with significant cross-functional friction."
- Must Have 含 `end-to-end` → "Tell me about a project you owned from 0 to ship."

每道题写成：

```
B1. "Tell me about a time you had to drive a decision with incomplete information."
  来源：Hidden Signal #2（ambiguity / unstructured）
  考察：Dealing with Ambiguity
  → 用 BQ Skill 找 / 挖一个 ambiguity 类故事
```

**Behavior 部分结尾统一一句**：
> "上面 5 道 Behavior 题，建议用 **BQ Skill** 挖故事或查故事库。如果还没有故事库，BQ Skill 可以从这几道题反向帮你挖故事。"

### 类别 2 · Product Thinking / Domain（专业题）

根据 JD 涉及的产品领域出题。Designer / PM 岗位常见：

- "How would you design [JD 里提到的产品场景]?"
- "Critique [该公司现有产品 / 同类产品] — what would you change?"
- "How would you measure success for [JD 里强调的功能 / 方向]?"
- "Walk us through a design process from research to ship."

设计师岗加 portfolio 题：

- "Pick your strongest case study and walk us through it."
- "Show us a project where you changed direction based on user feedback."

### 类别 3 · Technical / Craft（技能题）

根据 JD 列的硬技能出。比如：

- JD 提到 AI / LLM → "Walk me through how you'd design for hallucinations / model failure modes."
- JD 提到 enterprise / B2B → "How do you design for admin vs end-user personas?"
- JD 提到 0→1 → "How do you decide what to ship in v1 vs defer?"
- JD 提到 data-driven → "Tell me about a metric you defined and how it changed product decisions."

非设计岗（PM / Eng）换对应技能题。

### 类别 4 · Company-specific（针对该公司 / 团队）

3-5 道根据这家公司具体推断的题。例如：

- 公司在做 AI agent → "What's your point of view on the right UX for autonomous agents?"
- 公司是 startup → "Why startup over big tech? Why this size of company?"
- 公司是 mission-driven → "What about our mission resonates with you?"
- 用户从大厂跳过去 → "How will you adjust to a less structured environment?"
- 用户跨行业 → "Why this domain after [previous domain]?"

每道题标"基于 JD / 公司情况推断"，**不要装作内部消息**。

---

## Step 3 · 排个优先级

20 道题平铺信息量太大。最后给一个 **Top 5 必练**清单：

```
🎯 优先级最高的 5 道（按风险×概率排）：
1. B3 — 因为 Hidden Signal 反复出现 ambiguity
2. P2 — 因为是 JD 核心场景
3. C1 — 因为用户简历有大厂跳创业的画像风险
4. ...
```

排序依据：**出现概率 × 用户准备的薄弱度**。

---

## Step 4 · 沉淀 + 导流

1. **更新 JD 文件**：加 predicted_questions section，记录 20 道题。
2. **导流**：
   > "面试题预测完成 ✅。建议：
   > - Behavior 部分 → 去 **BQ Skill** 挖故事 / 模拟面试
   > - Product / Craft 部分 → 自己整理 talking points，重点准备 Top 5
   > - 想模拟面试 → BQ Skill 有轻量模拟流程
   > - 还想看其他职位 → 继续给我新 JD"

---

## 常见卡点

| 症状 | 处理 |
|---|---|
| 用户问"这家公司具体面试流程是什么" | 老实说：「我没有内部信息，建议查 Glassdoor / Blind / Levels.fyi / 联系前员工」 |
| JD 信息太少推不出 20 道 | 给能推出的（10-15 道）+ 1 个清单："剩下的题需要这些信息：① ② ③" |
| 用户希望具体答案 | 说"这里只出题，准备答案：Behavior 去 BQ Skill；Product 题建议自己准备 talking points（我不替你编案例）" |
| 用户面试已经很近 | 直接给 Top 5 必练 + 每道题的"准备方向"，跳过完整 20 道 |
