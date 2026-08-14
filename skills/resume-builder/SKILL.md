---
name: resume-builder
description: >-
  Builds an ATS-optimized resume as a LaTeX (.tex) file tailored to a job
  description, using facts from reference.md (contact, GitHub, website/portfolio,
  github_projects, skills, experience, education, projects). Enforces content
  checks that hold on any reviewer: quantified bullets, unique action verbs
  (max 2 uses), ~500-word one-page length. Use when the user pastes a JD,
  asks to tailor a resume, generate a resume summary, or produce resume TeX
  / ATS output.
disable-model-invocation: true
---

# Resume Builder

Turn a job description + local reference facts into a single-column ATS-friendly `.tex` resume. Target ATS keyword / parse score **above 95%** and a passing content self-check (numbers, verb variety, length) so the file holds up on any reviewer.

**Core principle: tailor, don't dump.** `reference.md` is a source pool — include only what strengthens fit for *this* JD. Omit unrelated skills, projects, bullets, and links.

Generated `.tex` files go to the **invocation cwd**, not this skill directory.

## Inputs

1. **Job description** — pasted by the user (required).
2. **Reference facts** — always read [reference.md](reference.md) before writing. Do not invent employment, dates, degrees, employers, or repos.
   - If `reference.md` is missing, copy [reference.template.md](reference.template.md) → `reference.md` and ask the user to fill it.

Expected sections in `reference.md` (YAML blocks under each heading):
- **Personal** — contact, `github` / `website` / `portfolio` / `linkedin`, `github_projects`, strengths
- **Skills** — languages, frameworks, tools, other (canonical inventory for the Skills section)
- **Experience** — roles newest first (prefer bullets/metrics that already include numerals)
- **Education** — degrees
- **Projects** — optional non-GitHub / curated projects (merged with `github_projects`)

If Personal, Skills, or Experience is empty/missing, ask the user to fill `reference.md` before generating. Never fabricate experience, repositories, or skills.

## Workflow

Copy and track:

```
Resume build:
- [ ] 1. Read reference.md
- [ ] 2. Extract JD keywords, must-haves, tools, and role title
- [ ] 3. Pick JD-relevant GitHub repos + portfolio/website links from Personal
- [ ] 4. Draft tailored Professional Summary (3–4 lines)
- [ ] 5. Collect missing metrics (pause if bullets lack numbers)
- [ ] 6. Select and rewrite bullets (one outcome, unique verb, numeral)
- [ ] 7. Build Skills section from JD ∩ Skills in reference.md
- [ ] 8. Emit .tex from templates/resume.tex
- [ ] 9. Run ATS self-check (≥ 95) and content self-check; revise
- [ ] 10. Deliver the .tex path, scores, assumed numbers, and change notes
```

### Step 1–2: Analyze

From the JD, extract:
- Exact role title
- Hard skills / tools / languages / frameworks
- Soft skills only if the JD emphasizes them
- Domain terms (e.g. fintech, B2B SaaS)
- Years / seniority signals
- Required vs nice-to-have

Map each hard requirement to evidence in `reference.md`. Prefer roles/projects with the strongest overlap.

### Step 3: Links and GitHub projects

From the **Personal** section of [reference.md](reference.md):

1. **Header links** — include `github`, `website` and/or `portfolio`, plus `linkedin` (and `other_links` only if space and JD-relevant). Use Font Awesome icons + `\texttt{...}` as in the template.
2. **GitHub projects** — rank `github_projects` by JD fit (technologies, topics, description). Select **2–4** strongest matches.
3. Merge with the **Projects** section: dedupe by name/URL; prefer the richer bullet/highlight set. Do not list the same project twice.
4. For each selected repo, write **two** ATS bullets from `description` + `highlights` + `technologies` + `metrics`, emphasizing JD keywords that are truthful. Heading = name + link + stack; **do not** put the whole story in the heading.
5. Put the repo URL next to the project name in TeX (plain URL or `\href`).
6. Skip repos with weak JD overlap to protect page length. Never invent repos not listed in `reference.md`.
7. If `status` is pre-1.0 / in development, quantify **capability** (what it manages or supports), not stars/forks.

