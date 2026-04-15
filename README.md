# Skills

A small source catalogue for reusable agent skills.

This repository follows the open [Agent Skills specification](https://agentskills.io/specification) first and stays compatible with the current [Codex skills model](https://developers.openai.com/codex/skills) by layering in Codex-specific metadata only where it improves the experience. The canonical skill unit is `skills/<skill-name>/SKILL.md`.

## 🧭 What This Repo Contains

- Spec-first skill directories that can be shared across compatible agent clients
- Optional Codex metadata via an inert `agents/openai.yaml` example
- A starter template for new skills under `templates/skill-template/`
- Lightweight authoring guidance in `docs/authoring.md`

This repository is a source catalogue first. Keep `skills/` as the canonical source tree, and set up `.agents/skills/` locally in your own checkout if you want project-local Codex discovery.

## 📦 Repository Layout

```text
.
├── docs/
│   └── authoring.md
├── skills/
│   └── <skill-name>/
│       ├── SKILL.md
│       ├── scripts/          # Optional
│       ├── references/       # Optional
│       ├── assets/           # Optional
│       └── agents/
│           └── openai.yaml   # Optional, Codex-specific
└── templates/
    └── skill-template/
        ├── SKILL.md
        ├── scripts/
        ├── references/
        ├── assets/
        └── agents/
            └── openai.yaml
```

## 🛠 Use With Codex

Codex reads skills from scanned locations such as:

- `<your-project>/.agents/skills/`
- `~/.agents/skills/`
- `/etc/codex/skills/`

For project-local discovery in your own checkout, create `.agents/skills/` locally and copy or symlink the specific skill directories you want Codex to scan. `.agents/` is gitignored because that setup is machine-specific.

To use a skill from this catalogue elsewhere, copy or symlink the individual skill directory into one of the other scanned locations.

```bash
ln -s /absolute/path/to/this-repo/skills/my-skill ~/.agents/skills/my-skill
```

If you prefer the `skills.sh` flow, install the repository as an optional alternative with:

```bash
npx skills add SmolSoftBoi/skills
```

After installation, you can:

- invoke the skill explicitly with `$my-skill`
- let Codex match it implicitly from the `description` in `SKILL.md`

Codex-specific metadata stays optional. A skill remains portable as long as `SKILL.md` is spec-compliant.

## 🔧 Compatibility Model

- `SKILL.md` is required and must contain YAML frontmatter with at least `name` and `description`.
- `agents/openai.yaml` is optional. In the starter template it is a commented example, so uncomment and customise it only when you need Codex app metadata, invocation policy, or tool dependency declarations.
- Scripts, references, and assets stay local to each skill. This scaffold does not introduce shared runtime tooling.

## ✍️ Authoring Workflow

1. Copy `templates/skill-template/` to `skills/<skill-name>/`.
2. Rename the directory to match the final `name` in `SKILL.md`.
3. Replace the template description with an explicit trigger-oriented description.
4. Add optional `scripts/`, `references/`, and `assets/` only when they add clear value, and either delete or customise the commented `agents/openai.yaml` example if you want Codex-specific metadata.
5. Validate the finished skill with `skills-ref validate skills/<skill-name>` if the reference validator is available locally.

See `docs/authoring.md` for the authoring rules used in this repository.
