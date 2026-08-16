# Job Hunt List

A standalone agent skill for turning a resume, target direction, seed JD, or a pile of job links into a searchable HTML job database.

## What it does

- Builds a focused search profile and complementary query matrix
- Finds public roles across LinkedIn, company career pages, and web search
- Deduplicates by canonical job id / URL
- Separates verified facts, partial evidence, inference, and unknowns
- Deep-scores only roles with enough visible JD evidence
- Keeps the complete qualified candidate pool instead of collapsing it into a shortlist
- Generates a self-contained HTML report with search, filters, domain tags, reasons, gaps, and direct job links
- Updates an existing list while preserving first-seen history

## What it never does

- Apply for jobs, fill forms, or send messages
- Ask for passwords, verification codes, cookies, or session tokens
- Bypass login walls, CAPTCHAs, rate limits, or robots restrictions
- Invent salary, posted date, workplace policy, visa policy, or JD requirements

## Trigger examples

- "Build me a job hunt list from my resume."
- "Find all matching Principal Product Designer roles and make a searchable report."
- "Turn these LinkedIn links into a deduplicated job tracker."
- "Update last week's job list with newly posted AI design roles."

## Install

Copy the entire `job-hunt-list/` directory into your agent skills directory. The folder is self-contained and does not require the rest of Offer Toolkit.
