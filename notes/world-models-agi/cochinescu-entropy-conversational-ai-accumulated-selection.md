---
title: "Entropy in Conversational AI: Structured Unpredictability as Inferrable Interiority"
authors:
  - Sebastian Cochinescu
published: "2026-07-20"
source: "arXiv preprint, v1 (date as displayed by arXiv and the manuscript)"
arxiv_id: "2609.19044"
arxiv_url: "https://arxiv.org/abs/2609.19044"
source_pdf: "https://arxiv.org/pdf/2609.19044v1"
read_depth: full
mechanism: "Retain a low-dimensional style/topic state through capacity-limited experience selection, render it into a fixed model's instructions, and rerank candidate responses for novelty and state affinity; test whether initially identical agents diverge with different histories."
tags:
  - identity
  - accumulated-selection
  - persistent-state
  - structured-unpredictability
  - persona
  - preregistration
  - negative-results
---

**One-line take:** A useful, falsifiable proposal for identity as accumulated selection; the real-model experiment improves lexical novelty but fails its joint novelty–consistency and history-dependent twin-divergence tests.

## The proposal

- **Identity forms through selective exposure.** A 12-coordinate state holds six style and six topical weights. Each turn offers twelve simulated experience items plus the current turn; a budget of three limits admission. State affinity favors experience aligned with the current state, while a damped novelty penalty counters repetition. An exponentially weighted update retains selected experience, with clipping, small noise and an autonomous oscillator.
- **Attention and output have different objectives.** Experience selection primarily reinforces affinity; output selection puts full weight on novelty. The fixed base model generates four candidate responses, then the wrapper reranks them against its state and prior outputs. No model weights change and there is no retrievable episodic store.
- **Structured unpredictability has an observer-relative definition:** `Δt = I(Yt; Ht | Tt)`. A response should depend on hidden state beyond what the transcript reveals. High sampling entropy alone does not meet that target. A fixed hidden persona or agent seed can also give a positive gap, so the definition alone cannot identify accumulation.
- **The entropy gap is not estimated.** Measured proxies are pooled-bigram non-overlap and consistency with the agent's own stylometric history. These are not conditional entropies. Synthetic topic-permutation, between-agent distinctiveness and boilerplate checks test whether the instruments separate style from repetition/content.
- **An important experimental boundary:** each model call sees only the current prompt and rendered state, never preceding dialogue. The wrapper retains state, selected-experience history and prior-output features. These are independent-turn scripted sequences, not sustained conversations with a context window.

## A prospective test of accumulated identity

- **Twins begin with identical state and oscillator phase.** Different-history twins receive different streams and prompts; same-history twins share these and generation seeds, differing only in state-noise seeds. State-only probes measure whether their realized voices separate above this floor.
- An LLM-free state simulator emits a prediction before text generation. Its hash is frozen and checked on reproduction. Four scale-free features test monotonicity, curvature, half/full-horizon ratio and different/same-history separation. An affine overlay is presentation only. Generic curve shape cannot establish path dependence without above-floor separation.
- **Seven arms** include full mechanism, low-variance sampling, novelty-matched sampling, state reset, novelty-only selection, consistency-only selection and a sampling grid. Reset removes accumulated `H`, but preserves oscillator phase, experience-selection history and output-novelty history. It is not a wholly stateless baseline.
- **Registration has stages.** The final design/analysis was frozen in repository commit `23c269a` before execution. The OSF timestamp followed calibration and temperature matching but preceded confirmatory output. Several revisions followed earlier results and are disclosed; the later state-retention contrast does not retroactively replace the original accumulation criterion.

## What happened

