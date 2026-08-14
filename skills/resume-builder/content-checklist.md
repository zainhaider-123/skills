# Content quality self-check

Run this **after** the ATS checklist. External resume reviewers (ATS tools, recruiter platforms, humans) flag these even when keywords parse fine.

Pass only if **every** item below is met. If not, revise the `.tex` and re-check. Report: `Content self-check: PASS` or list the failing items.

## 1. Hard numbers (most common fail)

**Rule:** Almost every Experience and Projects bullet must contain a **numeral** (count, rate, money, time, %, parallelism, retries, users, pages, records).

Entry-level is not an exemption. “Automated X” and “integrated Y and Z” without a number will be flagged.

| Include a number for… | Ask / derive… |
|-----------------------|----------------|
| Integrations / intake | Volume per week or month (submissions, documents, events) |
| Background jobs / queues / webhooks | Reliability: retries, tasks processed, lost-data prevented, error drop |
| Products / portals | Scale: users, accounts, roles, transaction value, currencies |
| Internal tools / QA / reporting | Cadence + time saved vs the manual path; batch size / parallelism |
| Side projects / CLIs | Stars/forks **or** (if pre-release) capability scope — not vanity metrics |

**One outcome per bullet.** Do not glue two systems together with “and [verb] …” — split them so each can carry its own number.

**If `reference.md` lacks numbers:** pause and ask the questions in SKILL.md Step 5. Do not emit a numberless draft.

**If the user describes impact qualitatively and says to pick numbers:** choose **conservative, round** figures that follow from what they described (e.g. retry attempts, weekly volume, minutes vs hours). Put those figures in the bullets, then list the assumptions in the delivery notes so they can correct them.

Early-stage projects (`v0.x`, “still in development”): quantify **what it can do** (N items managed, N pages queued, N environments), not popularity.

## 2. Word count band (do not over-correct)

Target **one page** always (early-career).

| Career stage | Word count (visible body: summary + experience + projects + education + skills) |
|--------------|----------------------------------------------------------------------------------|
| Student / intern / ≲ 5 years | **470–540** (aim ~500) |
| 5–10 years | 550–700, still 1 page if it fits |
| 10+ years | 2 pages only if JD fit is strong |

Count by stripping TeX macros/`\resumeItem` wrappers and counting remaining English words. Header contact lines do not count toward the band.

**Too short (thin one-liners, few numbers):** add a numeral and a concrete “how/result” clause to existing bullets. You may add **one** extra bullet or a second project bullet. **Never pad toward ~1000 words** — that overshoots the band, will not fit one page at 11pt, and then reads as too long / wordy.

**Too long / wordy for career level:** cut stacked clauses, repeated tech names, and the weakest bullet. **Keep every number and every unique leading verb.** Do not strip quantification to save words.

## 3. Action-verb uniqueness

**Rule:** Across Experience + Projects, **no leading action verb more than twice**. Three uses of *Developed*, *Built*, or *Implemented* is a fail.

1. List the first word of every `\resumeItem`.
2. If any verb appears > 2 times, rewrite the extras with a different verb that still matches the fact.
3. Prefer a unique opener per bullet when the set is small (≤ ~10 bullets).

High-risk repeats: Built, Implemented, Developed, Designed, Created, Managed, Worked.

**SWE-oriented substitutes** (pick what is truthful):

Architected, Engineered, Shipped, Launched, Automated, Integrated, Orchestrated, Streamlined, Reduced, Accelerated, Established, Introduced, Hardened, Mapped, Queued, Exported, Authored, Configured, Deployed, Instrumented, Scaled, Migrated, Refactored, Spearheaded, Delivered, Produced, Refined, Consolidated, Converted, Expanded, Generated, Initiated, Optimized, Resolved, Simplified, Transformed, Upgraded.

Do not cycle the same 2–3 substitutes either. Do not use a verb that overclaims (e.g. *Spearheaded* for a solo bugfix).

## 4. Detail without bloat

Length feedback conflicts if you only add words **or** only cut words.

- **Enough detail:** Projects are not a heading plus a one-line blurb. Each selected project gets **2 quantified bullets** (same pattern as experience).
- **Not wordy:** Each bullet is **one sentence**, roughly **18–32 words**, one number, one tech cluster, one result. No three-clause “and … and …” stacks.
- Summary stays **3–4 lines** and includes 1–2 numbers if they are already in the body (do not invent a second set).

## Quick fail list

Revise before delivery if any of these are true:

- [ ] More than two experience/project bullets have **no digit**
- [ ] Any action verb used **3+** times
- [ ] Body word count **< 450** or **> 560** (early-career)
- [ ] A project is only a name + stack + one sentence
- [ ] Two achievements share one bullet
- [ ] Trimming removed the numbers that were added to pass check 1
