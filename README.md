<div align="center">

[中文](./README.zh.md) · **English**

# 🧰 Offer Toolkit

---

**Six job-hunt tools in one agent skill pack — Search · JD · Resume · BQ · Compare · Negotiate.**

[![License](https://img.shields.io/badge/LICENSE-MIT-4c8bf5?style=flat-square&labelColor=333)](./LICENSE)
[![Version](https://img.shields.io/badge/VERSION-1.2.0-2ea44f?style=flat-square&labelColor=333)]()
[![Skills](https://img.shields.io/badge/SKILLS-6-2ea44f?style=flat-square&labelColor=333)]()
[![Stars](https://img.shields.io/github/stars/yanliudesign/offer-toolkit-skill?style=flat-square&label=STARS&color=e37f2c&labelColor=333)](https://github.com/yanliudesign/offer-toolkit-skill/stargazers)
[![Disclaimer](https://img.shields.io/badge/DISCLAIMER-Not_professional_advice-6b7280?style=flat-square&labelColor=333)]()

[![Claude Code](https://img.shields.io/badge/Claude_Code-Skill-d97757?style=flat-square&labelColor=1a1a1a&logo=anthropic&logoColor=white)](https://claude.ai/code)
[![Codex](https://img.shields.io/badge/Codex-Skill-2ea44f?style=flat-square&labelColor=1a1a1a)]()
[![OpenCode](https://img.shields.io/badge/OpenCode-Skill-4c8bf5?style=flat-square&labelColor=1a1a1a)]()
[![OpenClaw](https://img.shields.io/badge/OpenClaw-Skill-8b5cf6?style=flat-square&labelColor=1a1a1a)]()
[![Hermes](https://img.shields.io/badge/Hermes-Skill-e879a8?style=flat-square&labelColor=1a1a1a)]()

</div>

Six job-hunting tools bundled as an agent skill pack. Use the whole thing, or just the piece you need — each sub-folder works on its own.

```
0  Discover opportunities → job-hunt-skill           Build a deduplicated, searchable HTML job list.
1  See a job you want    →  job-description-skill    Decode the JD, get an Offer Strategy report.
2  Decide to apply       →  resume-skill             Tailor & polish. 11 print-ready templates.
3  Land the interview    →  bq-skill                 Mine stories, build a story bank, prep BQs.
4  Compare offers        →  offer-compare-skill      Compare TC, growth, risk, and get a clear recommendation.
5  Negotiate the package →  salary-negotiation-skill Diagnose leverage, generate scripts, and set stop-lines.
```

## What's inside

<table>
<thead><tr><th width="30%">Sub-skill</th><th>What it does</th></tr></thead>
<tbody>
<tr><td><strong><a href="job-hunt-skill/">job&#8209;hunt&#8209;skill</a></strong></td><td>Give it a resume, target direction, seed JD, or existing job links. It searches public sources, deduplicates candidates, separates verified facts from inference, and generates a searchable HTML job list. It discovers and analyzes; it never applies for you.</td></tr>
<tr><td><strong><a href="job-description-skill/">job&#8209;description&#8209;skill</a></strong></td><td>Give it a JD and your resume. You get back an HTML report telling you: whether this job is worth applying to, how well you match it, where the gaps are, what you'll probably be asked in interviews, whether the salary is reasonable, and what to do over the next six weeks.</td></tr>
<tr><td><strong><a href="resume-skill/">resume&#8209;skill</a></strong></td><td>Polishes an existing resume, pulls one in from LinkedIn, or builds one from scratch by chatting with you. The content then flows into <strong>11 print-ready templates</strong> (Classic-ATS, Ledger, Tech Compact, Modern Sidebar, Pillar, Elegant Serif, Atelier, Timeline, Swiss, Executive, Color-block). Each render gives you two files: one that prints straight to PDF, and one you can click on in the browser to edit.</td></tr>
<tr><td><strong><a href="bq-skill/">bq&#8209;skill</a></strong></td><td>Instead of handing you canned answers, it helps you dig your real past experiences out and organize them into a story bank you can reuse. It asks about your experience step by step, uses STAR/CAR to shape each story, tags them ("took ownership", "handled ambiguity", etc.), and saves them in English and Chinese — so next time you get a different behavioral question, the same story still works. It can also read a JD, predict the 20 questions that company is likely to ask, and walk you through prep for each one.</td></tr>
<tr><td><strong><a href="offer-compare-skill/">offer&#8209;compare&#8209;skill</a></strong></td><td>Compares two or more offers across four-year TC, growth, AI exposure, company and team risk, promotion, lifestyle, resume value, and future mobility. It produces an HTML Offer Decision Report with an explicit recommendation.</td></tr>
<tr><td><strong><a href="salary-negotiation-skill/">salary&#8209;negotiation&#8209;skill</a></strong></td><td>Diagnoses Base, RSU, Sign-on, and Bonus leverage; builds a negotiation strategy; writes ready-to-use phone and email scripts; simulates recruiter pushback; and defines clear sign, walk, and stop-lines in an HTML Negotiation Playbook.</td></tr>
</tbody>
</table>

## Examples

<table>
<tr>
<td width="33%" align="center"><h2>01 · JOB DISCOVERY</h2></td>
<td width="34%" align="center"><h2>02 · JD ANALYSIS</h2></td>
<td width="33%" align="center"><h2>03 · RESUME</h2></td>
</tr>
<tr>
<td valign="top"><img src="docs/showcase/en/01-job-discovery-v2.png" alt="job-hunt-skill report overview" width="100%"></td>
<td valign="top"><img src="docs/showcase/en/02-jd-analysis.png" alt="job-description-skill Offer Strategy Report preview" width="100%"></td>
<td valign="top"><img src="docs/showcase/en/03-resume-v2.png" alt="resume-skill template gallery" width="100%"></td>
</tr>
<tr>
<td valign="top"><sub>Ranked opportunities, evidence labels, and filters.</sub></td>
<td valign="top"><sub>Role fit, gaps, interview predictions, compensation, and action plan.</sub></td>
<td valign="top"><sub>Eleven print-ready layouts with browser editing and PDF export.</sub></td>
</tr>
<tr>
<td align="center"><h2>04 · BQ PREP</h2></td>
<td align="center"><h2>05 · OFFER COMPARE</h2></td>
<td align="center"><h2>06 · NEGOTIATION</h2></td>
</tr>
<tr>
<td valign="top"><img src="docs/showcase/en/04-bq-prep-v2.png" alt="bq-skill behavioral interview prep report preview" width="100%"></td>
<td valign="top"><img src="docs/showcase/en/05-offer-compare-v2.png" alt="offer-compare-skill decision report preview" width="100%"></td>
<td valign="top"><img src="docs/showcase/en/06-salary-negotiation-v2.png" alt="salary-negotiation-skill playbook preview" width="100%"></td>
</tr>
<tr>
<td valign="top"><sub>Top 20 questions with STAR templates and editable model answers.</sub></td>
<td valign="top"><sub>Four-year compensation, career upside, risks, and a clear recommendation.</sub></td>
<td valign="top"><sub>Leverage diagnosis, counter strategy, scripts, and decision boundaries.</sub></td>
</tr>
</table>

## Four rules the sub-skills share

1. **Never fabricate.** Every experience, number, and title comes from what the user actually said. Sharpen weak content, don't invent it. Verify numbers.
2. **Ask only what changes the answer.** Follow each child skill's stated one-at-a-time or batched intake cadence; never turn the conversation into a sprawling questionnaire.
3. **Structure first, render second.** Get the content into a standard shape and confirm it before generating anything.
4. **Never apply on the user's behalf.** Search can be automated; submitting forms and sending messages remain user actions.

## Install

Drop the whole `offer-toolkit-skill/` folder into your skills directory (e.g. `~/.claude/skills/` or VS Code's prompts folder). All six sub-skills get picked up.

Only want one? Copy just that sub-folder — each one is self-contained.

> 🔒 **Your data stays on your machine.** JDs, resumes, and stories are read by the model in the moment and written back to your local disk — nothing gets shipped to a server or trained on.

### Try it in 30 seconds

Once installed, just paste any of these into your Claude Code / VS Code chat:

- *"Should I apply to this?"* + paste a JD link (or full text)
- *"Use this JD and my resume to find matching LinkedIn jobs"*
- *"Beautify my resume"* + drag in a PDF
- *"Prep me for behavioral interviews"*
- *"Compare these two offers and tell me which one to take"*
- *"Help me negotiate this offer"*

The router picks the right sub-skill. You get an HTML report / resume / story bank on your desktop, ready to open.

## Trigger phrases

| You say | Runs |
|---|---|
| *"Find me a job"* / *"Search LinkedIn for matching roles"* / *"Use job-hunt-skill with my resume"* | job-hunt-skill |
| Paste a JD / *"should I apply to this?"* / *"help me with this job"* | job-description-skill |
| *"Beautify my resume"* / *"build me one from scratch"* / upload PDF / paste LinkedIn | resume-skill |
| *"Prep me for behavioral interviews"* / *"tell me about a time…"* / *"mine a story"* | bq-skill |
| *"Compare these offers"* / *"which offer should I take?"* / *"calculate four-year TC"* | offer-compare-skill |
| *"Help me negotiate"* / *"write a counter offer"* / *"can I ask for more RSU?"* | salary-negotiation-skill |
| *"Help me find a job"* / hand over JD + resume at once | Top-level [SKILL.md](SKILL.md) routes you to the right one |

## Layout

```
offer-toolkit-skill/
├── SKILL.md                        # Router: intent → sub-skill
├── README.md / README.zh.md
├── LICENSE                         # MIT
├── job-hunt-skill/                 # ⓪ Complete searchable job discovery list
├── job-description-skill/          # ① JD decoder + Offer Strategy report
├── resume-skill/                   # ② Resume builder + 11 templates
├── bq-skill/                       # ③ Behavioral interview / story bank
├── offer-compare-skill/            # ④ Multi-offer comparison + decision report
└── salary-negotiation-skill/       # ⑤ Package negotiation + scripts
```

Each sub-folder has its own `SKILL.md`, README, prompts, frameworks, and templates.

## Standalone repos

These six also live as separate repos and get maintained there:

- [job-hunt-skill](https://github.com/yanliudesign/job-hunt-skill)
- [job-description-skill](https://github.com/yanliudesign/job-description-skill)
- [resume-builder-skill](https://github.com/yanliudesign/resume-builder-skill)
- [Behavior-question-skill](https://github.com/yanliudesign/Behavior-question-skill)
- [offer-compare-skill](https://github.com/yanliudesign/offer-compare-skill)
- [salary-negotiation](https://github.com/yanliudesign/salary-negotiation)

This bundle just puts them together with a top-level router.

## License

MIT — fork it, remix it, ship your own version.

Created by [Dreameryanyan](https://www.linkedin.com/in/yanliudesign/) ·
[LinkedIn](https://www.linkedin.com/in/yanliudesign/) ·
[X](https://x.com/yanliudreamer) ·
[Xiaohongshu](https://www.xiaohongshu.com/notification)
