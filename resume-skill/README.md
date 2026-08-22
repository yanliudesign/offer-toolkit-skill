<div align="center">

[中文](./README.zh.md) · **English**

# 📄 Resume Skill

---

**One resume data schema, eleven print-ready templates.**

[![License](https://img.shields.io/badge/LICENSE-MIT-4c8bf5?style=flat-square&labelColor=333)](./LICENSE)
[![Version](https://img.shields.io/badge/VERSION-1.0.0-2ea44f?style=flat-square&labelColor=333)]()
[![Templates](https://img.shields.io/badge/TEMPLATES-11-2ea44f?style=flat-square&labelColor=333)]()
[![Stars](https://img.shields.io/github/stars/yanliudesign/resume-builder-skill?style=flat-square&label=STARS&color=e37f2c&labelColor=333)](https://github.com/yanliudesign/resume-builder-skill/stargazers)

[![Claude Code](https://img.shields.io/badge/Claude_Code-Skill-d97757?style=flat-square&labelColor=1a1a1a&logo=anthropic&logoColor=white)](https://claude.ai/code)
[![Codex](https://img.shields.io/badge/Codex-Skill-2ea44f?style=flat-square&labelColor=1a1a1a)]()
[![OpenCode](https://img.shields.io/badge/OpenCode-Skill-4c8bf5?style=flat-square&labelColor=1a1a1a)]()
[![OpenClaw](https://img.shields.io/badge/OpenClaw-Skill-8b5cf6?style=flat-square&labelColor=1a1a1a)]()
[![Hermes](https://img.shields.io/badge/Hermes-Skill-e879a8?style=flat-square&labelColor=1a1a1a)]()

</div>

> 📦 Part of the **[offer-toolkit-skill](https://github.com/yanliudesign/offer-toolkit-skill)** — the full job-hunt bundle (Search · JD · Resume · BQ · Compare · Negotiate). Install the bundle to get all six in one shot.

An agent skill that polishes an existing resume, pulls one in from LinkedIn, or builds one from scratch by chatting with you. Every input funnels through one standardized data schema and then renders into any of 13 print-ready templates — switching templates is just a skin change, the content stays the same.

![Thirteen print-ready resume templates rendered from one data schema](docs/preview.png)

<sub>More screenshots: [English gallery](docs/en/) · [中文相册](docs/zh/)</sub>

---

## Three entry points

| What the user says | Flow | Script |
|---|---|---|
| *"Beautify my resume"* / uploads a PDF/docx/txt | **A. Beautify an existing resume** | [`prompts/beautify.md`](prompts/beautify.md) |
| *"Here's my LinkedIn"* / pastes a linkedin.com link | **B. LinkedIn import** | [`prompts/linkedin-import.md`](prompts/linkedin-import.md) |
| *"Build me one from scratch"* / *"let's chat"* | **C. Conversational build** | [`prompts/interview.md`](prompts/interview.md) |

All three funnel into [`schema/resume-data.md`](schema/resume-data.md), then render through a template.

## Thirteen templates

| Preview | Template | Best for |
|:---:|---|---|
| <img src="docs/templates/classic-ats.png" width="300"> | **Classic / ATS**<br>[`classic-ats.html`](templates/classic-ats.html) | Single-column, machine-parseable, safest for mass applications |
| <img src="docs/templates/ledger.png" width="300"> | **Ledger**<br>[`ledger.html`](templates/ledger.html) | LaTeX-style serif, justified, nested bullets — SWE / data / eng |
| <img src="docs/templates/tech-compact.png" width="300"> | **Tech Compact**<br>[`tech-compact.html`](templates/tech-compact.html) | High density + mono accents, fits many projects on one page |
| <img src="docs/templates/modern-sidebar.png" width="300"> | **Modern Sidebar**<br>[`modern-sidebar.html`](templates/modern-sidebar.html) | Two-column with dark sidebar, modern feel |
| <img src="docs/templates/pillar.png" width="300"> | **Pillar**<br>[`pillar.html`](templates/pillar.html) | Enhancv-style, blue accents + skill chips + icon achievements — PM / marketing |
| <img src="docs/templates/elegant-serif.png" width="300"> | **Elegant Serif**<br>[`elegant-serif.html`](templates/elegant-serif.html) | Centered editorial serif — design / consulting / marketing |
| <img src="docs/templates/atelier.png" width="300"> | **Atelier**<br>[`atelier.html`](templates/atelier.html) | Whitespace-heavy minimal — design / creative roles |
| <img src="docs/templates/timeline.png" width="300"> | **Timeline**<br>[`timeline.html`](templates/timeline.html) | Vertical timeline spine — shows career progression at a glance |
| <img src="docs/templates/swiss.png" width="300"> | **Swiss**<br>[`swiss.html`](templates/swiss.html) | Swiss grid, bold Helvetica + red accent — design / brand / creative |
| <img src="docs/templates/executive.png" width="300"> | **Executive**<br>[`executive.html`](templates/executive.html) | Navy serif, understated gravitas — finance / consulting / senior leaders |
| <img src="docs/templates/editorial-banner.png" width="300"> | **Editorial Banner**<br>[`editorial-banner.html`](templates/editorial-banner.html) | Magazine-style 3-col header, red serif accent, giant last-name band at the bottom — brand / content / editorial |
| <img src="docs/templates/photo-corporate.png" width="300"> | **Photo Corporate**<br>[`photo-corporate.html`](templates/photo-corporate.html) | Dark banner + circular photo, sidebar with skill bars, vertical timeline, References section — marketing / PM / business |
| <img src="docs/templates/photo-minimal.png" width="300"> | **Photo Minimal**<br>[`photo-minimal.html`](templates/photo-minimal.html) | Red-accent split serif name, circular photo, Awards + Skills sidebar — designer / creator / portfolio |

**Picking one:** mass-applying / passing the bots → Classic-ATS or Ledger; a human reads it / referral / portfolio-facing → the others stand out more.

## Three first principles

1. **Never fabricate.** Every experience, responsibility and number comes from what the user actually provided. Guide, probe, sharpen weak bullets — but never invent a company, title, result, or metric. Verify every number; mark unknowns `[to confirm]`.
2. **One question at a time.** Building a resume by conversation is an interview, not a questionnaire.
3. **Structure first, render second.** Whatever the entry point, organize content into the `schema/resume-data.md` fields and confirm it before rendering HTML.

## Editable variant — click any text to edit

Every render produces **two files**:

| File | Use |
|---|---|
| `<name>-resume-<template>.html` | Locked print-ready output — `Cmd+P` → PDF |
| `<name>-resume-<template>-editable.html` | Click any text in the browser to edit; `Cmd+P` when done |

The editable variant layers three things on top of any template (see [`prompts/editable-version.md`](prompts/editable-version.md)) without touching its visual design:

- `contenteditable="true"` on the content container
- Hover / focus affordance (dashed yellow → solid blue outline)
- A floating toolbar (top-right) with **Save as PDF** and **Lock** buttons
- `@media print` hides the toolbar and edit highlights so the exported PDF stays clean

⚠️ Browser edits live only in the current tab — refresh and they're gone. Always `Cmd+P` to lock changes into a PDF.

## Usage

Drop the whole `resume-skill/` folder into your skills directory (e.g. `~/.claude/skills/resume-skill/`) and just say *"beautify this resume"* (attach a PDF), *"I have no resume, let's build one"*, or *"here's my LinkedIn, make me one."* Claude reads `SKILL.md` and runs the matching flow.

**Output:** two self-contained single-file HTMLs — `<name>-resume-<template>.html` (locked) and `<name>-resume-<template>-editable.html` (click-to-edit). Open either in a browser → `Cmd+P` → Save as PDF (margins None/Default, **enable background graphics**).

## Layout
```
resume-skill/
├── SKILL.md                       # Workflow entry point (read first)
├── schema/resume-data.md          # Standardized fields — the hub format for every entry point
├── prompts/
│   ├── beautify.md                # Entry A: beautify an existing resume
│   ├── linkedin-import.md         # Entry B: LinkedIn import + fallback
│   ├── interview.md               # Entry C: conversational collection
│   └── editable-version.md        # Injection snippet that upgrades any render into a click-to-edit page
├── guides/writing-tips.md         # Bullet craft, quantification, ATS keywords, common mistakes
└── templates/                     # 13 print-optimized HTML templates
```

## Related skills
- [offer-toolkit-skill](https://github.com/yanliudesign/offer-toolkit-skill) — the all-in-one bundle (Search · JD · Resume · BQ · Compare · Negotiate)
- [job-hunt-skill](https://github.com/yanliudesign/job-hunt-skill) — Job discovery and searchable opportunity list
- [job-description-skill](https://github.com/yanliudesign/job-description-skill) — Job Description Decoder
- [Behavior-question-skill](https://github.com/yanliudesign/Behavior-question-skill) — Behavioral interview / story bank

## License

MIT — fork it, remix it, ship your own version.

Created by [Dreameryanyan](https://www.linkedin.com/in/yanliudesign/) ·
[LinkedIn](https://www.linkedin.com/in/yanliudesign/) ·
[X](https://x.com/yanliudreamer) ·
[Xiaohongshu](https://www.xiaohongshu.com/notification)
