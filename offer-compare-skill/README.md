<div align="center">

[中文](./README.zh.md) · **English**

# ⚖️ Offer Compare Skill

---

**Turn two (or more) offers into one clear, opinionated decision — in 3 steps.**

[![License](https://img.shields.io/badge/LICENSE-MIT-4c8bf5?style=flat-square&labelColor=333)](./LICENSE)
[![Version](https://img.shields.io/badge/VERSION-1.0.0-2ea44f?style=flat-square&labelColor=333)]()
[![Stars](https://img.shields.io/github/stars/yanliudesign/offer-compare-skill?style=flat-square&label=STARS&color=e37f2c&labelColor=333)](https://github.com/yanliudesign/offer-compare-skill/stargazers)

[![Claude Code](https://img.shields.io/badge/Claude_Code-Skill-d97757?style=flat-square&labelColor=1a1a1a&logo=anthropic&logoColor=white)](https://claude.ai/code)
[![Codex](https://img.shields.io/badge/Codex-Skill-2ea44f?style=flat-square&labelColor=1a1a1a)]()
[![OpenCode](https://img.shields.io/badge/OpenCode-Skill-4c8bf5?style=flat-square&labelColor=1a1a1a)]()
[![OpenClaw](https://img.shields.io/badge/OpenClaw-Skill-8b5cf6?style=flat-square&labelColor=1a1a1a)]()
[![Hermes](https://img.shields.io/badge/Hermes-Skill-e879a8?style=flat-square&labelColor=1a1a1a)]()

</div>

> 📦 Part of the **[offer-toolkit-skill](https://github.com/yanliudesign/offer-toolkit-skill)** — the full job-hunt bundle (Search · JD · Resume · BQ · Compare · Negotiate). Install the bundle to get all six in one shot.

An agent skill for choosing between multiple offers. Modeled after a Senior Career Decision Advisor who is willing to take a side. Drop in two (or more) offers and it hands back an HTML decision report telling you: the honest 4-year TC range for each (with every assumption listed), a 7-dimension side-by-side scoreboard (Comp · Growth · AI Exposure · Company Strength · Manager/Team Risk · Promo Speed · Lifestyle), 5 hidden signals people usually miss (front-loaded vs long-term upside · resume value · switch-out difficulty · uncertainty), the top 4–6 risks per offer, and — most important — **one clear recommendation** (never a neutral "both look great, up to you") with an "If you are X → A / If you are Y → B" fork so a second archetype is also covered. This is not a side-by-side spreadsheet. It's a call.

---

## How it works — just 3 steps

Invoke the skill with anything like "help me compare these two offers" / "两个 offer 该选哪个" / "which offer should I take" and you go through exactly:

1. **Paste both offers** — Company / Role / Level / Location / TC breakdown (Base + Bonus + RSU with 4-year vest schedule + Sign-on) for each. Missing pieces are batched into one follow-up, not drip-fed one at a time.
2. **Answer priorities & context** (optional but strongly recommended) — pick 2–3 priorities (💰 comp · 📈 growth · 🤖 AI · 🏢 stability · 🌍 lifestyle · 🚀 promo speed · 🎯 resume value · 🔁 future mobility) + tell me about visa, burnout, family, current base, deadline.
3. **HTML decision report auto-opens** — a single-file report is generated to `~/Desktop/Claude skills/offer-compare-<A>-vs-<B>-<YYYYMM>.html` and pops open in your browser. Inside: Verdict, Assumptions block, §1 Offer Breakdown, §2 Dimension Compare (7 axes), §3 Hidden Signals (5), §4 Risk Analysis, §5 Recommendation. Bilingual EN / 中文 toggle + Export PDF / Markdown baked in.

Then loop: change an assumption / add a new priority → the skill regenerates the report. Everything gets cached to `offer-bank/` so "the A vs B thing from last time" is a lookup, not a re-paste.

---

## Decision Report · the 5-section framework

Every wizard run ends with a single-file HTML report at `~/Desktop/Claude skills/offer-compare-<A>-vs-<B>-<YYYYMM>.html`. Fixed 5-section spine, plus a Verdict + Assumptions preamble:

| # | Section | What it answers |
|---|---------|-----------------|
| — | **Verdict** | One-line recommendation (**A** / **B** / **walk-away**) + ⭐ conviction score. Never neutral. |
| — | **Assumptions** | Every assumption listed explicitly (RSU vest schedule · FX rate · bonus target · stock volatility). If any is wrong, re-run. |
| **1** | **Offer Breakdown** | Base / Bonus / RSU / Sign-on / 4-year TC **range** / equity risk / company stability, side-by-side table. |
| **2** | **Dimension Compare** | 7-axis scoreboard: 💰 Comp · 📈 Growth · 🤖 AI Exposure · 🏢 Company Strength · 👤 Manager/Team Risk · 🔁 Promo Speed · 🌍 Lifestyle. |
| **3** | **Hidden Signals** | 5 signals people miss: front-loaded vs long-term upside · uncertainty · resume value · switch-out difficulty. |
| **4** | **Risk Analysis** | 4–6 explicit risks per offer, grouped by equity / role / team / market / life. |
| **5** | **Recommendation** | Clear pick + tradeoff explanation + "If you are X → A / If you are Y → B" fork. |

The report supports **EN / 中文 toggle**, **Export to PDF**, and **Export to Markdown**. Spec: [`frameworks/offer-compare-report.md`](frameworks/offer-compare-report.md) · skeleton: [`examples/offer-compare-template.html`](examples/offer-compare-template.html).

---

## Three iron rules

1. **Never neutral.** One clear pick is mandatory, backed by an "If X → A / If Y → B" fork so a second archetype is also covered. "Both look great, up to you" is banned.
2. **Numbers as ranges + explicit assumptions.** 4-year TC is always `$X ~ $Y` (RSU refresh on/off · stock ±30% · bonus min/max). Every assumption is listed in the Assumptions block at the top. Single-point numbers are this tool's biggest credibility killer.
3. **Never fabricate insider signals.** Company signals (team health / manager style / promo speed) may only come from public data + what the user provided, and must be tagged "inferred from ___". Numbers the user didn't give (base, share price, current comp) are marked `[needs user input]`, never guessed.

---

## File Structure

```
offer-compare-skill/
├── SKILL.md                              # Entry · routing · 3-step flow · 3 iron rules
├── prompts/                              # 5 internal flows
│   ├── offer-breakdown.md                # §1
│   ├── dimension-compare.md              # §2
│   ├── hidden-signals.md                 # §3
│   ├── risk-analysis.md                  # §4
│   └── recommendation.md                 # §5
├── frameworks/                           # Reusable frameworks / rubrics
│   ├── dimension-rubric.md               # 7-axis scoring rubric + weights
│   ├── hidden-signals-dictionary.md      # Detection rules for the 5 hidden signals
│   ├── risk-taxonomy.md                  # 5 risk categories × common patterns
│   └── offer-compare-report.md           # Final HTML report — spec + mandatory footer
├── examples/                             # Reference skeleton (no personal data)
│   └── offer-compare-template.html
└── offer-bank/                           # Local cache of past decisions
    ├── _index.md                         # Index
    └── _template.md                      # Starter template for new decisions
```

---

## How it thinks

- **Two offers is a decision, not a table.** People who paste "here are two offers" usually already have a gut feel — they want someone honest enough to say it out loud. This skill's job is to be that voice, not to hide behind neutrality.
- **The dimension that decides is usually not comp.** Comp dominates the spreadsheet, but the *decisive* dimension is often AI exposure, resume value, or switch-out difficulty. §2 and §3 exist to surface that.
- **4-year TC without a range is a lie.** RSU refresh assumption alone can swing TC by 30–40%. Ranges force the tradeoff into the open.
- **Every offer has hidden risk. Both.** §4 must be filled for both offers — including the recommended one. Otherwise §5 looks like a sales pitch, not a decision.

---

## Related skills

Pairs with these — the full job-hunt loop:

- [offer-toolkit-skill](https://github.com/yanliudesign/offer-toolkit-skill) — the all-in-one bundle (Search · JD · Resume · BQ · Compare · Negotiate)
- [job-description-skill](https://github.com/yanliudesign/job-description-skill) — Job Description decoder + should-I-apply
- [resume-builder-skill](https://github.com/yanliudesign/resume-builder-skill) — Resume Builder & Beautifier (11 print-ready templates)
- [Behavior-question-skill](https://github.com/yanliudesign/Behavior-question-skill) — Behavioral interview / story bank
- [salary-negotiation](https://github.com/yanliudesign/salary-negotiation) — Negotiate the offer you picked here

```
See a dream job → JD Skill (decode · match · should-I-apply)
                     ↓ decide to apply
                 Resume Skill (tailor + polish)
                     ↓ get the interview
                 BQ Skill (mine stories · mock interview)
                     ↓ get the offer(s)
             Offer Compare (this skill — pick one, opinionated)
                     ↓ decided
             Salary Skill (diagnose · script · counter · sign)
```

---

## License

MIT — fork it, remix it, ship your own version.

Created by [Dreameryanyan](https://www.linkedin.com/in/yanliudesign/) · [LinkedIn](https://www.linkedin.com/in/yanliudesign/) · [X](https://x.com/yanliudreamer) · [Xiaohongshu](https://www.xiaohongshu.com/user/profile/5b2afdf311be104ac3c22931)
