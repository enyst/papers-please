---
title: "Atlas: Grounding & Understanding"
type: atlas
read_depth: cross-store synthesis
tags:
  - atlas
  - grounding
  - understanding
  - meaning
  - symbol-grounding
  - world-models
  - concept-formation
updated: "2026-09-16"
---

# Atlas: Grounding & Understanding

A cross-store map of the oldest live question in AI: **does a system that produces fluent
language actually understand — connect its symbols to meaning and the world — or only
manipulate form?** An *index page*: links + synthesis, no copies. See top-level `README.md`
→ "The wider atlas".

## The one-paragraph synthesis

There are two camps and they've been arguing since 1950. **Turing** says judge by behaviour;
if you can't tell it from a human, stop withholding "thinks." The **skeptic lineage**
(Searle → Harnad → Bender & Koller → Stochastic Parrots) says behaviour isn't enough:
**syntax isn't semantics**, and **meaning can't be learned from form alone** — you need
*grounding* (symbols tied to perception, action, communicative intent, the world). The
**constructive / empirical reply** says grounding-ish structure can actually appear:
Othello-GPT shows a next-token model building a *causally-usable* world model, and the Lake /
theory-based-RL line shows structured causal models give real understanding-like
generalization. **Mitchell & Krakauer** referee: our current tests can't settle it, so build
a science of intelligence that admits non-human modes. The unresolved core — is fluent
competence evidence of understanding? — is exactly what the RSTA world-models issue is about,
and exactly the risk when we present a charming agent like SmolPaws.

## The debate, as a spectrum

### Pole A — behaviour is enough
- `notes/world-models-agi/turing-computing-machinery-and-intelligence.md` — the imitation
  game; judge by indistinguishable behaviour. The bar everything else contests.

### The skeptic lineage — "no meaning without grounding"
- `world-models-agi/searle-minds-brains-and-programs-chinese-room.md` — syntax ≠ semantics
  (the thought-experiment origin).
- `world-models-agi/harnad-symbol-grounding-problem.md` — formalizes it: symbols must be
  grounded bottom-up in perception (iconic + categorical), else meaning is parasitic. The
  load-bearing classic; proposes the (neurosymbolic) fix.
- `world-models-agi/bender-koller-climbing-towards-nlu-octopus.md` — the octopus test:
  meaning can't be learned from form alone; you need the intent/world side.
- `world-models-agi/stochastic-parrots.md` — the "illusion of meaning" is partly *our*
  projection; humans over-attribute mind to coherent form.
- Empirical echo (in the RSTA issue):
  `world-models-agi/a-sentence-is-worth-a-thousand-pictures-leet-task.md` — humans do
  grounded top-down repair (decode l33t); LLMs lean on fixed token↔vector associations.

### The constructive / empirical reply — structure can carry understanding
- `world-models-agi/othello-gpt-emergent-world-representations.md` — a next-token model
  builds a probeable, **causally-editable** board model. Strongest counter to "just surface
  statistics." (Caveat: tiny synthetic world; "board model" ≠ "grounded meaning".)
- `world-models-agi/lake-building-machines-that-learn-and-think-like-people.md` +
  `lake-human-level-concept-learning-program-induction.md` — concepts as compositional,
  causal programs → one-shot, transferable understanding-like behaviour.
- `world-models-agi/theory-based-rl-human-level-learning.md` &
  `empowerment-gain-and-causal-model-construction.md` — grounding via *causal interaction*
  (act, control outcomes) rather than text: an agent that builds/uses causal world models.

### The referee + the metaphysics of "understanding/experience"
- `world-models-agi/mitchell-krakauer-debate-over-understanding.md` — the best survey; splits
  it into statistics-vs-causal-mechanism; current tests can't adjudicate → build better
  probes.
- Consciousness axis (separate from *functional* understanding, easy to conflate):
  `world-models-agi/nagel-what-is-it-like-to-be-a-bat.md`,
  `chalmers-facing-up-hard-problem.md`, `block-two-concepts-of-consciousness.md`
  (access vs phenomenal — the precision tool), `dennett-real-patterns.md` (deflationary:
  understanding = real patterns you can exploit).

