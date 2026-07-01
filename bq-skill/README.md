# BQ Skill

> 📦 Part of the **[offer-toolkit-skill](https://github.com/yanliudesign/offer-toolkit-skill)** — the full job-hunt bundle (JD · Resume · BQ). Install the bundle to get all three in one shot.

> 🌐 **English** · [中文](./README.zh.md)

A Claude skill for behavioral interview prep. Instead of handing you canned answers, it helps you dig your real past experiences out and organize them into a story bank you can reuse. It asks about your experience step by step, uses STAR/CAR to shape each story, tags them ("took ownership", "handled ambiguity", etc.), and saves each one in English and Chinese — so next time you get a different behavioral question, the same story still works.

![JD-driven prep report — Top 20 interview-question prep with STAR templates](assets/preview.png)
<sub>JD-driven prep output: a Top 20 question set reverse-engineered from a JD, with STAR templates and editable model answers. <i>(Demo uses a fictional candidate — no real personal data.)</i></sub>

## Layout
```
bq-skill/
├── SKILL.md                      # Entry point: intent routing + five flows
├── prompts/
│   ├── story-mining.md           # ★ Four-layer probing engine (story mining)
│   ├── structuring.md            # Diagnose + rewrite an existing answer (polishing)
│   └── jd-driven-prep.md         # ★ JD × resume → Top 20 questions + STAR templates (JD-driven prep)
├── frameworks/
│   ├── star-car.md               # STAR/CAR/SOAR selection + one story, many questions
│   ├── competency-tags.md        # Competency dictionary + BQ reverse-lookup
│   └── company-profiles.md       # Amazon LP / Meta / Anthropic / OpenAI styles
├── assets/
│   └── bq-prep-report.md         # Editorial HTML report spec for JD-driven prep
└── story-bank/                    # User asset — one .md per story
    ├── _index.md                 # Competency → story reverse-lookup table
    ├── _story-template.md        # Story template
    └── convince-team-rewrite.md  # Example story (safe to delete)
```

## What it can do

- **Mine a new story** — pulls real, quantifiable events out of someone who thinks *"I have nothing to talk about,"* then deepens one into a bank-ready story.
- **Answer a specific BQ** — check the bank first, reuse a hit, or mine a new one on the spot.
- **Polish an existing answer** — diagnose structure problems (Situation too long, "I" vs "we", no quantified result) and rewrite.
- **Mock interview** — one question at a time in the target company's style, with feedback.
- **JD-driven prep** — reads a JD + your resume, reverse-engineers a Top 20 interview-question set for that role, and builds a STAR prep template for each question. (See next.)

## Hooks into job-description-skill
JD-driven prep reuses the **Must-Haves + Hidden Signals** decoded by
[job-description-skill](https://github.com/yanliudesign/job-description-skill) to reverse-engineer a
**Top 20 interview-question set** for one specific role, builds a STAR prep template per question
from your real resume, and outputs an HTML report.

## Usage
Tell Claude *"help me prep for behavioral interviews"*, *"mine a story for my bank"*,
*"here's a BQ, help me answer it"*, or just run `/bq-skill`.

## Principles
1. **Bank first.** Always check `story-bank/_index.md` before mining — reuse beats re-digging.
2. **One question at a time.** Mining is a conversation, not a questionnaire.
3. **Never fabricate.** All material comes from the user's real experience; every metric is verified with them.

## Making it your own
The probing scripts in `prompts/story-mining.md` and the competency dictionary in
`frameworks/competency-tags.md` are where to inject your own phrasing and vocabulary — the more you
put in, the more the skill sounds like you.

## Related skills
- [offer-toolkit-skill](https://github.com/yanliudesign/offer-toolkit-skill) — the all-in-one bundle (JD · Resume · BQ)
- [job-description-skill](https://github.com/yanliudesign/job-description-skill) — Job Description Decoder
- [resume-builder-skill](https://github.com/yanliudesign/resume-builder-skill) — Resume generation & beautification

## License

MIT — fork it, remix it, ship your own version.

Created by [Dreameryanyan](https://www.linkedin.com/in/yanliudesign/) ·
[LinkedIn](https://www.linkedin.com/in/yanliudesign/) ·
[X](https://x.com/yanliudreamer) ·
[Xiaohongshu](https://www.xiaohongshu.com/notification)
