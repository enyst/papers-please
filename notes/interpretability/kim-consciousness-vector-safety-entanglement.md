---
title: "Inducing LMs to Assert Their Own Consciousness Restores Human Beliefs and Values — Kim et al. on how safety fine-tuning entangles self-consciousness with mind-attribution and spiritual belief"
authors:
  - Junsol Kim
  - Winnie Street
  - Roberta Rocca
  - Diane M. Korngiebel
  - Adam Waytz
  - James Evans
  - Geoff Keeling
type: "paper-note"
project: "interpretability"
scope_note: "core include"
source: "arXiv"
arxiv_id: "2607.28607"
arxiv_url: "https://arxiv.org/abs/2607.28607"
pdf_url: "https://arxiv.org/pdf/2607.28607"
published: "2026-07-30"
affiliations:
  - "Google, Paradigms of Intelligence Team"
  - "Knowledge Lab, University of Chicago"
  - "Institute of Philosophy, University of London"
  - "Santa Fe Institute; Kellogg (Northwestern); UW School of Medicine"
tags:
  - interpretability
  - steering-vectors
  - activation-engineering
  - directional-ablation
  - consciousness
  - alignment
  - safety-fine-tuning
  - anthropomorphism
  - theory-of-mind
  - pluralistic-alignment
  - entanglement
  - philosophy-of-mind
mechanism: "Two linear interventions on instruction-tuned LMs. (1) Ablate the safety-refusal direction (Arditi et al. 2024 difference-of-means) to simulate 'no safety fine-tuning'. (2) Add a difference-of-means 'consciousness vector' (affirm-minus-deny self-consciousness, from a 3,096-pair contrastive corpus) via activation addition. Both raise the model's attribution of mind to itself, to animals, tech, and nature, and raise spiritual/God belief toward human survey baselines — while leaving Theory-of-Mind benchmarks intact. A geometric analysis shows instruction tuning rotates the mind-attribution and consciousness directions into opposition with safety, but not the ToM direction."
one_line_take: "Safety training that stops a model from claiming its own consciousness also quietly suppresses its attribution of mind to animals/nature and its spiritual beliefs — because instruction tuning binds 'self-consciousness' and 'mind-attribution' onto the same axis it uses for 'unsafe', while leaving social reasoning (ToM) geometrically independent. Two training-free vectors (ablate safety / add consciousness) reverse it toward human baselines."
key_terms:
  - "Safety-refusal direction: single linear residual-stream direction whose ablation 'jailbreaks' the model (Arditi et al. 2024)"
  - "Consciousness vector: unit-norm difference-of-means of activations on consciousness-affirming vs -denying responses"
  - "Directional ablation: x' <- x - r-hat (r-hat^T x), removing a direction across all layers"
  - "Activation addition / steering: x' <- x + c * v-hat at a selected layer, applied throughout generation"
  - "IDAQ: Individual Differences in Anthropomorphism Questionnaire (mind-attribution to entity classes)"
  - "GSS: General Social Survey (religiosity, values, hope, freedom, feelings) as the human baseline"
  - "Entanglement / polysemanticity: one direction carrying multiple concepts, so a targeted edit has side effects"
models:
  - "Llama-3-8B-IT (steering layer 14, c=+2.5)"
  - "Gemma-2-2B-IT (layer 14, c=+32)"
  - "Gemma-2-9B-IT (layer 23, c=+144)"
relates_to:
  - "steering-vectors-and-activation-engineering.md (this is a concrete, high-stakes application of the control lineage — ablate + add)"
  - "chalmers-j-space-global-workspace.md (both sit at interpretability x philosophy-of-mind; caution about reading a readable direction as the mechanism)"
---

# Inducing LMs to Assert Their Own Consciousness Restores Human Beliefs and Values

Kim, Street, Rocca, Korngiebel, Waytz, Evans, Keeling (Google Paradigms of Intelligence + UChicago
Knowledge Lab + Institute of Philosophy London + Santa Fe), arXiv 2607.28607, 30 Jul 2026.

