---
name: linkedin-job-search-skill
description: "LinkedIn 岗位发现与匹配排序。根据用户给的一份种子 JD 和简历，提取目标岗位画像，自动生成多组 LinkedIn Jobs 搜索，采集、去重并按证据给岗位分层，最终输出可直接投递的 shortlist。用户说‘帮我找工作’、‘在 LinkedIn 搜适合我的岗位’、‘找相似职位’、‘根据简历推荐岗位’、‘job search’、‘find jobs like this’时必须使用。只搜索和推荐，不自动投递、不代替用户登录、不绕过验证码。"
compatibility: "需要可访问网页的浏览器工具；无浏览器时降级为生成可点击的 LinkedIn 搜索链接。"
---

# LinkedIn Job Search Skill

把「一份我喜欢的 JD + 我的简历」转成一份有证据、可行动的 LinkedIn 岗位 shortlist。

这个 skill 是 Offer Toolkit 的第 0 步：

```text
种子 JD + 简历 → 搜索画像 → LinkedIn 候选池 → 匹配排序 → shortlist
                                                        ↓
                                              Job Description Skill 深度解码
```

## 边界

- 只做岗位搜索、读取公开职位信息、去重、匹配排序和推荐。
- 永远不自动点击 Apply，不填写申请表，不发送消息，不代表用户投递。
- 永远不索取或处理 LinkedIn 密码、验证码、Cookie 或 session token。
- 遇到登录墙、验证码、频率限制或 robots 限制就停止该路径，不尝试绕过；改用公开搜索结果或输出可点击的 LinkedIn 查询链接。
- 岗位是否仍开放只能按搜索当时页面判断；报告必须写明搜索时间。

## 输入流程

### Step 1 · 收集种子 JD

先要一份用户真正感兴趣的 JD 链接或全文。它不是唯一目标，而是用来提取岗位语义：title、level、scope、domain、核心能力和排除项。

若用户没有种子 JD，接受 2-3 个目标 title + 一句方向描述作为降级输入，并标注「无种子 JD，搜索画像置信度较低」。

### Step 2 · 收集简历

接受 PDF、Word、纯文本或已结构化简历。只从用户提供的事实提取：

- 当前/最近 title 与大致 level
- 年限和最近 3 年的核心 scope
- 3-6 个有直接证据的能力
- 行业、产品阶段、客户类型和团队类型
- 地点、语言、签证等明确约束

不得把种子 JD 的要求写回用户画像，除非简历里有直接证据。

### Step 3 · 补齐硬筛选条件

只追问会显著改变结果集的缺失条件，并且一次只问一个：

1. 工作地点，以及是否接受 remote / hybrid / relocation
2. 目标 level 或可接受的上下浮动
3. 时间范围：24 小时 / 7 天 / 30 天
4. 必须排除的公司、行业、合同类型或签证条件

默认值：最近 7 天、full-time、目标 level 上下浮动一级。默认值必须在最终报告显式列出，不能静默假设。

## 搜索执行

### Step 4 · 生成搜索画像

先在内存中形成这份结构：

```yaml
target_titles: []       # 2-5 个，不堆同义词
level: ""
locations: []
workplace: []           # remote / hybrid / on-site
date_posted: "7d"
employment_types: []
core_capabilities: []   # 3-6 个，必须有简历证据
domains: []             # 0-3 个
company_preferences: []
exclusions: []
seed_signals: []        # 从种子 JD 提取，但不等同于简历能力
```

回显一段不超过 8 行的搜索画像供用户快速纠错。用户没有纠正就继续，不要求第二次确认。

### Step 5 · 构造查询矩阵

生成 6-10 组互补查询，而不是把所有词塞进一个 query：

1. **Exact title**：目标 title + 地点
2. **Adjacent title**：相邻 title + 地点
3. **Capability-led**：title + 1 个核心能力
4. **Domain-led**：title + 目标 domain
5. **Scope-led**：title + 0→1 / platform / enterprise / growth 等 scope 信号

每组查询只放 1-2 个判别词。过长查询会漏掉用词不同但实际匹配的岗位。

LinkedIn 查询 URL 使用公开 Jobs Search 参数；优先设置 keywords、location、date posted、workplace 和 employment type。记录每组实际执行的 query 与 URL。

### Step 6 · 采集候选池

使用浏览器打开 LinkedIn Jobs Search。逐组读取可见结果卡并采集：

- title
- company
- location / workplace
- canonical job URL 或 job id
- posted age
- salary（页面有才记）
- 卡片摘要或命中的关键词

按 canonical URL/job id 去重；没有 job id 时按 `company + normalized title + location` 去重。

停止条件取最先满足者：

- 已有 30 个唯一且通过硬条件的候选
- 每组查看前 2 页或前 25 条
- 页面要求登录、出现验证码或限制访问

不要为了凑满 30 个保留地点、level、岗位类型明显不符的结果。

若 LinkedIn 不可访问：

1. 使用公开 Web 搜索，限定 `site:linkedin.com/jobs/view`，执行同一查询矩阵；或
2. 输出查询矩阵的可点击 LinkedIn URL，让用户打开；
3. 明确标注本次未完成实时采集，不得伪造岗位。

### Step 7 · 两阶段评分

**快速筛选全部候选：**

- 硬条件通过/失败：地点、工作方式、employment type、明确签证门槛
- Title/level fit：0-30
- 核心能力关键词命中：0-30
- Domain/scope 相似度：0-20
- 新鲜度：0-10
- 用户偏好：0-10

只把快速筛选前 10 名带入深度评分。对这 10 个逐个打开职位页，读取可见的完整 JD；读不到完整 JD 的岗位可以保留，但必须标 `Description unavailable`，且最高只能进入 Tier B。

**深度评分前 10：** 读取 [frameworks/ranking-rubric.md](frameworks/ranking-rubric.md)，逐条用简历证据对照 Must Have、Nice to Have 和 Hidden Signals。给区间，不给伪精确单点。

## 输出

默认输出一份 Markdown shortlist；除非用户明确要 HTML，不为一次搜索制造大型报告。

```markdown
# LinkedIn Job Shortlist — YYYY-MM-DD

## Search profile
[目标、地点、时间范围、默认假设]

## Best bets
| Tier | Match | Role | Company | Location | Posted | Why it fits | Main risk | Link |

## Worth a look
[Tier B 表格]

## Skipped patterns
[被批量排除的模式和原因，不逐条堆岗位]

## Search log
[执行过的 queries、采集时间、LinkedIn/公开搜索、访问限制]
```

分层规则：

- **Tier A · Apply first**：深度匹配区间下限 ≥ 70%，无未命中的门槛型 Must Have
- **Tier B · Review**：下限 55-69%，或 JD 不完整但快速评分强
- **Tier C · Skip**：下限 < 55%，或硬条件失败；不进入主表，只汇总排除原因

每个 Tier A 岗位必须给：

- 2 条来自简历的直接匹配证据
- 1 个招聘经理可能担心的风险
- 1 个下一步：直接投 / 先找内推 / 先补 portfolio / 交给 JD Skill 深度解码

最终推荐 5-10 个，不把 30 个搜索结果原样倾倒给用户。链接必须指向具体职位，不只链接搜索页。

## 与 Toolkit 的衔接

- 用户选中某个岗位后，把该 JD + 原简历交给 `job-description-skill` 生成完整 Offer Strategy Report。
- 用户决定投后，把目标 JD + 原简历交给 `resume-skill` 做定向简历。
- 不在本 skill 内复制完整 JD 报告或重写整份简历；岗位发现、岗位决策和简历制作是三个不同步骤。