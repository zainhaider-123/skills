# Personal

Copy this file to `reference.md` and fill in your facts.
Contact, links, and GitHub repos for the header / Projects section.
Only include public / shareable URLs.

```yaml
full_name: ""
email: ""
phone: ""              # include country code if useful
location: ""           # City, Country
linkedin: ""
github: ""             # https://github.com/username
website: ""
portfolio: ""          # if different from website
target_titles:
  - ""
core_strengths:
  - ""
other_links:
  - label: ""
    url: ""

# Repos the agent can feature when they match the JD (pick 2–4 best).
github_projects:
  - name: ""
    url: ""            # https://github.com/user/repo
    description: ""
    technologies: []
    status: ""         # e.g. v0.0.1, in development — agent will quantify scope, not stars
    highlights:        # each highlight should include a number when possible
      - ""
    topics: []         # e.g. api, react, ml
    metrics:           # optional; used when highlights lack numbers
      volume: ""       # e.g. N items processed / skills managed
      scale: ""        # users, environments, skill types
      time_saved: ""
```

# Experience

Newest first. Only facts — the agent rewrites bullets per JD.
Prefer Action + scope + tech + **numeral** + result. One outcome per bullet.

```yaml
- title: ""
  company: ""
  location: ""
  start: ""            # Month YYYY
  end: ""              # Month YYYY or present
  technologies: []
  bullets:
    - ""               # include a number: volume, time, $, %, users, retries
  metrics:             # fill when bullets are still qualitative — agent will ask if empty
    volume: ""         # e.g. N submissions/week, N documents/month
    scale: ""          # users, accounts, roles, $ value, currencies
    reliability: ""    # retries, error drop, uptime, zero data loss
    time_saved: ""     # manual vs automated; cadence (daily/weekly)
    other: ""
```

# Skills

Canonical inventory. The agent intersects with the JD — do not invent skills here.

```yaml
languages: []
frameworks:
  frontend: []
  backend: []
  database: []
tools: []
other: []
```

# Education

```yaml
- degree: ""
  University: ""
  location: ""
  start: ""
  graduation: ""       # Month YYYY or Expected YYYY
  gpa: ""              # optional
  highlights: []
```

# Projects

Optional curated / non-GitHub projects. Merged with `github_projects`; dedupe by name/URL.

```yaml
- name: ""
  url: ""
  start: ""
  end: ""
  technologies: []
  bullets:
    - ""               # 2 quantified bullets on the resume, not a one-line blurb
  metrics:
    volume: ""
    scale: ""
    time_saved: ""
```
