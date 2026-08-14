# ATS checklist (100 points)

Score the draft resume before delivery. Require **≥ 95**.

## Parseability (40)

| Pts | Criterion |
|----:|-----------|
| 10 | Single-column haider template layout (tabular* entry rows OK; no multi-column body or text boxes) |
| 10 | Standard section headings only (PROFESSIONAL SUMMARY, EXPERIENCE, PROJECTS, EDUCATION, SKILLS) |
| 8  | Contact info at top with name, phone, email, location, plus LinkedIn/GitHub/portfolio from reference.md (icons + `\texttt` OK) |
| 6  | No photos/charts; Font Awesome + section rules from the template are allowed; content still readable as plain text |
| 6  | Dates and titles clearly paired via `\resumeSubheading` / `\resumeProjectHeading` (Company/Title/Dates adjacent) |

## Keyword alignment (40)

| Pts | Criterion |
|----:|-----------|
| 15 | ≥ 90% of JD **must-have** hard skills appear verbatim in Skills and/or bullets |
| 10 | Professional Summary includes role title + top 3–5 JD terms |
| 10 | Experience bullets reuse JD verbs/tools where truthful |
| 5  | Nice-to-haves included when supported by references (no fabrication) |

## Content quality (20)

| Pts | Criterion |
|----:|-----------|
| 8  | Every experience/project bullet is Action + scope + tech + **a numeral** + result; one outcome per bullet |
| 6  | No first-person pronouns; no fluff ("responsible for", "team player"); no action verb used 3+ times |
| 6  | One page; early-career body **~500 words** (470–540); past tense for old roles, present for current |

## Scoring

1. Award points only when the criterion is clearly met.
2. If keyword alignment fails on a must-have the candidate **does** have in references, fix the TeX and re-score.
3. If a must-have is **not** in references, do not invent it; note the gap to the user and score honestly (may stay below 95 — tell the user which skills are missing).
4. After this score, run [content-checklist.md](content-checklist.md). ATS ≥ 95 is not enough if numbers, verb repeats, or length fail.

Report as: `ATS self-score: NN/100` plus a one-line list of deductions if any.