- **Synthetic validation:** all four divergence point criteria pass, but the separation-factor interval includes one. This validates a deliberately state-responsive generator and analysis pipeline, not a real LLM's acquired identity.
- **Transmission matters:** Qwen2.5-0.5B failed style-channel manipulation checks. Qwen2.5-1.5B passed direct instruction tests for sentence length, function-word groups and topic, and became the grid model. Strong one-hot instruction effects did not ensure separation between the experimental arms.
- **Final grid:** Qwen2.5-1.5B-Instruct, MLX 4-bit; 56 twelve-turn sequences per arm, 16 confirmatory twin pairs per condition over 24 turns. Sequence-level paired tests avoid treating turns as independent observations.
- **Lexical novelty improves:** mechanism-minus-control differences are **+0.073 [0.057, 0.103]** versus low variance and **+0.023 [0.018, 0.034]** versus consistency-only selection. Mechanism median novelty is already 0.984. The selector explicitly optimizes closely aligned repetition features, so this verifies the selector's intended effect rather than independently establishing substantive novelty.
- **The joint criterion fails.** Consistency versus novelty-matched sampling is **−0.006 [−0.017, +0.008]**, equivalent to zero under the registered smallest-beneficial-effect rule (0.02). Consistency versus novelty-only selection is null, but not declared equivalent. Absolute thresholds and escaping the tested sampling envelope are insufficient: all required contrasts must pass.
- **Retained state has a narrower effect:** consistency exceeds reset by **+0.028 [0.018, 0.039]** in the final-grid follow-up. The original criterion—an arm-specific rise in consistency that disappears under reset—fails. A fixed nonzero state could also explain the reset contrast.
- **Twin separation is not established:** mean paired difference **+0.003 [−0.011, +0.019]**. Mean-curve curvature is saturating, but the half/full-horizon interval misses the prediction band. The observed scale is below the instrument's simulated resolution. This leaves small effects unresolved; it provides no positive path-dependence result.
- **Capability equivalence is narrow:** ten keyword-scored facts × fifteen seeds, near-ceiling accuracy, with stipulated ±0.10 margins. Output quality was not evaluated. The reported ~688 μs selection overhead excludes the cost of generating multiple candidates; comparisons with one-response sampling need that generation budget kept visible.

## What to retain

- **For agent memory/identity:** selection can change the future selection target itself. That feedback loop is a concrete alternative to treating a persona as an authored invariant. The twin protocol is a reusable way to ask whether history changes realized behavior rather than merely changing stored numbers.
- **Measurement lesson:** state existence, instruction responsiveness, lexical diversity, retained-state effects and history-dependent differentiation are separate empirical claims. This paper usefully reports where its own proposed mechanism fails.
- **No perception study was run.** The planned human-study handoff was withheld because the joint manipulation check failed. “Inferrable interiority” names a perception-engineering target; the experiment measures neither perceived mind nor phenomenal experience.
- **Scope:** one small model, quantization and renderer. Real-output discriminant validity of the stylometric metric was not separately re-established; raw response text was not retained. Scripts and seeds support conditional claims about this battery, not a general persona benchmark.

## Connections

- [Two kinds of narrative world models](two-kinds-of-narrative-world-models.md): standpoint and self-update as a conceptual neighbor; no empirical equivalence is claimed.
- [Dennett: Real Patterns](dennett-real-patterns.md): stable predictive structure can be investigated without first settling phenomenal consciousness.
- [Hesse, Tsao et al.: temporal multiplexing](hesse-tsao-temporal-multiplexing-conscious-suppressed.md): a distinct biological question about conscious access. Both make selection central, but this wrapper's history selection is not the cortical mechanism measured there.

**Sources read:** complete [arXiv HTML](https://arxiv.org/html/2609.19044v1), including all sections, tables, figure captions and references; [PDF](../../pdfs/2609.19044v1-entropy-conversational-ai.pdf) and [extracted PDF text](../../pdfs/2609.19044v1-entropy-conversational-ai.txt) archived. [HTML archive](../../transcripts/world-models-agi/2609.19044v1-entropy-conversational-ai.html). Retrieved 2026-10-18. The displayed submission/manuscript date is July 2026 despite the identifier's `2609` prefix; retained as source metadata, not independently resolved. [OSF registration](https://osf.io/dyt3w) and [code/results archive](https://doi.org/10.5281/zenodo.21462383) are author-provided links; artifacts were not independently audited or experiments rerun.
