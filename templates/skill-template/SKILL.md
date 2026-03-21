---
name: skill-template
description: Use this template when creating a new reusable skill for this repository. Replace the frontmatter and instructions after copying it into skills/<skill-name>/.
---

# Skill Template

Copy this directory to `skills/<skill-name>/`, then replace the placeholders with the real workflow.

## Purpose

State what the skill should help with, when it should trigger, and any constraints the agent must respect.

## Workflow

1. Describe the preferred order of operations.
2. Call out non-obvious defaults, constraints, or validation steps.
3. Keep the core instructions short and move bulky detail into `references/` when needed.

## Optional Bundled Resources

```text
skill-template/
├── SKILL.md
├── scripts/          # Optional: deterministic helpers or wrappers
├── references/       # Optional: long docs, schemas, and examples
├── assets/           # Optional: templates, sample files, icons, fonts
└── agents/
    └── openai.yaml   # Optional: Codex-specific metadata
```

- Add `scripts/` only when deterministic behaviour or repeated logic justifies it.
- Add `references/` for documentation that should load on demand rather than live in `SKILL.md`.
- Add `assets/` for files the agent uses in outputs rather than as context.
- Add `agents/openai.yaml` only when Codex app metadata, invocation policy, or tool dependencies improve the experience.

## Validation Checklist

- Keep `name` aligned with the directory name.
- Make `description` explicit about when to use the skill.
- Use relative paths for any bundled files you reference.
- Validate the finished skill with `skills-ref validate skills/<skill-name>` when the validator is available locally.
