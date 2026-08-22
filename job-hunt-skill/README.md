<div align="center">

[中文](./README.zh.md) · **English**

# 🔎 job-hunt-skill

---

**Turn a resume or target direction into a complete, searchable job opportunity list.** Discover · deduplicate · verify · rank · track.

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

> 📦 Part of **[offer-toolkit-skill](https://github.com/yanliudesign/offer-toolkit-skill)** — the complete Search · JD · Resume · BQ · Compare · Negotiate workflow.

An agent skill for turning a resume, target direction, seed JD, or pile of job links into a searchable HTML job database. It searches public sources, removes duplicates, distinguishes verified facts from inference, and keeps the complete qualified pool instead of collapsing everything into a five-role shortlist.

---

## Report preview

<img src="examples/en/job-search-01.png" alt="job-hunt-skill report overview" width="100%">

<table>
	<tr>
		<td width="50%"><img src="examples/en/job-search-02.png" alt="Ranked job opportunities" width="100%"></td>
		<td width="50%"><img src="examples/en/job-search-03.png" alt="Job opportunity details" width="100%"></td>
	</tr>
	<tr>
		<td><img src="examples/en/job-search-04.png" alt="Job search strategy" width="100%"></td>
		<td><img src="examples/en/job-search-05.png" alt="Search methodology and evidence rules" width="100%"></td>
	</tr>
</table>

---

## How it works

```text
Resume / target / seed JD
		   ↓
Search profile → query matrix → public candidate pool → deduplication
		   ↓
Evidence grading → match ranking → searchable HTML job-hunt-skill report
```

1. **Provide a starting point** — a resume, target titles, a seed JD, or existing job links.
2. **Confirm hard constraints** — location, workplace mode, level, date range, and exclusions.
3. **Get a searchable report** — every qualified unique role, evidence status, match rationale, gaps, and direct links in one HTML file.

## What it does

- Builds a focused search profile and complementary query matrix
- Searches LinkedIn, company career pages, and other public sources
- Deduplicates by canonical job ID and URL
- Separates verified facts, partial evidence, inference, and unknowns
- Deep-scores only roles with enough visible JD evidence
- Keeps the complete qualified pool instead of returning an arbitrary shortlist
- Generates a self-contained HTML report with search, filters, domain tags, reasons, gaps, and direct job links
- Updates an existing list while preserving first-seen history

## Boundaries

- Never applies for jobs, fills forms, sends messages, or acts as the user
- Never asks for passwords, verification codes, cookies, or session tokens
- Never bypasses login walls, CAPTCHAs, rate limits, or robots restrictions
- Never invents salary, posted date, workplace policy, visa policy, or JD requirements

## Trigger examples

- “Use job-hunt-skill to build a searchable report from my resume.”
- “Find matching Principal Product Designer roles and make a searchable report.”
- “Turn these LinkedIn links into a deduplicated job tracker.”
- “Update last week’s job list with newly posted AI design roles.”

## Install

Copy the entire `job-hunt-skill/` directory into your agent skills directory. The folder is self-contained and does not require the rest of Offer Toolkit.

## Repository structure

```text
job-hunt-skill/
├── SKILL.md                     # Workflow, boundaries, and output contract
├── README.md / README.zh.md    # English and Chinese documentation
├── examples/
│   ├── en/                     # English report screenshots
│   └── cn/                     # Chinese report screenshots
├── assets/
│   └── report-spec.md          # Searchable HTML report specification
├── references/
│   └── evidence-ranking.md     # Evidence and ranking rules
└── evals/
	└── evals.json              # Trigger and behavior evaluations
```

## Related skills

- [offer-toolkit-skill](https://github.com/yanliudesign/offer-toolkit-skill) — complete Search · JD · Resume · BQ · Compare · Negotiate bundle
- [job-description-skill](https://github.com/yanliudesign/job-description-skill) — deep analysis for a selected role
- [resume-builder-skill](https://github.com/yanliudesign/resume-builder-skill) — resume generation and beautification
- [Behavior-question-skill](https://github.com/yanliudesign/Behavior-question-skill) — behavioral interview preparation and story bank

## License

MIT — fork it, remix it, ship your own version.

Created by [Dreameryanyan](https://www.linkedin.com/in/yanliudesign/) ·
[LinkedIn](https://www.linkedin.com/in/yanliudesign/) ·
[X](https://x.com/yanliudreamer) ·
[Xiaohongshu](https://www.xiaohongshu.com/notification)
