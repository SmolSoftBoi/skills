---
name: skill-template
description: Use this template when creating a reusable skill for this repository. Copy it into `skills/<skill-name>/`, then replace the frontmatter and workflow with the real skill.
---

# Skill Template

Copy this directory to `skills/<skill-name>/`, rename it to the final skill name, then replace the placeholders with the real workflow.

## Purpose

State:

- what the skill helps with
- when it should trigger
- any constraints, defaults, or safety rules the agent must respect

## Workflow

1. Describe the preferred order of operations in direct, reviewable steps.
2. Explain any validation or prerequisite checks before the main workflow.
3. Call out defaults and constraints that should not be guessed.
4. Keep the core instructions short and move bulky detail into `references/` when needed.

## Description Checklist

- Replace `name` with the final directory name exactly.
- Make `description` explicit about when to use the skill.
- Prefer trigger-oriented phrasing such as `Use this skill when...`.
- Describe user intent rather than internal implementation details.

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
- Add `agents/openai.yaml` only when Codex-specific metadata, invocation policy, or tool dependencies improve the experience.
- Keep the base skill usable without `agents/openai.yaml`; it is additive metadata, not the core skill definition.

## Validation Checklist

- Keep `name` aligned with the directory name.
- Make `description` explicit about when to use the skill.
- Keep instructions readable, direct, and narrow enough to avoid noisy activation.
- Use relative paths for any bundled files you reference.
- Validate the finished skill with `skills-ref validate skills/<skill-name>` when the validator is available locally.
