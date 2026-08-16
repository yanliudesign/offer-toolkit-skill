---
name: job-hunt-list
description: "批量发现、整理和持续维护求职岗位清单。根据用户的简历、目标方向或种子 JD，搜索 LinkedIn 与公开网页，去重并建立尽量完整的候选池，用证据区分已核验事实和方向性推断，最后生成可搜索、可筛选的单文件 HTML Job Hunt List。用户说‘帮我批量找岗位’、‘整理职位清单’、‘做一个 job hunt list’、‘根据简历搜工作’、‘把这些 LinkedIn 职位做成表格’、‘持续跟踪岗位’时必须使用。只发现和分析岗位；绝不自动申请、处理登录凭据或绕过访问限制。"
compatibility: "需要网页或浏览器工具以实时发现岗位；无法访问网页时可整理用户提供的链接，或输出可点击的搜索查询。生成报告需要本地文件写入能力。"
---

# Job Hunt List

把“帮我看看有哪些工作”变成一份可以持续搜索、比较和更新的职位数据库，而不是一次性的推荐答案。

```text
简历 / 目标方向 / 种子 JD
          ↓
搜索画像 → 查询矩阵 → 公开候选池 → 去重与证据分层
          ↓
完整 Job Hunt List HTML → 搜索 / 筛选 / 打开职位 → 选择深评对象
```

## 职责边界

- 负责批量发现、采集公开信息、去重、初筛、证据分层、排序和生成职位清单。
- 默认保留所有通过硬条件的唯一职位；不要擅自压缩成 5–10 个 shortlist。
- 不自动点击 Apply，不填写表单，不发送消息，不代表用户投递。
- 不索取或处理密码、验证码、Cookie、session token 或其他登录凭据。
- 遇到登录墙、验证码、HTTP 429、robots 限制时停止该访问路径；切换到公开公司招聘页、公开搜索结果或可点击查询链接，不尝试绕过。
- 不把职位发现扩写成完整单岗位 Offer Strategy。用户选中岗位后再交给 `job-description-skill`。

## 0. 判断输入是否足够

优先使用用户已经提供的材料，不重复索取：

1. 简历：PDF、Word、HTML 或纯文本均可。
2. 目标：title、level、领域、地点、工作方式。
3. 可选种子 JD：用于补充岗位语义，不得反向伪造简历能力。
4. 可选已有链接：用于合并、补充或更新旧清单。

若缺少会显著改变结果集的信息，一次只问一个问题，顺序如下：

1. 目标 title / level
2. 地点与 remote / hybrid / relocation
3. 时间范围
4. 必须排除的行业、公司、合同类型或签证门槛

默认值为最近 30 天、full-time、目标 level 上下浮动一级。最终报告必须显式写出默认值。

## 1. 建立搜索画像

只从用户材料提取有证据的能力，形成：

```yaml
target_titles: []
adjacent_titles: []
level: ""
locations: []
workplace: []
date_posted: "30d"
employment_types: ["full-time"]
core_capabilities: []
domains: []
company_preferences: []
exclusions: []
seed_signals: []
```

向用户回显不超过 8 行的画像。若用户没有纠正，继续执行，不要求二次确认。

## 2. 生成互补查询矩阵

生成 6–12 组短查询，每组只放 1–2 个判别词：

1. Exact title：目标 title + 地点
2. Adjacent title：相邻 title + 地点
3. Capability-led：title + 核心能力
4. Domain-led：title + 领域
5. Scope-led：title + platform / growth / 0-to-1 / enterprise 等 scope
6. Company-led：用户偏好公司或相邻公司 + title

记录每组 query、URL、执行时间和来源。不要把所有同义词塞进一个查询，否则会系统性漏岗。

## 3. 发现公开职位

按以下优先级使用可访问来源：

1. 具体职位页或公司官方招聘页
2. LinkedIn 可公开访问的职位页与搜索结果
3. 搜索引擎中的 `site:linkedin.com/jobs/view` 结果
4. 其他公开招聘页面

每条候选尽可能采集：

- title
- company
- canonical URL / job id
- location 与 workplace
- posted date / age
- salary，仅页面明确展示时记录
- JD 可见程度：full / partial / unavailable
- source 与 checked_at

按 canonical job id / URL 去重。没有 id 时，使用 `normalized company + title + location`，并保留证据更完整、更新时间更新的记录。

停止条件：

- 查询矩阵全部跑完；或
- 每组已查看前 2 页 / 前 25 条；或
- 当前来源触发访问限制。

不要为了凑数量保留明显违反地点、level、employment type 或硬门槛的岗位。

## 4. 严格区分事实与推断

读取 [references/evidence-ranking.md](references/evidence-ranking.md)，为每条字段标记证据状态：

- `verified`：职位页或官方页直接出现
- `partial`：公开摘要可见，但完整 JD 不可见
- `inferred`：根据 title、公司或邻近信号推断
- `unknown`：没有可靠信息

未知字段留空或显示“待核验”。绝不补写薪资、发布时间、工作方式、签证政策、岗位状态或 JD 要求。

## 5. 排序，但不删掉完整候选池

先通过硬条件，再按两个层次排序：

1. 已读取完整 JD 的岗位：用 `0.60 Must Have + 0.20 Nice to Have + 0.20 Hidden Signal Fit` 计算匹配区间。
2. JD 不完整的岗位：只做方向性排序，不显示伪精确 match score。

排序顺序：证据完整度 → 匹配强度 → 发布时间 → 与目标方向的接近度。缺失发布时间不能自动视为旧岗位。

内部可保留优先级字段用于排序和筛选，但默认不要在职位行显示 Tier A / Tier B 标签。用户要求显示时才显示。

## 6. 生成单文件 HTML

默认生成 HTML，而不是 Markdown。读取 [assets/report-spec.md](assets/report-spec.md) 并遵守其数据、表格和交互契约。

文件名：`job-hunt-list-{candidate-or-topic}-{YYYYMMDD}.html`

默认保存到用户指定目录；未指定时保存到当前工作目录。生成后打开本地文件供用户检查。

报告必须包含：

- 搜索画像、生成时间、来源与证据说明
- 完整唯一职位数、深度核验数
- 搜索框和快速筛选
- 职位、公司、领域标签、推荐理由、主要 Gap
- 可核验的发布日期、地点 / 工作方式、薪资、匹配度
- 指向具体职位的打开链接
- 查询日志和访问限制说明

不要在页面里暴露本地简历全文、登录信息或无关个人数据。

## 7. 验证后再交付

至少完成以下检查：

1. HTML 内联 JavaScript 语法有效。
2. 渲染职位行数等于去重后的数据行数。
3. 每行表格列数一致，具体职位链接有效成形。
4. 搜索能命中 title、company、domain、reason 与 gap。
5. “待核验”字段没有被自动补成事实。
6. 若有领域标签，标签紧邻公司名并可被搜索。
7. 页面不显示 Tier A / Tier B badge，除非用户明确要求。

有浏览器测试工具时，实际加载页面并验证 DOM；没有时至少做脚本语法检查和静态结构检查。

## 8. 后续更新

用户提供旧 Job Hunt List 时：

1. 解析现有职位 id / URL。
2. 只新增新发现职位，合并更完整证据。
3. 不因为暂时访问不到就断言岗位关闭。
4. 保留原始 `first_seen`，更新 `last_checked`。
5. 在报告中列出新增、更新、待复核数量。

## 交付口径

简要告诉用户：保存路径、唯一职位数、深评数量、访问限制和验证结果。不要把整张职位表复制回聊天。