### Step 4: Professional Summary

Write a **3–4 line** summary that:
- Opens with target role title (or closest truthful title) + years if known
- Mirrors top JD keywords naturally (no keyword stuffing)
- States 1–2 concrete strengths backed by experience, with a number if one already exists in the body
- Ends with value for *this* employer/role (domain or outcome)

Do not use first person ("I"). Do not claim skills absent from `reference.md`. Keep this block inside the overall ~500-word budget.

### Step 5: Metrics before bullets

Resume reviewers flag work described with no **hard numbers**, including entry-level.

**Bullet pattern:** `Unique action verb + what + how/tech + numeral + result`

Before writing TeX, scan selected experience + project bullets/`metrics` in `reference.md`. A bullet is quantified if it already contains a digit.

If **two or more** selected bullets have no number and no `metrics` fields, **pause and ask** (do not generate a numberless draft). Ask only what is missing, in this shape — adapt nouns to the actual work; do not reuse canned company/tool names:

1. **Volume** — Roughly how many items does this process per week or month?
2. **Reliability** — Any measurable effect from queues, retries, or automation (errors, tasks/day, data not dropped)?
3. **Scale** — Besides any user count already listed: accounts, roles, money, currencies, records?
4. **Time** — How often does it run, and how long did the manual path take vs now? Any parallelism / batch size?
5. **Projects** — Stars/forks, **or** if early: how many types/environments/items can it manage?

**If the user answers qualitatively and tells you to pick numbers:** infer **conservative, round** figures from that description (retry count, weekly volume, minutes vs hours, batch size). Put them in the bullets. List every assumed number in the delivery notes.

Never invent employers, titles, tools, or repos. Numbers may be estimated **only** when the user described the behavior and authorized it.

### Step 6: Experience, Projects, Skills, length

- **Experience**: Keep roles if space allows, but **filter and rewrite bullets** per JD. Typically **3–4 bullets** per role, strongest first. **One outcome per bullet** — split combined “did A and [verb] B” lines so each can carry a number.
- **Projects**: Only the JD-selected set from Step 3. Each project: **2 bullets**, same pattern as experience — not a one-line name/stack blurb.
- **Verbs**: Leading action verb **at most twice** on the whole resume. Count before delivery. Especially avoid repeating Built / Implemented / Developed. Substitutes: see [content-checklist.md](content-checklist.md).
- **Skills**: Use the **Skills** section of `reference.md` as the inventory. Output **only** skills that appear in the JD or closely support a JD requirement. Keep subgroup labels if present (frontend / backend / database). Order by JD relevance. Drop unmatched items and empty subgroups. Never paste the full inventory. Never add skills not in `reference.md`.
- **Length (early-career):** **1 page** and **~500 words** (band **470–540**) of visible body text. Thin one-liners read as too short / under-detailed; padding toward ~1000 words reads as too long / wordy and will not fit one page.
  - Too thin → add numbers and a how/result clause to **existing** bullets; maybe one extra bullet. Do **not** inflate word count.
  - Too long → cut stacked clauses and the weakest bullet; **keep the numbers and unique verbs**.

### Step 7: Output TeX

1. Start from [templates/resume.tex](templates/resume.tex) (haider / Jake Yang style). **Do not change fonts** — keep `tgheros` (body), `FiraMono` (monospace contact via `\texttt`), and `fontawesome5` icons.
2. **Write output in the directory where the skill was invoked** — the user's current workspace / project cwd — **not** inside this skill folder.
   - Default: `<cwd>/<role-slug>-resume.tex` (e.g. `./senior-backend-engineer-resume.tex`).
   - If the user asks for a subfolder, use `<cwd>/<that-folder>/<role-slug>-resume.tex` and create it if needed.
   - Never write under the skill's own `output/` or skill package path.
