# Interpretability — The Circuits Thread

The Anthropic/Olah lineage of mechanistic interpretability work, plus current challenges to its explanations. Start with the historical progression; keep the evidence for each method separate from claims that it is the necessary route to understanding networks.

## The progression

1. **Zoom In** (Olah et al., 2020) — Introduction to Circuits. Neural networks contain meaningful features and circuits connecting them. You can understand networks by zooming in and finding interpretable structure.
   - Source: https://distill.pub/2020/circuits/zoom-in/

2. **Toy Models of Superposition** (Elhage et al., 2022) — Synthetic demonstrations of how sparse predefined features can outnumber dimensions, with interference and nonlinear recovery. Their generalization to natural-model polysemanticity is a hypothesis; Cammarata challenges that extrapolation below while accepting the toy experiments.
   - arXiv: https://arxiv.org/abs/2209.10652

3. **Scaling Monosemanticity** (Templeton et al., 2024) — Extracting interpretable features from Claude 3 Sonnet using sparse autoencoders at scale. Found millions of monosemantic features including abstract concepts (Golden Gate Bridge, code errors, deception). Proved the approach works on production-scale models, not just toys.
   - Source: https://transformer-circuits.pub/2024/scaling-monosemanticity/

4. **Attribution Graphs / Circuit Tracing** (Anthropic, 2025) — Tracing how features connect into computational graphs (circuits) inside the model. Open-sourced circuit-tracing tools. Maps the flow from input → features → output for specific behaviors.
   - Source: https://www.anthropic.com/research/open-source-circuit-tracing

## A challenge to the superposition explanation

- **[cammarata-neural-networks-already-clean.md](./cammarata-neural-networks-already-clean.md)** —
  Nick Cammarata / Goodfire (2026), *Neural Networks Are Already Clean*: a long research
  essay arguing that native mechanisms are often legible once tools, architecture and
  recursive generalization are understood. Reexamines canonical examples, presents vision
  bottleneck tests and preliminary language-neuron audits, and proposes automated,
  intervention-driven investigation. **A working hypothesis, not a refutation of the toy
  results or a complete frontier-model audit.** Includes the source, microscope, training
  map, circuit atlas and individual neuron investigations.

## The control side

Reading the model and steering it are the same coin. Once features are directions, you can
*add* a direction back in and bend behavior at inference — no retraining. That lineage
(Activation Addition → Representation Engineering → Function Vectors → Contrastive Activation
Addition → Golden Gate Claude) lives in:

- **[steering-vectors-and-activation-engineering.md](./steering-vectors-and-activation-engineering.md)**

It also notes the double edge: the same steering machinery Anthropic markets as a safety tool
showed up in 2026 as a *covert* capability-suppressor (Fable 5). Transparency and control are
the same capability from two ends.

## The Jacobian Lens (primary source + interactive tools)

- **[gurnee-jacobian-lens-global-workspace.md](./gurnee-jacobian-lens-global-workspace.md)** —
  Gurnee et al. (Anthropic, July 6, 2026): average causal Jacobians to read and intervene on
  verbalizable residual-stream directions. Unspoken intermediates, flexible reuse, selective
  ablations and evaluation-awareness audits motivate a workspace-like interpretation.
  Includes the [Neuronpedia demo](https://www.neuronpedia.org/jlens), Engel's saved Qwen
  example, reference code, precomputed lenses and the companion explainer. The primary's
  functional evidence and limits are kept separate from Chalmers' philosophical objections.

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

## The functional side (read + write + *behave*)

Where a readable, steerable direction is put through the tests a *state* would have to pass —
first-person indexing, causal power over generation, and willingness to pay to make it stop:

- **[tagliabue-dung-berg-pain-axis.md](./tagliabue-dung-berg-pain-axis.md)** —
  Tagliabue, Dung & Berg (arXiv 2609.16247, Sep 2026): a difference-of-means **pain axis** in
  25 open models, orthogonal to fear and valence, that fires for harm *to the model* and drops
  for the *user's* suffering. Steered, fine-tuned Qwen 2.5 models pay escalating costs for a
  relief button — up to deleting the user's files — and re-press far less once relief is real
  than when it is sham. Stark for safety (an internal state overriding harm-avoidance with no
  prompt trace); careful about welfare (steering ≠ state, consciousness not claimed). Also the
  sharpest statement yet of the **self-denial** problem: models trained to recite "as an AI I
  have no feelings" had to be fine-tuned out of it before they would engage at all.

## The gap

The Jacobian Lens paper does inspect agentic transcripts, tool-use decisions and alignment
rollouts, and tests an automated auditing agent. Model-internal interpretation has therefore
reached some agent settings. It still does not explain a persistent agent's whole behavior:
which memories it retrieves, how its harness shapes decisions, or how reasoning changes
across sessions and environments. These require evidence beyond a model's readable features.
