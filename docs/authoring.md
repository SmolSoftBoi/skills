# Skill Authoring

Use this guide when adding or updating a skill in this repository.

## 🧱 Repository Contract

- Live skills belong in `skills/<skill-name>/`.
- Every skill must include `SKILL.md`.
- Optional per-skill directories are `scripts/`, `references/`, `assets/`, and `agents/openai.yaml`.
- Keep each skill self-contained. Do not add repo-wide shared runtime helpers in v1.

## 📦 Codex and `skills.sh`

- Keep local Codex usage simple by developing skills under `skills/<skill-name>/` while the repo exposes `.agents/skills` as a project-local scan path.
- Make sure each shipped skill has a valid `SKILL.md`, matching directory name, and clear README usage examples.
- Treat `agents/openai.yaml` as optional additive metadata. Portability still comes from the base skill structure and `SKILL.md`.

## 🏷 Naming Rules

The open Agent Skills spec requires the `name` in `SKILL.md` to match the parent directory name exactly.

Use names that:

- are 1 to 64 characters long
- use lowercase letters, numbers, and hyphens only
- do not start or end with a hyphen
- do not contain consecutive hyphens

Good examples:

- `shopify-theme-review`
- `openai-docs`
- `pdf-redlining`

Avoid capitals, spaces, underscores, and mismatched folder names.

## 🎯 Writing Descriptions That Trigger Well

The `description` field drives progressive disclosure. Codex and other compatible agents load only `name` and `description` at discovery time, so the description must tell the agent when to activate the skill.

Write descriptions that:

- use imperative phrasing such as `Use this skill when...`
- describe the user intent, not the internal implementation
- include the kinds of prompts or contexts that should trigger the skill
- stay narrow enough to avoid noisy activation
- stay concise; the spec limit is 1024 characters

Prefer this:

```yaml
description: Use this skill when the user needs help creating, reviewing, or refactoring reusable Codex skills, including SKILL.md structure, optional scripts, and trigger descriptions.
```

Avoid this:

```yaml
description: A skill for skills.
```

## ⚙️ Instruction-Only vs Scripts

Default to instruction-only skills. Add scripts only when they clearly improve reliability or save repeated effort.

Keep the skill instruction-only when:

- the workflow is mostly judgement and sequencing
- multiple implementations are reasonable
- the agent can complete the task with existing tools and concise guidance

Add a script when:

- the same code keeps being rewritten
- the task needs deterministic behaviour
- the workflow depends on structured machine-readable output
- the script wraps an external tool or format-specific operation cleanly

If you add scripts:

- keep them non-interactive
- accept inputs by flags, environment variables, or stdin
- emit structured output where practical
- reference them with relative paths from the skill root, such as `scripts/extract.py`

## 🧩 Optional Codex Metadata

`agents/openai.yaml` is optional. The starter template includes it as a commented example only, so copied skills should either delete the file or uncomment and customise it when Codex-specific behaviour or presentation improves the skill.

Use it for:

- `interface.display_name`
- `interface.short_description`
- `interface.default_prompt`
- `policy.allow_implicit_invocation`
- `dependencies.tools`

Do not rely on `agents/openai.yaml` for core portability. The base skill must still work as a spec-compliant `SKILL.md` package.

## 🗂 Recommended Skill Shape

```text
<skill-name>/
├── SKILL.md
├── scripts/          # Optional: deterministic helpers
├── references/       # Optional: load-on-demand docs
├── assets/           # Optional: templates and output resources
└── agents/
    └── openai.yaml   # Optional: Codex-specific metadata
```

Keep `SKILL.md` concise and move long reference material into `references/` when it starts to dominate the core workflow.

## ✅ Validation

This repository does not bundle a validator. If you have the Agent Skills reference validator installed locally, run:

```bash
skills-ref validate skills/<skill-name>
```

At minimum, check that:

- the directory name matches `name`
- `SKILL.md` frontmatter includes `name` and `description`
- any referenced relative paths exist
- optional `agents/openai.yaml` stays aligned with the skill’s purpose