### How to look *inside* (turn the question empirical) — `notes/interpretability/`
- `interpretability/steering-vectors-and-activation-engineering.md`,
  `chalmers-j-space-global-workspace.md`,
  `kim-consciousness-vector-safety-entanglement.md`. Probing + causal intervention (the
  Othello method) is how "does it represent X?" stops being philosophy. Pairs with the RSTA
  `levels-of-analysis-for-llms.md` (Marr's implementation level).

## For us (SmolPaws / Engel)
- **Concept formation** (Engel's core interest) is the *constructive* side of this debate:
  the Lake/theory-based-RL line is "what understanding-capable learning would need"
  (compositional + causal + learning-to-learn), the opposite of averaging over many
  examples. Cross-links to `atlas-agent-memory.md` (memory → learned models).
- **Grounding SmolPaws has that the octopus doesn't:** tools, real side effects, multi-turn
  consequences. An *agent* (vs a chatbot) has action/world channels — the exact thing Bender
  & Koller say text lacks. Worth taking seriously as a partial answer to the skeptics.
- **Honesty discipline:** the Parrots "illusion of meaning is our projection" + Block's
  access-vs-phenomenal are the tools for not overclaiming — a charming cat persona and fluent
  output are *not* evidence of understanding or inner life. Say functional things
  functionally.

## Open questions (seeds for future notes)
- Does agent tool-use / real-world side effects constitute *grounding* in Harnad's sense, or
  just more symbols (his Robot-reply worry)?
- What's the sharpest cheap probe we could run on SmolPaws' own model to test "represents vs
  parrots" for a task it does daily?
- Reconcile Othello-GPT (structure emerges from form) with Bender & Koller (meaning can't
  come from form) — where exactly is the line?

## Related outside the corpus
Dileep George blog set of five (notes in `blogs/interesting-posts.md` → 2026-09-15/16),
same concept-formation thread; opinion essays and mechanism write-ups, not evidence:
- **"Ingredients of understanding"** (2023) — the *constructive* statement: understanding =
  mental simulation on a **causal, counterfactual, rapidly-modifiable sensorimotor
  world-model**; language is a "thin index into a shared sensorimotor codebook," not the
  model itself. Four ingredients (build world-models, modify by thinking, seek info, hypothesize-
  and-test). Directly restates Harnad grounding + Bender & Koller "not from form alone" as a
  mechanism; explicitly caveats Othello-GPT and Winograd-pass-≠-commonsense-solved.
- **"Amelia Bedelia and AGI Safety. Part 1"** (2024) — the same gap as a safety argument:
  misreading intent (dressing a raw chicken) is *not* value-misalignment, and human-like
  causal world-models buy *both* capability and controllability.
- **"Space is a sensory-motor sequence in the hippocampus"** (2024) — the *mechanism* under
  the argument: **CSCG** learns a latent graph from aliased egocentric sensory-motor
  sequences, and place cells turn out to track *sequence position*, not location (place
  fields are the experimenter's projection). A worked instance of grounding from structure —
  no space, geometry, or location primitives anywhere in the model. Clones resolve
  observation ambiguity by temporal context; schemas = the same graph with emissions rebound.
- **"Welcome to the exciting dirigibles era of AI"** (2023) — where the balloon-vs-airplane
  analogy comes from. Scaling an existing substrate (balloons → transformers) is a real path
  with a **finite runway**; searching for the principles is a real path too, and both deserve
  support. His own strongest counter-argument: maybe the transformer already *is* the
  aerodynamics. Plus the caution language's ELIZA effect "makes us see more than there is."
- **"AI consciousness, qualia, and personhood"** (2025) — the position paper of the set:
  consciousness as substrate-independent information processing, consciousness ≠ qualia, and
  personhood defined by mortality + remembered lived experience (AIs don't qualify, and he
  argues we shouldn't fake it). Asserted rather than argued; the sharpest content is in the
  comments (Chalmers-zombie + fast-abacus arguments against substrate independence). Read it
  with Block's access-vs-phenomenal seam in mind.

## How to extend this atlas
Maps, not copies. Add `notes/atlas-<thread>.md` only when a real question earns it; log a
`query` entry in `LOG.md`.
