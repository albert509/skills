# Agent Skills

Personal Codex/agent skills for reusable engineering workflows.

[![skills.sh](https://skills.sh/b/albert509/skills)](https://skills.sh/albert509/skills)

## Skills

| Skill | Purpose |
|---|---|
| [`codebase-discovery`](skills/codebase-discovery/) | Discover, map, and onboard into large software codebases with developer-focused field guides. |

## Layout

Published skills live under `skills/`. Each skill folder should match the `name` in its `SKILL.md` frontmatter.

```text
skills/
└── skill-name/
    ├── SKILL.md
    ├── agents/
    │   └── openai.yaml
    └── references/
        └── ...
```

## Install

After this repository is pushed to GitHub as `albert509/skills`, install with:

```bash
npx skills@latest add albert509/skills
```

To list the skills detected in this repository:

```bash
npx skills@latest add albert509/skills --list
```

To install only one skill:

```bash
npx skills@latest add albert509/skills --skill codebase-discovery
```

For local development before publishing:

```bash
npx skills@latest add ./ --skill codebase-discovery
```

Restart Codex after adding or updating skills so the registry can refresh.

## Validate

Use the bundled `skill-creator` validator from Codex when available:

```bash
python3 /Users/luisalmonte/.codex/skills/.system/skill-creator/scripts/quick_validate.py skills/codebase-discovery
```
