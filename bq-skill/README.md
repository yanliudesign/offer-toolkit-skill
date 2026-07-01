# BQ Skill — Career Story OS

> 🌐 **English** · [中文](./README.zh.md)

A Claude / Copilot skill that turns *"I can answer this one behavioral question"* into *"I own a reusable bank of career stories."* It mines your real experiences, structures them with STAR/CAR, maps them to competencies, and builds a bilingual (EN/中文) story bank you can reuse across any behavioral interview.

![Flow E report — JD-driven Top 20 interview-question prep with STAR templates](assets/preview.png)
<sub>Flow E output: a Top 20 question set reverse-engineered from a JD, with STAR templates and editable model answers. <i>(Demo uses a fictional candidate — no real personal data.)</i></sub>

## Core loop
Mine → Structure → Map → Save → Reuse

## Layout
```
bq-skill/
├── SKILL.md                      # Entry point: intent routing + five flows
├── prompts/
│   ├── story-mining.md           # ★ Four-layer probing engine (Flow A)
│   ├── structuring.md            # Diagnose + rewrite an existing answer (Flow C)
│   └── jd-driven-prep.md         # ★ JD × resume → Top 20 questions + STAR templates (Flow E)
├── frameworks/
│   ├── star-car.md               # STAR/CAR/SOAR selection + one story, many questions
│   ├── competency-tags.md        # Competency dictionary + BQ reverse-lookup
│   └── company-profiles.md       # Amazon LP / Meta / Anthropic / OpenAI styles
├── assets/
│   └── bq-prep-report.md         # Editorial HTML report spec for Flow E
└── story-bank/                    # User asset — one .md per story
    ├── _index.md                 # Competency → story reverse-lookup table
    ├── _story-template.md        # Story template
    └── convince-team-rewrite.md  # Example story (safe to delete)
```

## The five flows
- **A · Mine a new story** — a four-layer probing engine that pulls real, signal-rich, quantifiable events out of someone who thinks "I have nothing to talk about," then deepens one into a bank-ready story.
- **B · Answer a specific BQ** — check the bank first, reuse a hit, or mine a new one on the spot.
- **C · Polish an existing answer** — diagnose structure problems (Situation too long, "I" vs "we", no quantified result) and rewrite.
- **D · Mock interview** — one question at a time in the target company's style, with feedback.
- **E · JD-driven prep** — see below.

## Hooks into job-description-skill
Flow E reuses the **Must-Haves + Hidden Signals** decoded by
[job-description-skill](https://github.com/yanliudesign/job-description-skill) to reverse-engineer a
**Top 20 interview-question set** for one specific role, builds a STAR prep template per question from
the candidate's real resume, and outputs an editorial-style HTML report. Together the three skills form
a Career Copilot loop: **JD decode → match / tailor résumé → BQ prep + story building.**

## Usage
Tell Claude *"help me prep for behavioral interviews"*, *"mine a story for my bank"*,
*"here's a BQ, help me answer it"*, or just run `/bq-skill`.

## Principles
1. **Bank first.** Always check `story-bank/_index.md` before mining — reuse beats re-digging.
2. **One question at a time.** Mining is a conversation, not a questionnaire.
3. **Never fabricate.** All material comes from the user's real experience; every metric is verified with them.

## Versions
- **v0.6 (current)** — Story Mining engine + single-story closed loop + bilingual output + lightweight mock +
  **Flow E (JD-driven Top 20 questions + STAR templates + editorial HTML report, hooked into job-description-skill).**
- v1 — deeper competency dictionary / company profiles, bank retrieval polish.
- v2 — deeper mock interview (per-company questions + scored feedback).

## What you inject (the moat)
The probing scripts in `prompts/story-mining.md` and the tag dictionary in
`frameworks/competency-tags.md` are where a coach's private experience lives — feed in your own phrasing
and tags and the skill grows more and more like *you*.

## Related skills
- [job-description-skill](https://github.com/yanliudesign/job-description-skill) — JD Decoder & Offer Strategy OS
- [resume-builder-skill](https://github.com/yanliudesign/resume-builder-skill) — Resume generation & beautification
