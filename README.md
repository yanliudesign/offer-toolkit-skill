# Offer Toolkit — Career Copilot OS

> 🌐 **English** · [中文](./README.zh.md)

> An end-to-end **Career Copilot skill pack** for job hunting. Three independent, self-contained sub-skills packaged as one — install the whole toolkit, or grab just the piece you need.

```
See a dream job → [Job Description Skill] decode JD · generate Offer Strategy Report
                       ↓ decide to apply
                  [Resume Skill] tailor + polish · 11 print-ready templates · single-file HTML
                       ↓ get the interview
                  [BQ Skill] mine stories · build story bank · STAR structuring · mock interviews
```

---

## What's inside

Three sub-skills, each fully usable on its own:

| # | Sub-skill | What it does | Entry |
|---|---|---|---|
| 1 | **[Job Description Skill](job-description-skill/)** | Decode any JD into a 10-section **Offer Strategy Report** (HTML): TL;DR verdict, Match Score, Interview Probability, company background, JD-to-resume line-by-line match, gaps, why apply / why not, salary reality check, Top 10 interview questions, 6-week action plan. | [`job-description-skill/SKILL.md`](job-description-skill/SKILL.md) |
| 2 | **[Resume Skill](resume-skill/)** | Beautify an existing resume, import from LinkedIn, or build one from scratch by conversation. All roads lead to one structured schema, then render through **11 print-ready templates** (Classic-ATS, Ledger, Tech Compact, Modern Sidebar, Pillar, Elegant Serif, Atelier, Timeline, Swiss, Executive, Color-block). Every render outputs both a locked print version and an in-browser **editable** version. | [`resume-skill/SKILL.md`](resume-skill/SKILL.md) |
| 3 | **[BQ Skill](bq-skill/)** | Not answer-memorization — a reusable **career story bank**. Mine real experiences with a 4-layer probing engine, structure with STAR/CAR, map to competency tags, save bilingual (EN/中文) stories, reuse across any behavioral interview. Flow E: JD-driven Top 20 questions + STAR templates + HTML report. | [`bq-skill/SKILL.md`](bq-skill/SKILL.md) |

---

## The three shared principles

Every sub-skill enforces the same three rules:

1. **Never fabricate.** Every experience, number and title comes from what the user actually provided. Guide, probe, sharpen weak content — but never invent companies, results, or metrics. Verify all numbers.
2. **One question at a time.** Mining stories, building a resume, prepping BQs — these are conversations, not questionnaires.
3. **Structure first, render second.** Whatever the entry point, organize content into a standard data model and confirm it before generating any HTML or answer.

---

## Install

### As a Claude / Copilot skill pack

Drop the whole `offer-toolkit-skill/` folder into your skills directory (e.g. `~/.claude/skills/` or VS Code's prompts folder). All three sub-skills are auto-discovered together.

### Just one of them

Each sub-skill is self-contained. Copy any single subdirectory (e.g. `resume-skill/`) into your skills folder and it works standalone.

### Trigger phrases

| You say | Routes to |
|---|---|
| *"Should I apply to this?"* / paste a JD / *"help me with this job"* | Job Description Skill |
| *"Beautify my resume"* / *"build me one from scratch"* / upload PDF / paste LinkedIn | Resume Skill |
| *"Prep me for behavioral interviews"* / *"tell me about a time…"* / *"mine a story"* | BQ Skill |
| Vague *"help me find a job"* / hand over JD + resume at once | Top-level [`SKILL.md`](SKILL.md) router → runs the full chain |

---

## Repo layout

```
offer-toolkit-skill/
├── SKILL.md                        # Top-level router: intent → sub-skill
├── README.md / README.zh.md
├── LICENSE                         # MIT
├── job-description-skill/          # ① JD decoder & Offer Strategy Report
│   ├── SKILL.md · README.md · README.zh.md
│   ├── prompts/                    # decode / match / tailor / predict / go-no-go
│   ├── frameworks/                 # decode patterns, match rubric, report spec
│   ├── examples/                   # offer-strategy-template.html
│   ├── docs/                       # report preview
│   └── jd-bank/                    # local JD cache (gitignored)
├── resume-skill/                   # ② Resume builder & beautifier
│   ├── SKILL.md · README.md · README.zh.md
│   ├── prompts/                    # beautify / linkedin-import / interview / editable-version
│   ├── schema/                     # resume-data.md — the shared data model
│   ├── guides/                     # writing-tips.md
│   ├── templates/                  # 11 print-ready HTML templates
│   └── docs/                       # template previews
└── bq-skill/                       # ③ Behavioral interview / Career Story OS
    ├── SKILL.md · README.md · README.zh.md
    ├── prompts/                    # story-mining / structuring / jd-driven-prep
    ├── frameworks/                 # STAR/CAR, competency tags, company profiles
    ├── assets/                     # bq-prep report spec + demo
    └── story-bank/                 # user asset — one .md per story
```

---

## Why bundle them?

Each sub-skill originally shipped as its own repo:

- [`job-description-skill`](https://github.com/yanliudesign/job-description-skill)
- [`resume-builder-skill`](https://github.com/yanliudesign/resume-builder-skill)
- [`Behavior-question-skill`](https://github.com/yanliudesign/Behavior-question-skill)

They're still there, still maintained. This toolkit is the **one-stop bundle** for people who want the full Career Copilot loop in a single clone — plus a top-level `SKILL.md` that auto-routes based on where in the job hunt you are.

---

## License

MIT — fork it, remix it, ship your own version.

Created by [Dreameryanyan](https://www.linkedin.com/in/yanliudesign/) ·
[LinkedIn](https://www.linkedin.com/in/yanliudesign/) ·
[X](https://x.com/dreameryanyan) ·
[小红书](https://www.xiaohongshu.com/user/profile/5c1d8d3c000000001202b7fb)
