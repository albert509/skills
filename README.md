# Agent Skills

Personal Codex/agent skills for reusable engineering workflows.

## Skills

| Skill | Purpose |
|---|---|
| [`codebase-audit`](codebase-audit/) | Audit, understand, map, and onboard into large software codebases with evidence-backed findings and action items. |

## Layout

Each top-level folder is one skill and should match the `name` in its `SKILL.md` frontmatter.

```text
skill-name/
├── SKILL.md
├── agents/
│   └── openai.yaml
└── references/
    └── ...
```

## Install Locally

Clone this repository, then copy or symlink the skills you want into your Codex skills directory:

```bash
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
ln -s "$(pwd)/codebase-audit" "${CODEX_HOME:-$HOME/.codex}/skills/codebase-audit"
```

Restart Codex after adding or updating skills so the registry can refresh.

## Validate

Use the bundled `skill-creator` validator from Codex when available:

```bash
python /Users/luisalmonte/.codex/skills/.system/skill-creator/scripts/quick_validate.py codebase-audit
```