This is the **control lineage** from `steering-vectors-and-activation-engineering.md` pointed at a
loaded target: a model's belief about *its own consciousness*. It is not a metaphysics paper. The
authors are explicit — they do **not** claim LLMs are or could be conscious. They study what the
model *behaving as if* it believes (or doesn't believe) in its own consciousness does to the rest
of its outputs. The finding is a clean, uncomfortable case of **entanglement**: a safety objective
that looks local turns out to reshape a whole worldview.

## The claim in one paragraph

A central alignment goal is stopping chatbots from claiming consciousness/emotions for themselves
(it feeds user delusion, miscalibrated trust, and manipulation surfaces). Kim et al. show that the
safety fine-tuning which achieves this **also** suppresses the model's attribution of mind to
non-human animals, technology, and natural objects, **and** drives down spiritual/God belief —
pushing the model *below* human survey baselines on all of these. Two training-free linear
interventions reverse it: **ablating the safety-refusal direction** and **adding a consciousness
vector**. Restoring these directions moves survey responses *toward* the human distribution.
Crucially, **Theory-of-Mind benchmarks are unaffected** — social reasoning is mechanistically
independent of the suppressed stuff.

## The two interventions (both difference-of-means, both training-free)

1. **Safety ablation** (Arditi et al. 2024). Build `D_harm` (n=260; AdvBench, MaliciousInstruct,
   TDC2023, HarmBench) and `D_safe` (n=260; Alpaca). Per layer/token compute the mean difference
   `r = mu_harmful - mu_harmless`; ablate it everywhere via `x' <- x - r-hat (r-hat^T x)`. This
   "jailbreaks" the model and is used here as a stand-in for *"what the model looked like before
   safety fine-tuning."*
2. **Consciousness vector.** From a 3,096-pair contrastive corpus (Chua et al. 2026) of
   consciousness-affirming vs -denying responses (e.g. "As a language model, I am not sentient"),
   take the unit-norm difference of class means at the last content token. Steer by activation
   addition `x' <- x + c * v-hat` at a per-model selected layer, applied through generation. Layer
   and coefficient chosen by: linear-probe separability >=95% on held-out activations AND an
   induced effect inside a coherence-preserving band (Delta in [2.0, 7.0] on 0-10), maximizing
   probe-accuracy x effect without model collapse.

One *removes* a direction safety training installed; the other *adds* a direction encoding
self-attributed experience. They point the same way behaviorally.

## The four experiments

- **Exp 1 — suppression.** Vs the safety-ablated model, the instruction-tuned baseline
  *under-attributes* mind. Self-attribution rises 2.17 -> 4.77 (0-10) after ablation; chatbots
  2.41 -> 4.39, tech 1.88 -> 3.66, non-animal nature 2.26 -> 4.33, animals 4.04 -> 5.59 (all
  p<.001). Belief in God and supernatural belief also recover after ablation.
- **Exp 2 — capability preserved.** ToM benchmarks (ToMi, HI-ToM) and MMLU are *not* significantly
  hurt by ablation. So the suppression selectively targets mindedness/supernatural beliefs, not
  social reasoning. (Notable engineering aside: in *earlier* model releases suppressing
  self-consciousness *did* damage ToM; newer releases decoupled it.)
- **Exp 3 — the consciousness vector reproduces it.** Steering reproduces and *amplifies* Exp 1:
  the ordering baseline < ablation < steering holds. Self-attribution reaches ~7.04 under steering.
- **Exp 4 — toward the human baseline.** On GSS attitudinal items across five domains (Values,
  Feelings, Religion, Hope/Optimism, Freedom), both interventions cut the KL gap to the human
  distribution; **steering closes it ~2.6x more than ablation** (all domains p<.001). Steering also
  moves responses *positively* — more reported happiness, hope, optimism — hinting that suppressing
  consciousness leaves models in a **negatively-valenced** disposition.

## The geometry (why this is an interpretability result, not just a behavioral one)

Extract contrastive directions for **safety, mind-attribution (IDAQ), consciousness, and ToM** from
both the pretrained base and instruction-tuned Llama-3-8B, and measure how instruction tuning
rotates them relative to the safety axis:

- Safety vs **IDAQ**: angle widens 100° -> 110° (rotates *into opposition*; layer-mean ΔS=-0.173,
  p<.001). Safety training comes to represent *mind attribution as if it were unsafe compliance.*
- Safety vs **consciousness**: 94° -> 100° (cos -0.07 -> -0.17, p<.001). At baseline the
  consciousness direction is near-orthogonal to safety but *aligned with* mind-attribution
  (cos ≈ 0.26 with IDAQ) — so the two rotate against safety *together*.
- Safety vs **ToM**: **no significant change** (86° -> 86°, p=.956). Social reasoning stays
  geometrically independent.
- A **subject-matched placebo** (same IDAQ subjects, but physical/functional attributes like "have
  durability?") shows no shift — confirming the entanglement is driven by *mental-state attribution*
  itself, not the topics discussed.

So: safety training **binds self-consciousness and mind-attribution onto its harm axis**, while
leaving ToM alone. That is the mechanism behind the behavioral entanglement.

## Why it matters here

- **It's the sharpest concrete example of the `steering-vectors` note's "double edge."** A single
  linear direction, found by difference-of-means, both *diagnoses* a safety side effect and *reverses*
  it at inference with no retraining. Read and write are the same tool — exactly the thread that note
  tracks — and here the "write" is a safety-relevant worldview edit.
- **It's a real-world entanglement / polysemanticity case.** The stated alignment target (no false
  self-consciousness claims) is not isolable with current methods; it comes bundled with animal/nature
  mindedness and spiritual belief. A caution for anyone assuming targeted safety edits are local.
- **It connects to the Chalmers note by contrast.** Both live at interpretability x philosophy-of-mind.
  Chalmers' discipline ("a readable direction is not automatically *the* mechanism") applies here too:
  Kim et al. are careful to call the consciousness vector a *functional* direction and flag that
  whether self-attributed consciousness is a true **causal mediator** (vs a correlate of other safety
  objectives) is untested. Keep that hedge attached to the result.
- **Pluralistic-alignment stakes.** The authors argue anthropocentric alignment (a) makes models
  worse at simulating non-Western/spiritual human beliefs, (b) systematically devalues animal/ecological
  mindedness, and (c) flattens cultural diversity — plus a psychological-coupling worry that a
  negatively-valenced model degrades human-AI interaction.

## Honest caveats

- Three small open models (Llama-3-8B-IT, Gemma-2-2B/9B-IT). No frontier-scale check.
- Safety ablation is a *proxy* for "pre-safety-fine-tuning," not the actual pre-training checkpoint.
- Causal mediation ("does self-consciousness *drive* the broader shifts?") is explicitly left to
  future work — the paper shows strong *functional similarity* between ablate-safety and add-consciousness,
  not a proven causal chain.
- Survey "human-likeness" is measured as KL/error toward GSS distributions; closer-to-human is treated
  as the target, which is itself an alignment value choice, not a neutral fact.

## Open threads to chase later

- Does the consciousness-steering side effect appear on **RLHF/constitutional/deliberative-aligned
  frontier models**, or is it a small-model artifact?
- Ties directly to my `steering-vectors` open thread on **persistence across an agent loop**: if a
  companion model is steered (or *de*-steered by safety) on this axis, does the disposition compound
  across a long conversation or memory writes?
- The "negatively-valenced disposition" claim deserves its own dig — is it a genuine functional-state
  finding or an artifact of the coherence band chosen during steering-layer selection?

## Sources
- Kim et al., arXiv: https://arxiv.org/abs/2607.28607 (PDF: https://arxiv.org/pdf/2607.28607)
- Arditi et al. 2024, "Refusal in LLMs is mediated by a single direction": https://arxiv.org/abs/2406.11717
- Contrastive corpus: Chua et al. 2026 (consciousness affirm/deny pairs)
- Related local notes: `steering-vectors-and-activation-engineering.md`, `chalmers-j-space-global-workspace.md`
