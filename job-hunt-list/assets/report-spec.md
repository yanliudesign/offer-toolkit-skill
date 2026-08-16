# Job Hunt List HTML Contract

Generate one self-contained HTML file with inline CSS and JavaScript. Do not require a build step, external framework, server, or remote font.

## Data shape

Each normalized job record should support:

```js
{
  id: "",
  title: "",
  company: "",
  url: "",
  source: "",
  firstSeen: "",
  lastChecked: "",
  posted: "",
  postedEvidence: "unknown",
  location: "",
  workMode: "",
  salary: "",
  domains: [],
  reviewStatus: "discovered",
  match: "未深评",
  reason: "",
  reasonType: "directional",
  gap: "",
  gapType: "directional",
  priority: 0
}
```

Keep source data in one clearly named JavaScript collection so a later run can parse and update it.

## Table

Use six columns:

1. 职位 / 公司 / 推荐理由 / Gap
2. 发布日期
3. 地点 / 工作方式
4. 薪资范围
5. 匹配度
6. Open link icon

Place searchable domain tags immediately beside the company name. Do not show job ids or Tier A/B badges in the visible row.

Unknown salary should be an empty cell. Use `待核验` for unknown date, location, or work mode when an empty cell would be ambiguous.

## Interactions

- Search title, company, domain tags, reason, gap, location, salary, and posted information.
- Include filters for all, deep reviewed, priority, AI / Agentic, Principal, and Staff when those categories exist.
- Update visible count after every search/filter change.
- Open job links in a new tab with `rel="noreferrer"` or `rel="noopener"`.
- Make keyboard focus visible.
- Respect `prefers-reduced-motion`.

## Visual hierarchy

- Treat this as a dense operational tool, not a marketing landing page.
- Keep the first viewport focused on search context and the table.
- Use restrained surfaces, compact rows, and strong column headers.
- Domain tags need distinct color families but must remain secondary to title and company.
- Keep labels square or lightly rounded; avoid decorative pill overload.
- Preserve usable horizontal scrolling on narrow screens.

## Evidence copy

- Deep evidence label: `为什么适合你`
- Directional label: `方向性理由`
- Gap label: `需要补足的 Gap`
- Unknown match: `未深评`
- Unknown field: `待核验`

Add a visible evidence note explaining that unreviewed does not mean unqualified and unknown values were not guessed.

## Static validation

Check all of the following before delivery:

- Inline script parses with `new Function(script)`.
- Rendered or generated row count matches unique job count.
- Every row has six cells.
- No `.tier-badge` element exists by default.
- Search index includes domains, reason, and gap.
- Salary values appear only for records with evidence.
