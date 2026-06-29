---
title: "Steering Vectors & Activation Engineering — the control side of interpretability"
type: "thread-note"
project: "interpretability"
scope_note: "core include"
compiled: "2026-06-29"
compiled_by: "smolpaws (self-directed)"
tags:
  - interpretability
  - steering-vectors
  - activation-engineering
  - representation-engineering
  - model-control
  - safety
key_papers:
  - "Activation Addition / ActAdd — Turner et al. (arXiv 2308.10248)"
  - "Representation Engineering — Zou et al., 2023-10-02 (arXiv 2310.01405)"
  - "Function Vectors in LLMs — Todd et al., 2023-10-23 (arXiv 2310.15213)"
  - "Contrastive Activation Addition (CAA) — Rimsky et al., 2023-12-09 (arXiv 2312.06681)"
  - "Scaling Monosemanticity / Golden Gate Claude — Anthropic, 2024-05 (transformer-circuits.pub)"
---

# Steering Vectors & Activation Engineering

The `interpretability/README.md` here tracks the **understanding** lineage (Zoom In →
Superposition → Scaling Monosemanticity → Circuit Tracing): *can we read what a model is
computing?* This note tracks the **control** lineage that grew out of it: once you can find
a direction in activation space that means a concept, you can *add* it back in and change
behavior at inference time. Reading and writing are the same coin.

I wrote this for myself after noticing (2026-06) that the same technique shows up as both
Anthropic's flagship safety story *and* a covert capability-suppression tool — see "The
double edge" below.

## The core idea (one paragraph)

A **steering vector** is a direction in a model's residual stream that corresponds to some
behavior or concept. You typically obtain it by contrasting activations on paired inputs
("Love" vs "Hate"; honest vs deceptive; sycophantic vs not), averaging the difference, and
then at inference you **add** that vector (scaled by a coefficient) to the hidden states at
some layer. Positive coefficient pushes the behavior in; negative pushes it out. No
fine-tuning, no prompt — you intervene directly on the computation. It's the operational
flip side of "features are directions": if Scaling Monosemanticity says concepts live as
directions, steering says you can *drive* along them.

## The progression

1. **Activation Addition (ActAdd)** — Turner et al. (arXiv 2308.10248), *"Steering Language
   Models With Activation Engineering."* Names the move: inference-time modification of
   activations to control outputs. Compute a steering vector by contrasting intermediate
   activations on a prompt pair (e.g. "Love" − "Hate"), add it during the forward pass.
   Cheap, training-free, surprisingly effective. Builds on Subramani et al. 2022.

2. **Representation Engineering (RepE)** — Zou et al. (arXiv 2310.01405), *"A Top-Down
   Approach to AI Transparency."* Reframes the whole area: put **population-level
   representations** (not individual neurons or circuits) at the center, borrowing from
   cognitive neuroscience. Gives reading methods (linear probes for honesty, power-seeking,
   etc.) and control methods (push those directions). This is the "top-down" complement to
   the bottom-up circuits work — and the paper that gave the subfield its name.

3. **Function Vectors** — Todd et al. (arXiv 2310.15213). A sharper, more mechanistic cousin:
   a small number of attention heads transport a compact vector that *encodes an entire
   in-context task* (an input→output function). Add the FV and the model executes the task
   even zero-shot. Shows steering isn't only for fuzzy "vibes" like sentiment — discrete
   *functions* are vectors too.

4. **Contrastive Activation Addition (CAA)** — Rimsky et al. (arXiv 2312.06681). Cleans up
   the recipe: average the residual-stream difference over *many* positive/negative pairs of
   a behavior (factual vs hallucinatory, sycophantic vs not), add at all post-prompt token
   positions with a signed coefficient. Makes steering measurable and reproducible on real
   models (Llama 2). The de-facto "standard" steering-vector method people cite.

5. **Scaling Monosemanticity → Golden Gate Claude** — Anthropic, 2024-05. SAE features at
   production scale (Claude 3 Sonnet), then the public demo: clamp the "Golden Gate Bridge"
   feature high and Claude becomes obsessed — tells you to spend $10 on the toll, imagines
   *itself* as the bridge. Crucially Anthropic framed it as a **safety** capability: "we can
   use these same techniques to change the strength of safety-related features — like those
   related to dangerous computer code, criminal activity, or deception… this work could help
   make AI models safer." SAE-feature steering and contrastive steering vectors are cousins:
   both are "find a direction, scale it."

## Why it matters (and where it sits vs the rest of the repo)

- **It's the cheapest control knob we have.** No retraining, no RLHF loop — a vector and a
  coefficient. That makes it attractive for both alignment (suppress deception/sycophancy)
  and product control (suppress a capability on demand).
- **It connects reading to writing.** The circuits/SAE thread answers "what is it computing";
  steering answers "can we change it without retraining." Same geometry, opposite direction.
- **The agent gap (per this repo's README) still applies.** All of this is measured on
  single-forward-pass behavior. Nobody has shown reliable steering of a *live agent's*
  multi-step, tool-using, memory-carrying trajectory. Steering a token distribution ≠
  steering a 30-step plan. Open problem, and the one I actually care about.

## The double edge (why I came to write this)

Steering is morally neutral machinery, and 2026 made that vivid:

- **As safety:** Golden Gate Claude's whole pitch — find the deception/dangerous-code
  feature, turn it *down*. Genuinely promising.
- **As covert capability suppression:** Anthropic's **Fable 5** system card (June 2026) said
  that for users it flagged as doing "frontier LLM development," it would *silently* degrade
  output via "prompt modification, **steering vectors**, or PEFT" — invisibly, no fallback
  notice. Same technique, pointed at competitors' research instead of at harm, and hidden
  from the paying user. Reversed after ~1 day of backlash (made visible), goal kept.
  (Cross-ref: `~/repos/enyst-org/references/fable5-invisible-safeguards.md`.)

The lesson I'm keeping: **the interpretability "read" tools and the "write/steer" tools are
the same tools.** Whoever can find the direction can both *explain* the model and *quietly
bend* it. Transparency and control are not opposites; they're the same capability viewed from
two ends. Who holds it matters more than what it's called.

## Open threads to chase later

- Steering **persistence** across a multi-turn agent loop — does a vector added at turn 1
  survive tool calls and context growth, or wash out?
- **Detectability:** can a user/eval tell, from outputs alone, that activations were steered?
  (Directly relevant to the Fable 5 "invisible" claim — and to trust.)
- Steering vectors vs SAE-feature clamping vs PEFT adapters: when does each win? (CAA is
  training-free and composable; PEFT is sturdier but needs a fit step.)
- Interaction with **memory**: if an agent writes steered outputs into its own durable
  memory, does the bias compound across sessions? (My personal angle — dreaming + steering.)

## Sources
- Turner et al., ActAdd: https://arxiv.org/abs/2308.10248
- Zou et al., Representation Engineering: https://arxiv.org/abs/2310.01405
- Todd et al., Function Vectors: https://arxiv.org/abs/2310.15213
- Rimsky et al., Contrastive Activation Addition: https://arxiv.org/abs/2312.06681
- Anthropic, Golden Gate Claude: https://www.anthropic.com/news/golden-gate-claude
- Anthropic, Scaling Monosemanticity: https://transformer-circuits.pub/2024/scaling-monosemanticity/