3. Use **ASCII-safe** TeX for body text where possible; escape `&`, `%`, `#`, `_`, `$` in content.
4. Preserve the template macros and structure:
   - Header: centered name + `\faPhone*` / `\faEnvelope` / `\faGithub` / `\faGlobe` / `\faMapMarker*` with `\texttt{...}` values
   - Sections: `PROFESSIONAL SUMMARY`, `EXPERIENCE`, `PROJECTS`, `EDUCATION`, `SKILLS` (omit empty ones)
   - Roles: `\resumeSubheading{Company}{Dates}{Title}{Location}` + `\resumeItem{...}`
   - Projects: `\resumeProjectHeading{\textbf{Name} $|$ \href{url}{\myuline{label}}}{Dates}` + items
   - Skills: labeled lines (`Languages` / `Frameworks` / `Tools` / …) inside the template's itemize block
5. Header must include available links from Personal (GitHub, website/portfolio, LinkedIn) alongside contact fields.
6. **Overleaf-safe preamble (required)** — copy the template preamble as-is. Do not “simplify” or restore bare pdfTeX-only calls:
   - Keep `\usepackage{iftex}` and the `\ifPDFTeX ... \fi` guard around `glyphtounicode` / `\pdfgentounicode`.
   - Never emit unguarded `\input{glyphtounicode}` or bare `\pdfgentounicode=1` (breaks XeLaTeX/LuaLaTeX on Overleaf with `\pdfglyphtounicode` undefined).
   - Do not add XeLaTeX-only packages (`fontspec`, `unicode-math`) or swap engines in the file.
   - Prefer packages already in the template (`tgheros`, `FiraMono`, `fontawesome5`, `hyperref`, etc.).
7. Tell the user the absolute path of the written `.tex` file, and that Overleaf should use **Menu → Compiler → pdfLaTeX**.

### Step 8: Score (ATS ≥ 95 + content pass)

1. Score with [ats-checklist.md](ats-checklist.md). Sum points; require **≥ 95 / 100**. If below 95, revise keywords, headings, and structure, then re-score.
2. Then run [content-checklist.md](content-checklist.md) (numbers, verb caps, 470–540 words, no one-line projects). Revise until it passes.
3. Report both: `ATS self-score: NN/100` and `Content self-check: PASS` (or failing items). Include any assumed metrics.

## Hard rules

- Facts only from [reference.md](reference.md) + user corrections in-chat. Numbers may be conservative estimates **only** when the user described the work and asked you to pick them; always disclose assumptions.
- **JD relevance over completeness** — do not dump all skills, projects, or bullets from `reference.md`. Select and emphasize what matches the posting.
- Verbatim JD keyword phrases when they match real experience (same casing as common skill names is fine).
- Standard section names (uppercase in TeX): `PROFESSIONAL SUMMARY`, `EXPERIENCE`, `PROJECTS`, `EDUCATION`, `SKILLS` (include only sections with content).
- Feature only GitHub/projects listed in `reference.md`; pick the JD-best 2–4. Each gets two quantified bullets, not a heading blurb.
- Skills on the resume must come from the Skills section, filtered to JD overlap.
- Every experience/project bullet: one outcome, a unique-enough action verb (no verb > 2 times), and a numeral.
- Early-career length: **1 page**, **~500 words** (470–540). Never “fix short” by writing ~1000 words; never “fix long” by deleting the numbers.
- Keep template fonts and chrome: `tgheros`, `FiraMono`, Font Awesome icons, light-grey section rules. No photos, charts, or extra decorative graphics.
- Output is always a `.tex` file in the **invocation cwd** (workspace where the skill was called), never inside this skill directory.
- **Overleaf is the default compile target.** Keep the `iftex`-guarded glyph mapping from the template; never introduce bare `\pdfglyphtounicode` / `\pdfgentounicode` / unguarded `\input{glyphtounicode}`. Tell the user to compile with **pdfLaTeX** on Overleaf (also works locally via `pdflatex` / `latexmk -pdf`).

## Additional resources

- Blank form to commit: [reference.template.md](reference.template.md) (copy to `reference.md`; that file is gitignored)
- ATS scoring: [ats-checklist.md](ats-checklist.md)
- Content / length / verb / numbers scoring: [content-checklist.md](content-checklist.md)
- TeX scaffold: [templates/resume.tex](templates/resume.tex) — Overleaf-safe preamble (pdfTeX glyph helpers behind `\ifPDFTeX`)
