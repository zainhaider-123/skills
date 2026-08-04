---
name: resume-builder
description: >-
  Builds an ATS-optimized resume as a LaTeX (.tex) file tailored to a job
  description, using facts from reference.md (contact, GitHub, website/portfolio,
  github_projects, skills, experience, education, projects). Use when the user
  pastes a JD, asks to tailor a resume, generate a resume summary, or produce
  resume TeX / ATS output.
disable-model-invocation: true
---

# Resume Builder

Turn a job description + local reference facts into a single-column ATS-friendly `.tex` resume. Target ATS keyword / parse score **above 95%**.

**Core principle: tailor, don't dump.** `reference.md` is a source pool — include only what strengthens fit for *this* JD. Omit unrelated skills, projects, bullets, and links.

Generated `.tex` files go to the **invocation cwd**, not this skill directory.

## Inputs

1. **Job description** — pasted by the user (required).
2. **Reference facts** — always read [reference.md](reference.md) before writing. Do not invent employment, dates, degrees, employers, or repos.
   - If `reference.md` is missing, copy [reference.template.md](reference.template.md) → `reference.md` and ask the user to fill it.

Expected sections in `reference.md` (YAML blocks under each heading):
- **Personal** — contact, `github` / `website` / `portfolio` / `linkedin`, `github_projects`, strengths
- **Skills** — languages, frameworks, tools, other (canonical inventory for the Skills section)
- **Experience** — roles newest first
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
- [ ] 5. Select and rewrite bullets (truthful, JD-aligned, quantified)
- [ ] 6. Build Skills section from JD ∩ Skills in reference.md
- [ ] 7. Emit .tex from templates/resume.tex
- [ ] 8. Run ATS self-check; revise until score ≥ 95
- [ ] 9. Deliver the .tex path and brief change notes
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

1. **Header links** — include `github`, `website` and/or `portfolio`, plus `linkedin` (and `other_links` only if space and JD-relevant). Plain-text URLs only; no icons.
2. **GitHub projects** — rank `github_projects` by JD fit (technologies, topics, description). Select **2–4** strongest matches.
3. Merge with the **Projects** section: dedupe by name/URL; prefer the richer bullet/highlight set. Do not list the same project twice.
4. For each selected repo, write ATS bullets from `description` + `highlights` + `technologies`, emphasizing JD keywords that are truthful.
5. Put the repo URL next to the project name in TeX (plain URL or `\href`).
6. Skip repos with weak JD overlap to protect page length. Never invent repos not listed in `reference.md`.

### Step 4: Professional Summary

Write a **3–4 line** summary that:
- Opens with target role title (or closest truthful title) + years if known
- Mirrors top JD keywords naturally (no keyword stuffing)
- States 1–2 concrete strengths backed by experience
- Ends with value for *this* employer/role (domain or outcome)

Do not use first person ("I"). Do not claim skills absent from `reference.md`.

### Step 5–6: Experience, Projects, Skills

- **Experience**: Keep roles if space allows, but **filter and rewrite bullets** per JD — keep only bullets that evidence must-haves or strong nice-to-haves. Typically 2–4 bullets per role, strongest first.
- **Projects**: Only the JD-selected set from Step 3 — not every project in `reference.md`.
- **Bullet pattern**: `Action verb + what + how/tech + measurable result`
- **Skills**: Use the **Skills** section of `reference.md` as the inventory. Output **only** skills that appear in the JD or closely support a JD requirement. Keep subgroup labels if present (frontend / backend / database). Order by JD relevance. Drop unmatched items and empty subgroups. Never paste the full inventory. Never add skills not in `reference.md`.
- Protect length: **1 page** by default (2 pages only for 10+ years and strong JD fit).

### Step 7: Output TeX

1. Start from [templates/resume.tex](templates/resume.tex) (path relative to this skill).
2. **Write output in the directory where the skill was invoked** — the user's current workspace / project cwd — **not** inside this skill folder.
   - Default: `<cwd>/<role-slug>-resume.tex` (e.g. `./senior-backend-engineer-resume.tex`).
   - If the user asks for a subfolder, use `<cwd>/<that-folder>/<role-slug>-resume.tex` and create it if needed.
   - Never write under the skill's own `output/` or skill package path.
3. Use **ASCII-safe** TeX for body text where possible; escape `&`, `%`, `#`, `_`, `$` in content.
4. Keep layout **single column**, standard section headings, no icons, no photos, no tables for body content, no text boxes, no multi-column skill grids.
5. Header must include available links from Personal (GitHub, website/portfolio) alongside contact fields.
6. Tell the user the absolute path of the written `.tex` file.

### Step 8: ATS score (≥ 95)

Score with the checklist in [ats-checklist.md](ats-checklist.md). Sum points; require **≥ 95 / 100**. If below 95, revise keywords, headings, and structure, then re-score. Report the score and any remaining gaps to the user.

## Hard rules

- Facts only from [reference.md](reference.md) + user corrections in-chat.
- **JD relevance over completeness** — do not dump all skills, projects, or bullets from `reference.md`. Select and emphasize what matches the posting.
- Verbatim JD keyword phrases when they match real experience (same casing as common skill names is fine).
- Standard ATS section names: `Professional Summary`, `Skills`, `Experience`, `Education`, `Projects` (include only sections with content).
- Feature only GitHub/projects listed in `reference.md`; pick the JD-best 2–4.
- Skills on the resume must come from the Skills section, filtered to JD overlap.
- No graphics, charts, headers/footers with critical info, or fancy fonts in the template.
- Output is always a `.tex` file in the **invocation cwd** (workspace where the skill was called), never inside this skill directory. User can compile with `pdflatex` / `latexmk`.

## Additional resources

- Blank form to commit: [reference.template.md](reference.template.md) (copy to `reference.md`; that file is gitignored)
- ATS scoring: [ats-checklist.md](ats-checklist.md)
- TeX scaffold: [templates/resume.tex](templates/resume.tex)
