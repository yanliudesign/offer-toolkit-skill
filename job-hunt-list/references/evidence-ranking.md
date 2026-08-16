# Evidence and Ranking Rules

## Evidence hierarchy

Use the strongest available source for each field:

1. Official company job page or visible full job description
2. Public LinkedIn job page
3. Public search-result snippet
4. Title/company inference

Evidence is field-specific. A verified title does not make salary, workplace, posted date, or job status verified.

## Field states

| State | Meaning | Display rule |
|---|---|---|
| `verified` | Directly visible in a public source | Display value |
| `partial` | Visible only in a truncated summary | Display value with limited-evidence note when material |
| `inferred` | Derived from title, company, or adjacent evidence | Label as directional inference |
| `unknown` | No reliable evidence | Leave blank or display `待核验` |

Never convert `unknown` into a plausible value.

## Deep match scoring

Only score roles whose JD requirements are sufficiently visible.

1. Split the JD into Must Have, Nice to Have, Hidden Signals, and Hard Gates.
2. Score each requirement against resume evidence:
   - `1.0`: direct evidence with project, scope, result, or concrete detail
   - `0.5`: adjacent evidence or unsupported claim
   - `0.0`: no evidence
3. Calculate:

```text
Match = 0.60 × MustHave + 0.20 × NiceToHave + 0.20 × HiddenSignalFit
```

Display a range of ±5–8 percentage points, not a decimal point score.

Caps:

- One Must Have scored `0`: maximum 75%
- Two or more Must Haves scored `0`: maximum 55%
- Failed Hard Gate: exclude from main list and summarize the exclusion
- Full JD unavailable: no match percentage; use `未深评`

## Directional ranking

For roles without full JD, rank from visible evidence only:

- Title / level fit: 0–30
- Resume capability overlap: 0–30
- Domain / scope proximity: 0–20
- Freshness: 0–10
- User preference: 0–10

This score is internal. Do not present it as a verified match percentage.

## Reason and gap writing

For deep-reviewed roles:

- `Why it fits` cites two concrete resume facts.
- `Main gap` names the strongest missing or weaker requirement.

For unreviewed roles:

- Label the reason `方向性理由`.
- State which title, domain, or scope signal makes it worth reviewing.
- Label the gap as something to verify, not a known deficiency.
