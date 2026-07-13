## Summary

<!-- What changed? Keep this brief and specific. -->

- _Summarise the primary change._
- _Summarise any supporting change._
- _Note any compatibility or migration impact._

## Change type

<!-- Tick all that apply. -->

- [ ] New skill
- [ ] Skill improvement
- [ ] Documentation
- [ ] Template/scaffold change
- [ ] Validation or maintenance
- [ ] Other

## Skill checklist

<!-- Complete this section for new or changed skills. Delete if not relevant. -->

- [ ] The skill lives under `skills/<skill-name>/`.
- [ ] `SKILL.md` exists.
- [ ] The `name` field matches the skill directory exactly.
- [ ] The `description` is trigger-focused and starts with clear “Use this skill when…” style wording.
- [ ] Any referenced `scripts/`, `references/`, `assets/`, or `agents/openai.yaml` files exist.
- [ ] The skill remains usable without Codex-specific metadata.

## Documentation checklist

<!-- Complete this section for docs/template changes. Delete if not relevant. -->

- [ ] README guidance remains accurate.
- [ ] `docs/authoring.md` remains aligned with the repository contract.
- [ ] Template changes keep the default skill workflow simple and portable.

## Validation

<!-- What did you check? -->

- [ ] I reviewed the changed files manually.
- [ ] I validated the skill locally with `skills-ref validate skills/<skill-name>`.
- [ ] Not run / not applicable.

## Notes for review

<!-- Anything reviewers should focus on? -->
