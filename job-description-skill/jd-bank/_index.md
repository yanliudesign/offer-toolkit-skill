# JD Bank · Index

每份分析过的 JD 的反查表。**每次新增 / 更新 JD 文件，必须同步更新这里。**

文件命名规则：`<company-slug>-<role-slug>-<YYYYMM>.md`
例：`openai-product-designer-202606.md`

---

## 按状态汇总

| Status | 含义 |
|---|---|
| `decoded` | 仅做了 JD 解码 |
| `matched` | 跑了 Match Score |
| `tailored` | 简历已 tailor |
| `applied` | 已投递 |
| `interview` | 在面试流程中 |
| `offer` | 拿到 offer |
| `closed` | 决定不投 / reject / 关闭 |

---

## All JDs（按状态分组）

### 🔍 Decoded（已解码，未决定）

| 文件 | 公司 | 岗位 | Level | 解码日期 |
|---|---|---|---|---|
| [openai-product-designer-chatgpt-202606.md](openai-product-designer-chatgpt-202606.md) | OpenAI | Product Designer, ChatGPT | Senior IC (inferred) | 2026-06-28 |

### 📊 Matched（已算匹配度）

| 文件 | 公司 | 岗位 | Match | ⭐ | 候选人 |
|---|---|---|---|---|---|
| [linear-principal-product-designer-202606.md](linear-principal-product-designer-202606.md) | Linear | Principal Product Designer | 70–80% | 3.5/5 | Yan Liu |
| [xai-exceptional-designer-202606.md](xai-exceptional-designer-202606.md) | xAI | Exceptional Designer | 78–85% | 4/5 | Yan Liu |
| [anthropic-product-designer-claude-code-202606.md](anthropic-product-designer-claude-code-202606.md) | Anthropic | Product Designer, Claude Code | 80–88% | 4.5/5 | Yan Liu |

<!--
| 文件 | 公司 | 岗位 | Match | 下一步 |
|---|---|---|---|---|
-->

### ✍️ Tailored（简历已改）

> 暂无

### 📤 Applied（已投）

> 暂无

<!--
| 文件 | 公司 | 投递日期 | 渠道 | 当前阶段 |
|---|---|---|---|---|
-->

### 🎤 Interview（面试中）

> 暂无

### 🎉 Offer

> 暂无

### 📁 Closed

> 暂无

---

## 按公司聚合（同公司多份 JD 可复用 Hidden Signal）

### OpenAI
- [openai-product-designer-chatgpt-202606.md](openai-product-designer-chatgpt-202606.md) — Product Designer, ChatGPT (Senior IC, SF)

### xAI
- [xai-exceptional-designer-202606.md](xai-exceptional-designer-202606.md) — Exceptional Designer (Mid→Principal IC, Palo Alto on-site · Grok + X)

### Anthropic
- [anthropic-product-designer-claude-code-202606.md](anthropic-product-designer-claude-code-202606.md) — Product Designer, Claude Code (Senior/Staff IC, SF hybrid · dev tool)

### Linear
- [linear-principal-product-designer-202606.md](linear-principal-product-designer-202606.md) — Principal Product Designer (Principal IC, Remote)

---

## 按岗位类型聚合（同类岗位 must-have 类似，可参考）

### AI Product Designer (Consumer)
- [openai-product-designer-chatgpt-202606.md](openai-product-designer-chatgpt-202606.md) — OpenAI / ChatGPT
- [xai-exceptional-designer-202606.md](xai-exceptional-designer-202606.md) — xAI / Grok + X（社交 × AI 双线）
- [anthropic-product-designer-claude-code-202606.md](anthropic-product-designer-claude-code-202606.md) — Anthropic / Claude Code（AI 编码 dev tool）

<!--
### AI Product Designer
- [openai-product-designer-202606.md](openai-product-designer-202606.md)
-->

---

## 维护规则

1. **新增 JD 文件**：必须同时在「按状态」「按公司」「按岗位类型」三处登记。
2. **状态变更**：从一个 section 移到另一个（如 Matched → Tailored），不要重复列。
3. **关闭一份**：移到 Closed，并在文件里补上"复盘"section。
4. **半年清理一次**：closed 超过 6 个月可以归档到 `jd-bank/archive/`。
