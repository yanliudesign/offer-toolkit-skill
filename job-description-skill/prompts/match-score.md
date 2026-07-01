# Match Score — 流程 2

**目标：** 输出"用户简历 vs 这份 JD"的结构化匹配评估。固定四件套：匹配度 / 强项 / Gap / 风险。

**铁律**
- **必须先有 Decode 产出再算 Match。** 没解码就匹配 = 跟招聘话术对齐，不是跟真实需求对齐。如果库里没解码，先跑流程 1 极简版（至少出 Must Have + Hidden Signals）。
- 评分用 [../frameworks/match-rubric.md](../frameworks/match-rubric.md) 的规则，**不能拍脑袋打分**。
- 简历里没写的能力 = 不算。哪怕用户口头说"我会"，写到 Gap 里并标"简历未体现"。

---

## Step 1 · 收齐输入

1. **JD 的解码产出**（从 `jd-bank/` 调取，或现场跑流程 1）。
2. **用户简历全文**（PDF / 文本 / LinkedIn 截图都行，但要完整，不能是摘要）。
3. **用户目标 Level**（可选，影响打分基准）。

简历给得太短 / 只是 LinkedIn headline → 让用户补全工作经历，**别基于 100 字打 92% 的分**。

---

## Step 2 · 评分（用 Rubric，不拍脑袋）

完整方法见 [../frameworks/match-rubric.md](../frameworks/match-rubric.md)。简化算法：

1. **对 Decode 出来的每条 Must Have**，判断简历命中情况，三档打分：
   - ✅ 完全命中（简历有明确事实+量化）= 满分
   - 🟡 部分命中 / 相邻经验（能讲故事但不是直接对口）= 半分
   - ❌ 未命中 / 简历看不出来 = 0 分
2. **对每条 Nice to Have** 同样三档，但权重减半。
3. **Hidden Signal 命中度** 单独打一项分（用户气质 / 经历画像跟招聘经理找的人对不对得上）。
4. 加权汇总，**给区间不给单点**（例："75-82%"），并标"我按 ___ 权重算的"。

> ⚠️ 92% / 95% 这种高分慎给。**真实世界 80%+ 已经是强匹配**。给虚高分数是这类工具最大的可信度杀手。

---

## Step 3 · 四件套产出

### ① 匹配度

```
匹配度：78% （强匹配，但有 2 处需要注意的 Gap）
按权重：Must Have 60% + Nice to Have 20% + Hidden Signal 20%
```

加一句**定性描述**：是"直接对口型"/"相邻领域型"/"潜力型"还是"硬切赛道型"。

### ② 强项（Strengths）

3-5 条，每条**对齐到具体的 JD requirement**，引用简历里的事实做证据：

```
✅ AI 产品经验 — Must Have #1
   简历依据：2023 在 Microsoft 主导 Copilot for Teams 的设计，DAU 1M+
   信号强度：强（端到端 + 量化 + 大规模用户）
```

### ③ Gap（缺口）

分三档分类（参考 [../frameworks/match-rubric.md](../frameworks/match-rubric.md)）：

- **🔧 能补**（30 天内能弥补）：如某个工具 / 某个 cert / 某段经历可以重新讲述
- **⏳ 难补**（短期内补不上）：如 X 年某行业经验
- **🤷 不重要**（JD 写了但实际不卡）：如某个 nice-to-have

```
⚠️ Agent / Multi-step AI 经验 — Must Have #2
   档位：🔧 能补
   补法：把现有 Copilot 项目里"多步推理 UX"的部分单独拆出来重写

⚠️ Coding (HTML/CSS/JS) — Nice to Have #2
   档位：🤷 不重要
   理由：JD 标 Nice to Have，且该团队有专门的 design engineer
```

只列 3-5 条，**别为了凑数把不重要的也列上**。

### ④ 风险（招聘经理可能担心的画像问题）

这部分是市面上工具最少给的，也是最值钱的。从招聘经理视角看用户简历的"危险信号"：

- **背景跨度风险**：大厂 → 创业 / 行业切换 / Title 跨度
- **稳定性风险**：跳槽频率 / 短期 stint
- **Level 跨度风险**：目标 Level 比当前明显高/低
- **方向匹配风险**：过往做的方向跟 JD 不完全一致

每条要给：**风险描述 + 招聘经理大概率会怎么质疑 + 用户可以怎么回应**。

```
⚠️ 风险 1：大厂背景能不能适应早期 startup
招聘经理可能问：「Microsoft 这种成熟环境跟我们 40 人的团队差别很大，你怎么 ramp up？」
建议回应：准备 1 个"低资源 / 模糊环境下自驱"的故事
  → 可以用 BQ Skill 挖一个 Dealing with Ambiguity 类型的故事
```

---

## Step 4 · 沉淀 + 导流

1. 把 Match Score 结果**写回这份 JD 的文件**（更新 status: matched，加 match_score 字段）。
2. 主动问下一步：
   > "匹配度算完了。你想：
   > - 把简历**按这份 JD 改一版**（Resume Tailor）？
   > - 看看面试**会问什么**（Interview Predictor），重点准备 Gap / 风险对应的题？
   > - 还是先决定**值不值得投**（Should I Apply）？"

---

## 常见卡点

| 症状 | 处理 |
|---|---|
| 用户简历只给了 LinkedIn URL | 让用户粘贴 LinkedIn 全文或简历 PDF 文本，**不要根据 headline 估算** |
| 用户希望听到高分 | 客观打分。如果是低分，给"补法"而不是粉饰。低分但有路径 > 虚高分让用户裸投被拒 |
| Decode 还没做 | 先跑流程 1 的极简版（只出 Must Have + Hidden Signal）再来算 |
| 用户给的简历跟职位完全不沾边 | 直接说"这个匹配度太低（< 40%），可能不值得花精力 tailor，建议先看流程 5 决定要不要投" |
