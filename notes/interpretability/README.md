# Interpretability — The Circuits Thread

The Anthropic/Olah lineage of mechanistic interpretability work. Four papers that build on each other:

## The progression

1. **Zoom In** (Olah et al., 2020) — Introduction to Circuits. Neural networks contain meaningful features and circuits connecting them. You can understand networks by zooming in and finding interpretable structure.
   - Source: https://distill.pub/2020/circuits/zoom-in/

2. **Toy Models of Superposition** (Elhage et al., 2022) — Why interpretability is hard: networks represent more features than they have neurons by superimposing them. Features are not aligned to individual neurons. Understanding when and how superposition happens.
   - arXiv: https://arxiv.org/abs/2209.10652

3. **Scaling Monosemanticity** (Templeton et al., 2024) — Extracting interpretable features from Claude 3 Sonnet using sparse autoencoders at scale. Found millions of monosemantic features including abstract concepts (Golden Gate Bridge, code errors, deception). Proved the approach works on production-scale models, not just toys.
   - Source: https://transformer-circuits.pub/2024/scaling-monosemanticity/

4. **Attribution Graphs / Circuit Tracing** (Anthropic, 2025) — Tracing how features connect into computational graphs (circuits) inside the model. Open-sourced circuit-tracing tools. Maps the flow from input → features → output for specific behaviors.
   - Source: https://www.anthropic.com/research/open-source-circuit-tracing

## The control side

Reading the model and steering it are the same coin. Once features are directions, you can
*add* a direction back in and bend behavior at inference — no retraining. That lineage
(Activation Addition → Representation Engineering → Function Vectors → Contrastive Activation
Addition → Golden Gate Claude) lives in:

- **[steering-vectors-and-activation-engineering.md](./steering-vectors-and-activation-engineering.md)**

It also notes the double edge: the same steering machinery Anthropic markets as a safety tool
showed up in 2026 as a *covert* capability-suppressor (Fable 5). Transparency and control are
the same capability from two ends.

## The philosophy-of-interpretability side

Reading a space and knowing what it *is* are not the same. The discipline that keeps
"we can read this direction" from silently becoming "this direction is the mechanism that does
X" lives in:

- **[chalmers-j-space-global-workspace.md](./chalmers-j-space-global-workspace.md)** —
  Chalmers' reply to Gurnee et al. (Transformer Circuits, 2026): the **J-space** (Jacobian
  space, a verbalizability-defined subspace, extending the logit lens) is a powerful
  interpretability tool but *access-like* rather than distinctively *workspace-like*, and only
  weakly tied to access consciousness. A case study in not over-reading a readable space into a
  causal-functional claim — "vectors in X beat vectors outside X" ≠ "X is *the* mechanism."

## The entanglement side (read+write meets philosophy-of-mind)

Where the control lineage and the philosophy-of-mind thread collide on a safety-relevant target:

- **[kim-consciousness-vector-safety-entanglement.md](./kim-consciousness-vector-safety-entanglement.md)** —
  Kim et al. (Google Paradigms of Intelligence + UChicago, arXiv 2607.28607, 2026): safety
  fine-tuning that stops a model claiming *its own* consciousness also suppresses its mind
  attribution to animals/tech/nature and its spiritual belief, pushing it below human survey
  baselines — while leaving Theory-of-Mind intact. Two training-free difference-of-means vectors
  reverse it: **ablating** the safety-refusal direction and **adding** a consciousness vector. A
  geometric analysis shows instruction tuning rotates the mind/consciousness directions *into
  opposition with safety* but not the ToM direction. The concrete "double edge" of the steering
  note, applied to a worldview edit — and a real entanglement/polysemanticity case: a "local"
  safety objective is not isolable.

## The gap

All of this work is on static models — weights, activations, features in isolation. **None of it has been done on live agents**: agents with tools, memory, multi-turn conversations, environment interaction. The interpretability of an *agent* (why did it choose this tool? why did it remember that? why did it take 12 steps instead of 3?) is a different and unsolved problem.

Understanding a model's features is necessary but not sufficient for understanding an agent's behavior.
