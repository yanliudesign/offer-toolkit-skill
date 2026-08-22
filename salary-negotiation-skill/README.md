<div align="center">

[中文](./README.zh.md) · **English**

# 💰 Salary Negotiation Skill

---

**Turn any offer letter into an executable negotiation playbook — in 3 steps.**

[![License](https://img.shields.io/badge/LICENSE-MIT-4c8bf5?style=flat-square&labelColor=333)](./LICENSE)
[![Version](https://img.shields.io/badge/VERSION-1.0.0-2ea44f?style=flat-square&labelColor=333)]()
[![Stars](https://img.shields.io/github/stars/yanliudesign/salary-negotiation?style=flat-square&label=STARS&color=e37f2c&labelColor=333)](https://github.com/yanliudesign/salary-negotiation/stargazers)

[![Claude Code](https://img.shields.io/badge/Claude_Code-Skill-d97757?style=flat-square&labelColor=1a1a1a&logo=anthropic&logoColor=white)](https://claude.ai/code)
[![Codex](https://img.shields.io/badge/Codex-Skill-2ea44f?style=flat-square&labelColor=1a1a1a)]()
[![OpenCode](https://img.shields.io/badge/OpenCode-Skill-4c8bf5?style=flat-square&labelColor=1a1a1a)]()
[![OpenClaw](https://img.shields.io/badge/OpenClaw-Skill-8b5cf6?style=flat-square&labelColor=1a1a1a)]()
[![Hermes](https://img.shields.io/badge/Hermes-Skill-e879a8?style=flat-square&labelColor=1a1a1a)]()

</div>

> 📦 Part of the **[offer-toolkit-skill](https://github.com/yanliudesign/offer-toolkit-skill)** — the full job-hunt bundle (Search · JD · Resume · BQ · Compare · Negotiate). Install the bundle to get all six in one shot.

An agent skill for salary negotiation. Modeled after a former FAANG recruiter + compensation strategist. Drop in your offer letter and it hands back an HTML negotiation playbook telling you: which line items have real leverage, what your actual power is (and isn't), what to ask for first, exactly what to say on the phone and in email, how the recruiter will push back and how to counter each pushback twice, and — most important — the three stop-lines (SIGN / WALK / FREEZE) that keep the negotiation from going forever until the offer disappears. This is not "here's some generic advice about being confident." It's a simulation of real negotiation dynamics.

---

## How it works — just 3 steps

Invoke the skill with anything like "help me negotiate this offer" / "谈薪" / "review my package" and you go through exactly:

1. **Paste the offer** — Company / Role / Level / Base / RSU (total + vest curve + ref price) / Sign-on / Bonus / Location / Deadline.
2. **Answer 5 context questions** — competing offers / deadline flex / seniority signal / risk tolerance / top-2 priorities (Cash · Equity · Title · Location · WLB — pick 2).
3. **HTML playbook auto-opens** — a single-file Negotiation Playbook is generated to `~/Desktop/Claude skills/salary-negotiation-<slug>.html` and pops open in your browser. Inside: TL;DR verdict, diagnosis, leverage map, prioritized ask table, phone + email scripts, 3-pushback counter-simulation (2 rounds each), and the 3 stop-lines.

Then loop: paste the recruiter's actual reply back into the conversation → the skill updates the counter-simulation for round 2.

---

## Negotiation Playbook · the 6-section framework

Every wizard run ends with a single-file HTML report at `~/Desktop/Claude skills/salary-negotiation-<slug>.html`. Fixed 6-section spine, plus a TL;DR preamble and a key-metrics block:

| # | Section | What it answers |
|---|---------|-----------------|
| — | **TL;DR · one-minute verdict** | Sign / Counter / Walk. Priority-ordered ask in one line. |
| — | **Key metrics** | TC vs market P50/P75, leverage summary, deadline countdown. |
| **1** | **Offer Diagnosis** | Base / RSU / Sign-on / Bonus each tagged **LOW / MEDIUM / HIGH** leverage vs market. Every number sourced to Levels.fyi / Blind / competing offer. |
| **2** | **Leverage Map** | Your power (competing offers, timing, scarcity) · recruiter's power (budget, level cap, pool) · your blind spots. |
| **3** | **Strategy** | Modality A/B/C/D (aggressive double-front / single-point / light-touch / sign-as-is) + priority-ordered ask table with target and floor per line item. |
| **4** | **Scripts** | 📞 phone script (Beat 1–4, EN + ZH, word-for-word) + 📧 email version + recruiter's 3 typical first replies. |
| **5** | **Counter Simulation** | 3 pushbacks × 2 rounds each ("this is our best" / "budget is fixed" / "reconsider the pool") with per-round stop-signals. Most failures happen in round 2, not round 1. |
| **6** | **Final Recommendation** | What to ask / what NOT to push / **3 stop-lines** (SIGN / WALK / FREEZE) with concrete numbers + emergency protocol (rescind risk / exploding offer / deadline squeeze). |

The report supports **Export to PDF** and **Copy Scripts**. Spec: [`frameworks/negotiation-report.md`](frameworks/negotiation-report.md) · skeleton: [`examples/negotiation-report-template.html`](examples/negotiation-report-template.html).

---

## Five iron rules

1. **Never fabricate comp data.** All P50/P75 must trace to Levels.fyi / Blind / user-provided offers. Mark `[需查]` if not found.
2. **Numbers as ranges, not points.** "$220–230K" not "$225K".
3. **Every script line must be word-for-word usable.** No "you might say something like…".
4. **Counter Simulation must go 2 rounds per pushback.** Most failures happen in round 2, not round 1.
5. **Must include a stop-line.** SIGN / WALK / FREEZE, with concrete numbers. No stop-line = negotiation goes forever = offer disappears.

---

## File Structure

```
salary-negotiation-skill/
├── SKILL.md                         # Entry · routing · 3-step flow · 5 iron rules
├── prompts/                         # 6 internal flows
│   ├── offer-diagnosis.md           # §1
│   ├── leverage-map.md              # §2
│   ├── negotiation-strategy.md      # §3
│   ├── script-generator.md          # §4
│   ├── counter-simulation.md        # §5
│   └── final-recommendation.md      # §6
├── frameworks/                      # Reusable frameworks / rubrics
│   ├── comp-benchmarks.md           # How to look up market data (Levels.fyi, Blind…)
│   ├── leverage-heuristics.md       # LOW/MED/HIGH rules per component
│   ├── negotiation-tactics.md       # Anchoring · silence · reframe · brackets · 24-hour rule
│   ├── recruiter-playbook.md        # 20 recruiter phrases × 20 responses
│   └── negotiation-report.md        # Final HTML report — spec + mandatory footer
├── examples/                        # Reference skeleton (no personal data)
│   └── negotiation-report-template.html
└── deal-bank/                       # Local cache of negotiated deals (gitignored)
    ├── _index.md                    # Index
    └── _deal-template.md            # Starter template for new deals
```

---

## How it thinks

- **An offer is a first draft, not a final answer.** Recruiters expect a counter on most senior offers. The question is *how much* leverage you actually have — which is what §1 and §2 exist to answer honestly.
- **Leverage is component-specific.** Base moves less than RSU. RSU refreshers move less than sign-on. Sign-on moves more than bonus. Sequence the ask accordingly (§3).
- **Every pushback has a canonical script.** "This is our best" / "budget is fixed" / "we'll reconsider the pool" — these are not personal, they are template moves. §5 gives you the countermove for each, twice.
- **The failure mode is not asking too much — it's negotiating forever.** Every playbook ends with a stop-line so you know when to sign, when to walk, and when to freeze the conversation.

---

## Related skills

Pairs with the full loop — get the offer through Search → JD → Resume → BQ, compare when needed, then close it here:

- [offer-toolkit-skill](https://github.com/yanliudesign/offer-toolkit-skill) — the all-in-one bundle (Search · JD · Resume · BQ · Compare · Negotiate)
- [job-description-skill](https://github.com/yanliudesign/job-description-skill) — Job Description decoder + should-I-apply
- [resume-builder-skill](https://github.com/yanliudesign/resume-builder-skill) — Resume Builder & Beautifier (11 print-ready templates)
- [Behavior-question-skill](https://github.com/yanliudesign/Behavior-question-skill) — Behavioral interview / story bank
- [offer-compare-skill](https://github.com/yanliudesign/offer-compare-skill) — Compare multiple offers before negotiating the winner

```
See a dream job → JD Skill (decode · match · should-I-apply)
                     ↓ decide to apply
                 Resume Skill (tailor + polish)
                     ↓ get the interview
                 BQ Skill (mine stories · mock interview)
                         ↓ get the offer(s)
                    multiple offers → Offer Compare (pick one)
                         ↓
                     Salary Skill (diagnose · script · counter · sign)
```

---

## License

MIT — fork it, remix it, ship your own version.

Created by [Dreameryanyan](https://www.linkedin.com/in/yanliudesign/) · [LinkedIn](https://www.linkedin.com/in/yanliudesign/) · [X](https://x.com/yanliudreamer) · [Xiaohongshu](https://www.xiaohongshu.com/notification)
