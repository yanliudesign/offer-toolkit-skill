<div align="center">

**中文** · [English](./README.md)

# 🔎 job-hunt-skill

---

**把简历或求职方向变成一份完整、可搜索的职位机会清单。**发现 · 去重 · 核验 · 排序 · 跟踪。

[![License](https://img.shields.io/badge/LICENSE-MIT-4c8bf5?style=flat-square&labelColor=333)](https://github.com/yanliudesign/job-hunt-skill/blob/main/LICENSE)
[![Version](https://img.shields.io/badge/VERSION-1.0.0-2ea44f?style=flat-square&labelColor=333)]()
[![Output](https://img.shields.io/badge/OUTPUT-Searchable_HTML-2ea44f?style=flat-square&labelColor=333)]()
[![Stars](https://img.shields.io/github/stars/yanliudesign/job-hunt-skill?style=flat-square&label=STARS&color=e37f2c&labelColor=333)](https://github.com/yanliudesign/job-hunt-skill/stargazers)

[![Claude Code](https://img.shields.io/badge/Claude_Code-Skill-d97757?style=flat-square&labelColor=1a1a1a&logo=anthropic&logoColor=white)](https://claude.ai/code)
[![Codex](https://img.shields.io/badge/Codex-Skill-2ea44f?style=flat-square&labelColor=1a1a1a)]()
[![OpenCode](https://img.shields.io/badge/OpenCode-Skill-4c8bf5?style=flat-square&labelColor=1a1a1a)]()
[![OpenClaw](https://img.shields.io/badge/OpenClaw-Skill-8b5cf6?style=flat-square&labelColor=1a1a1a)]()
[![Hermes](https://img.shields.io/badge/Hermes-Skill-e879a8?style=flat-square&labelColor=1a1a1a)]()

</div>

> 📦 属于 **[offer-toolkit-skill](https://github.com/yanliudesign/offer-toolkit-skill)** 求职工具包 — 覆盖 Search · JD · Resume · BQ · Compare · Negotiate 的完整链路。

一个把简历、目标方向、种子 JD 或已有职位链接变成可搜索 HTML 职位数据库的 agent skill。它会搜索公开来源、去重、区分已核验事实与方向性推断，并保留所有通过硬条件的唯一岗位，而不是随意压缩成 5 个推荐。

---

## 报告预览

<img src="examples/cn/job-search-01.png" alt="job-hunt-skill 报告总览" width="100%">

<table>
    <tr>
        <td width="50%"><img src="examples/cn/job-search-02.png" alt="职位匹配与排序" width="100%"></td>
        <td width="50%"><img src="examples/cn/job-search-03.png" alt="职位机会详情" width="100%"></td>
    </tr>
    <tr>
        <td><img src="examples/cn/job-search-04.png" alt="职位搜索策略" width="100%"></td>
        <td><img src="examples/cn/job-search-05.png" alt="搜索方法与证据规则" width="100%"></td>
    </tr>
</table>

---

## 怎么运行

```text
简历 / 目标方向 / 种子 JD
             ↓
搜索画像 → 查询矩阵 → 公开候选池 → 去重
             ↓
证据分层 → 匹配排序 → 可搜索 HTML job-hunt-skill 报告
```

1. **给一个起点** — 简历、目标 title、种子 JD 或已有职位链接均可。
2. **确认硬条件** — 地点、工作方式、level、发布时间范围和排除项。
3. **拿到可搜索报告** — 所有合格唯一岗位、证据状态、匹配理由、差距和直达链接都在一个 HTML 文件里。

## 能做什么

- 建立聚焦的搜索画像和互补查询矩阵
- 搜索 LinkedIn、公司招聘页和其他公开来源
- 按 canonical job ID 和 URL 去重
- 区分已核验事实、部分证据、方向性推断和未知信息
- 只对有足够可见 JD 证据的岗位做深度评分
- 保留完整合格候选池，不随意截断成 shortlist
- 生成带搜索、筛选、领域标签、理由、差距和职位直达链接的单文件 HTML
- 更新旧清单，同时保留首次发现时间

## 边界

- 不自动投递、不填写表单、不发送消息、不代表用户行动
- 不索取密码、验证码、Cookie 或 session token
- 不绕过登录墙、CAPTCHA、频率限制或 robots 限制
- 不杜撰薪资、发布时间、办公政策、签证政策或 JD 要求

## 触发示例

- “根据我的简历做一份求职岗位清单。”
- “找一批匹配的 Principal Product Designer 职位，生成可搜索报告。”
- “把这些 LinkedIn 链接去重后做成职位 tracker。”
- “更新上周的职位清单，加入新发布的 AI 设计岗位。”

## 安装

把整个 `job-hunt-skill/` 目录复制到你的 agent skills 目录。它是自包含的，不需要同时安装 Offer Toolkit 的其他部分。

## 目录结构

```text
job-hunt-skill/
├── SKILL.md                     # 工作流、边界和交付契约
├── README.md / README.zh.md    # 中英文文档
├── examples/
│   ├── en/                     # 英文报告截图
│   └── cn/                     # 中文报告截图
├── assets/
│   └── report-spec.md          # 可搜索 HTML 报告规范
├── references/
│   └── evidence-ranking.md     # 证据与排序规则
└── evals/
    └── evals.json              # 触发与行为评测
```

## 配套 skill

- [offer-toolkit-skill](https://github.com/yanliudesign/offer-toolkit-skill) — Search · JD · Resume · BQ · Compare · Negotiate 完整工具包
- [job-description-skill](https://github.com/yanliudesign/job-description-skill) — 对选中岗位做深度解码
- [resume-builder-skill](https://github.com/yanliudesign/resume-builder-skill) — 简历生成与美化
- [Behavior-question-skill](https://github.com/yanliudesign/Behavior-question-skill) — 行为面试准备与故事库

## License

MIT 协议 — 随便 fork、改造、发布自己的版本。

Created by [Dreameryanyan](https://www.linkedin.com/in/yanliudesign/) ·
[LinkedIn](https://www.linkedin.com/in/yanliudesign/) ·
[X](https://x.com/yanliudreamer) ·
[小红书](https://www.xiaohongshu.com/notification)