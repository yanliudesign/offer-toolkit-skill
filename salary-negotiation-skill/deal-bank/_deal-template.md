# {{COMPANY}} — {{ROLE}} ({{LEVEL}})

## Frontmatter

```yaml
company: {{COMPANY}}
role: {{ROLE_TITLE}}
level: {{LEVEL}}                  # e.g. E5 / L5 / IC5 / Senior
location: {{LOCATION}}
received_at: {{YYYY-MM-DD}}
deadline: {{YYYY-MM-DD}}
status: received                  # received / diagnosed / countered / re-offered / accepted / walked / rescinded
report: ~/Desktop/Claude skills/salary-negotiation-{{slug}}.html
```

## Offer components (v1 · original)

| Component | Value | Notes |
|---|---|---|
| Base | $ | annual |
| RSU total | $ | over N years |
| RSU curve | 25/25/25/25 or 10/20/30/40 etc. | |
| RSU ref price | $ | grant-date reference share price |
| Sign-on | $ | one-time or split |
| Sign-on clawback | 12/24 months | |
| Annual bonus target | % | of base |
| Bonus guaranteed Y1? | Y / N | |
| Refresh policy | | e.g. annual refresh ~30% |
| Relocation | $ | lump / actual-cost |
| Y1 TC | $ | computed |
| 4-yr avg TC | $ | computed |

## Context snapshot

- Competing offers: [list or "none"]
- Deadline: [date, recruiter口头 vs email]
- Seniority level: [user's own view — right / feels down-leveled / feels up-leveled]
- Risk tolerance: [conservative / moderate / aggressive]
- Top-2 priorities: [cash / equity / title / location / WLB — pick 2]

## Diagnosis summary

| Component | Position | Leverage | One-liner |
|---|---|---|---|
| Base | Below P50 / At P50 / At P75 / Above P75 | HIGH / MED / LOW | |
| RSU | " | " | |
| Sign-on | " | " | |
| Bonus | " | " | |

**Overall Leverage**: HIGH / MED / LOW → Modality [A/B/C/D]

## Strategy summary

- Priority 1: [component + ask range]
- Priority 2: [component + ask range]
- Total TC uplift target: +X% (from $Y → $Z)

## SIGN LINE
> Recruiter gives [X] AND [Y] → sign immediately.

## WALK LINE
> Recruiter refuses to [Z] AND [Q] → walk.

## FREEZE LINE
> Recruiter says [P] OR you feel [emotion] → 24-hour pause.

---

## Rounds (append after each recruiter reply)

### Round 0 · Initial offer (received {{YYYY-MM-DD}})
Recruiter (channel: email / call):
> "..."

### Round 1 · Your counter (sent {{YYYY-MM-DD}}, channel: email / call)
Your ask:
> "..."

Recruiter response ({{YYYY-MM-DD}}):
> "..."

Diagnosis of response: [best-offer / budget-fixed / reconsider-pool / new-mid-number / accept-partial]

### Round 2 · [your response / recruiter's revised offer]
...

---

## Outcome

- Status: [accepted / walked / rescinded / pending]
- Final TC: $ (delta vs initial: +X% / -Y%)
- Report file: `~/Desktop/Claude skills/salary-negotiation-{{slug}}.html`
- Lessons for next negotiation: [1-3 lines, honest post-mortem]
