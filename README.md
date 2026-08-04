# Skills

A collection of [Cursor Agent Skills](https://cursor.com/docs) — reusable instruction packs that teach the agent how to run specific workflows.

Each skill lives in its own directory under `skills/` and is defined by a `SKILL.md` file.

## Layout

```
skills/
└── <skill-name>/
    ├── SKILL.md          # Required — instructions + YAML frontmatter
    ├── reference.md      # Optional — supporting facts or docs
    ├── templates/        # Optional — scaffolds the skill uses
    └── scripts/          # Optional — helpers the skill may run
```

## Skills

| Skill | Description |
|-------|-------------|
| [resume-builder](skills/resume-builder/) | ATS-optimized LaTeX resume tailored to a job description |

## Using a skill

Point Cursor at a skill directory (personal `~/.cursor/skills/`, project `.cursor/skills/`, or symlink/copy from this repo). The agent loads `SKILL.md` when the task matches the skill’s description.

## Adding a skill

1. Create `skills/<skill-name>/SKILL.md` with frontmatter (`name`, `description`) and the workflow body.
2. Add optional assets (`reference.md`, templates, scripts) as needed.
3. Document the skill in the table above.

Keep each skill focused on one workflow. Put durable facts the agent must not invent in `reference.md` (or similar), not in the chat history alone.
