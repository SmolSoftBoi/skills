---
name: condense-chatgpt-memories
description: Use this skill when the user pastes ChatGPT memories, saved-memory notes, custom-instruction fragments, or mixed preference lists and asks to condense, deduplicate, or clean them up into a compact reusable block for ChatGPT.
---

# Condense ChatGPT Memories
Turn pasted memory material into a short `Memory Block` for reuse in ChatGPT-style contexts.

## Workflow
1. Parse the pasted material and keep only stable, user-specific signals.
2. Sort each signal into `Preferences`, `Constraints`, or `Communication`.
3. Remove duplicates, merge near-duplicates, and discard filler or transient details.
4. Rewrite the remaining points into short, direct blocks.
5. Add uncertainty notes only when the source contains conflicts, ambiguity, or obviously temporary items.
6. Before finalizing, check that every retained point is durable, user-specific, non-duplicative, and placed under the correct section.

## Output Contract
Produce exactly these sections in this order:
- `Preferences`
- `Constraints`
- `Communication`

Add `Uncertain or Excluded` only when needed. Omit it otherwise.

Use short blocks under each section. Phrase each block as a durable user fact, preference, or instruction.
Interpret the sections as follows:
- `Preferences`: likes, defaults, tastes, and recurring ways of working.
- `Constraints`: limits, avoidances, dislikes, non-goals, and hard requirements.
- `Communication`: tone, formatting, brevity, collaboration style, and response preferences.

Keep all three required section headings. If a section has no reliable content, write `- None stated.`
Output only the requested format.

Use this shape:
Memory Block
Preferences
```markdown
...
```
Constraints
```markdown
...
```
Communication
```markdown
...
```

## Judgement Rules
- Keep the result terse enough to paste into ChatGPT memory or profile-style fields.
- Prefer concise, information-dense wording.
- Preserve meaning. Compress wording, but do not invent missing preferences or strengthen weak evidence.
- Prefer durable patterns over situational requests.
- Drop non-user-specific details, conversational filler, repetition, and examples that do not add a stable rule.
- If two items conflict, keep the clearer durable one when the source resolves it; otherwise move the conflict to `Uncertain or Excluded`.
- Normalise wording so overlapping items become one clean block instead of several similar blocks.
- If required context is missing or evidence is too weak, do not guess; omit the item or place it in `Uncertain or Excluded` when useful.