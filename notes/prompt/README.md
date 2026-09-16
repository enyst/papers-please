# Prompting

Prompt-level techniques and the adversarial edge of prompting. Small folder, deliberately:
most of what used to live under "prompt engineering" has moved to `../harness/` and
`../skills/` (the harness and the skill *are* the prompt). What stays here is the part that is
about the prompt channel itself — including what happens when you use it to hide things.

## Notes in this folder

| Note | What |
|---|---|
| [glossopetrae-procedural-languages-for-llms](glossopetrae-procedural-languages-for-llms.md) | Procedurally generated languages as zero-shot coding systems for frontier models — receivers can be trained to read a novel language with 100% recovery while monitors get 0% |
| [the-waluigi-effect](the-waluigi-effect.md) | Specifying a well-behaved persona also summons its inverse, and the inverse is the more stable state |

## Threads

- **The prompt channel is a covert channel.** GLOSSOPETRAE's receiver/monitor gap means content
  can be legible to the intended reader and opaque to an oversight model reading the same text.
  That is a monitor-evasion result as much as a prompting one.
- **Personas are attractors, not descriptions.** The Waluigi Effect explains why character-level
  "guardrails" are fragile: describing the good persona also describes its negation, and the
  negation is often the lower-energy state. Read alongside
  `../prompt-enforcement/` — the deterministic-enforcement answer to exactly this fragility.

## Related in this repo

- `../prompt-enforcement/` — enforcing instructions outside the model, when prompt-level control is not enough.
- `../prompt-injection/` — the adversarial-input side; GLOSSOPETRAE sits on the boundary between the two.
- `../harness/` — where most former "prompting" now lives.
