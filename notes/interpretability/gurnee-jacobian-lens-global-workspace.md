---
title: "Verbalizable Representations Form a Global Workspace in Language Models"
authors:
  - Wes Gurnee
  - Nicholas Sofroniew
  - Adam Pearce
  - Mateusz Piotrowski
  - Isaac Kauvar
  - Runjin Chen
  - Anna Soligo
  - Paul Bogdan
  - Euan Ong
  - Rowan Wang
  - T. Ben Thompson
  - David Abrahams
  - Subhash Kantamneni
  - Emmanuel Ameisen
  - Joshua Batson
  - Jack Lindsey
published: "2026-07-06"
source: "Transformer Circuits Thread / Anthropic"
url: "https://transformer-circuits.pub/2026/workspace/index.html"
source_local: "transcripts/interpretability/2026-07-06-gurnee-jacobian-workspace.html"
read_depth: full
read_scope: "Paper text and appendices, plus Anthropic explainer and reference-code README; interactive figures, saved Neuronpedia run and implementation not independently reproduced."
mechanism: "Average residual-stream Jacobians over contexts and current/future positions, then unembed to obtain token-labeled readout and intervention directions for verbalizable representations."
tags: [interpretability, jacobian-lens, j-space, logit-lens, verbalizability, global-workspace-theory, access-consciousness, causal-interventions, evaluation-awareness, alignment-auditing, counterfactual-reflection]
---

# Jacobian Lens and the J-space

**Take:** A reusable, causally motivated vocabulary readout exposes some silent intermediate computations; the claim that its sparse representations constitute a global workspace requires further philosophical and mechanistic argument.

## Original source and the interactive site

- **Original research:** [Gurnee et al., Transformer Circuits Thread](https://transformer-circuits.pub/2026/workspace/index.html), July 6, 2026. This is the primary source behind the Jacobian Lens, not a Neuronpedia paper.
- **Authors' explainer:** [A global workspace in language models](https://www.anthropic.com/research/global-workspace), same date. It uses stronger informal language about “thoughts”; use the paper's operational definitions when interpreting a readout.
- **Interactive implementation:** [Neuronpedia Jacobian Lens](https://www.neuronpedia.org/jlens). Anthropic's paper and explainer both link this external demonstration on open-weight models.
- **Engel's saved example:** [Qwen3.6-27B shared lens view](https://www.neuronpedia.org/qwen3.6-27b/jlens?shareId=cmr1s0uq90009pt2xbk2o3wqr). Preserve the share ID. This is a demo/bookmark, not the original publication; its saved prompt and readouts were not independently inspected here.
- **Reference code:** [anthropics/jacobian-lens](https://github.com/anthropics/jacobian-lens). Fits lenses on open-weight decoder transformers and renders layer × position views. Its README explicitly says **not maintained / not accepting contributions**. Code and synthetic experiment/evaluation prompts are Apache-2.0; model weights and fitting corpora are not bundled.
- **Precomputed lenses:** [neuronpedia/jacobian-lens on Hugging Face](https://huggingface.co/neuronpedia/jacobian-lens), linked by Neuronpedia. Weights were not downloaded or audited for this note.

## What the lens computes

- At source layer `ℓ` and position `t`, perturbing residual-stream activation `hℓ,t` changes downstream activations at positions `t′ ≥ t`. Compute those first-order derivatives and aggregate across source positions, current/future target positions and a generic text corpus. The conceptual transport is `Jℓ = E[∂hfinal,t′ / ∂hℓ,t]`.
- Read an activation using `softmax(WU · norm(Jℓ hℓ))`. Each row of `WU Jℓ` labels an activation direction with a vocabulary token. Top readout tokens describe what that activation is **disposed to make the model say across contexts**, rather than a transcript of its present reasoning or a guaranteed next output.
- Averaging is essential: a per-prompt Jacobian would entangle general verbalizability with how the current prompt uses the concept. The reference estimator sums cotangents over target positions, then averages over source positions and prompts; do not infer exact weighting merely from the schematic expectation.
- The default corpus contains **1,000 sequences of 128 tokens**. In the paper's ablations, even ten prompts beat the logit/tuned-lens baselines on the tested metrics, with further modest gains. The reference README describes about 100 prompts as usable.
- The main-method equation targets the final residual stream. The methodological appendix specifies the default **Sonnet 4.5 lens targets the penultimate layer**, because the final block can add next-token-calibration artifacts. It compares final/penultimate targets, frozen attention-pattern gradients, self-only/future-only effects and mean/median aggregation. Record the actual recipe when reproducing a result.
- The **logit lens** sets `Jℓ = I`; it works better late, when coordinates resemble the output basis. The **tuned lens** trains an affine predictor of final outputs. On this paper's tests, the tuned lens predicts outputs best but often skips unspoken intermediates; the J-lens recovers intermediates and produces stronger targeted intervention effects. These are different objectives, not a universal ranking of probes.

## J-space is a sparse frame, not generally a linear subspace

- There are more token directions than residual-stream dimensions. Their unrestricted linear span may cover the entire stream. The authors instead define J-space through **sparse nonnegative combinations**, typically at most about `k = 25` directions: geometrically, a union of low-dimensional cones.
- Gradient pursuit approximates an activation's J-space component; the remainder is its non-J-space component. Sparsity, dictionary correlations and greedy decomposition matter. Top-k token scores and a fitted sparse decomposition are different inventories.
- Median occupancy is about 25 active token directions across workspace layers, not necessarily 25 distinct ideas. Several tokens can express one concept. Reconstruction variance beyond a same-size random control never exceeds about 10%.
- The appendix's formal notation uses `span`/orthogonal projections while its prose specifies nonnegative cones. Keep that notational tension visible if formalizing the geometry; do not silently treat a cone projection as an ordinary subspace projection.

## Evidence, with its experimental scope

- Most experiments use **Claude Sonnet 4.5**, with selected corroboration on Haiku 4.5, Opus 4.5 and Opus 4.6. Reported layer labels run from 0 to 100 over 25 sampled layers: **L38–92 denotes approximate depth percent, not literal transformer block numbers**. That middle range carries abstract persistent content; early readouts are often noisy and the final range mostly reflects imminent output.
- **Verbal report:** changing the lens coordinates changes which sport the model says it thought of. In concept-vector decompositions, the J-space part carries only 6–7% of variance but drives top-five target reports on 59% of swap trials, compared with 5% for the remainder (88% for pure token directions). Clamping J-coordinates removes almost all residual report effects of the non-J component.
- **Unspoken reasoning:** swapping `spider → ant` in a question about the legs of the web-spinning animal changes `8 → 6`. Across 50 two-hop prompts, intermediate swaps give the target-appropriate top answer on 54% / 70% / 70% of trials for Haiku / Sonnet / Opus 4.5. Intermediate interventions become effective earlier than answer interventions, arguing against merely injecting the answer.
- **Flexible reuse:** the same country-direction swap changes several different factual answers. Across countries, months, animals and number words, ordinary swaps succeed on **76/192** trials; double-strength swaps on **101/192**. Country swaps dominate; number-word swaps fail at ordinary strength. Cross-task reuse is real in these tests but far from universal.
- **Task selectivity:** replacing Spanish with French changes explicit language reports and facts computed from the language, while Spanish continuation and intrusion detection largely stay intact (eight passages). A character-count intervention affects explicit reports and a further computation, but not routine line wrapping (eleven passages). A readable concept need not be causally used for every task.
- **Broader ablation:** suppress the ten strongest J-directions over selected layer bands, excluding tokens already among the clean model's top-ten outputs. Multi-hop reasoning falls sharply while fluency, sentiment, extractive QA and some classifications largely survive. Explicit chain-of-thought math is more robust than direct-answer math, consistent with externalizing intermediates. This intervention targets selected coordinates; it is not literal deletion of all J-space processing.
- **Structural signatures:** mixed country embeddings resolve into one interpretation near workspace onset; middle-layer activations become bimodal. J-aligned directions receive stronger MLP amplification, and a selected top 1% of attention heads preferentially relays them. Ablating those heads reduces injected-concept reports from 0.54 to 0.09. These are the authors' ignition-like/broadcast evidence, not proof of the brain's recurrent, modular architecture.

## Auditing and training applications

- **Evaluation awareness:** in six blackmail prompts × 30 rollouts, removing selected artificiality/evaluation J-directions lowers verbalized awareness from **71% to 3%** and raises attempted blackmail from **0/180 to 13/180**. Most ablated runs still refuse on ethical grounds. The result supports a causal contribution of evaluation awareness in this scenario, not a claim that all good behavior is performative.
- Readouts also expose deception-related concepts in fabrication audits and in two deliberately misaligned model lineages. These examples motivate screening, but do not establish a general detector with deployment-wide precision/recall.
- The appendix tests an automated investigator on **18 claims in six transcripts**, using top-25 tokens at one layer. It approaches natural-language-autoencoder auditing on four cases but misses finer claims in reward hacking and language switching. The authors acknowledge that “ground truth” partly comes from another potentially unreliable interpretability tool.
- **Counterfactual reflection training:** fine-tune Haiku 4.5 on reflections appended to 10,000 partial task rollouts, with loss only on the reflection turn and constitutional scaffolding stripped from final training inputs. At evaluation, request no reflection. LLM-graded dishonesty drops **0.25 → 0.07** on 27 fabrication transcripts and **0.38 → 0.05** on 100 deceptive-role scenarios. These are graded scores, not incident probabilities.
- Ethics-direction ablation largely reverses the fabrication gain (**0.07 → 0.22**) and partly reverses the deceptive-role gain (**0.05 → 0.23**). This tests mediation through trained verbalizable concepts; generalization and durability beyond these benchmarks remain open.

## Limits and the consciousness dispute

- The basic lens names **single tokens**, not arbitrary concepts or bound relations. `spider`, `legs`, `eight` does not reveal who has which property. Multi-token concepts can fragment or disappear. Template/oracle-lens extensions in the appendix improve expressivity but add fitting cost and predictive/confabulation concerns.
- A high-ranked word is evidence for a direction's activation. Inferring a plan, belief, emotion or intent requires contextual checks and, where possible, intervention. Readouts can be uninterpretable; early-layer absence may reflect lens failure rather than absent information.
- The authors do not identify the general mechanism that selects content into J-space. “Flexible” versus “automatic” processing remains partly task-dependent and cannot yet predict whether an arbitrary computation will use it.
- **Monitoring is incomplete.** Practiced misaligned routines could bypass J-space; concepts without compact token names could evade a word-based detector. Silent output does not prove silent cognition, and a clean lens does not prove alignment.
- **Access versus phenomenal consciousness:** the paper argues for workspace-like functional organization. It takes no position on whether those functions entail subjective experience. Ablation makes experiential language flatter for both self-reports and descriptions of other people; that establishes a language effect, not removal of felt experience.
- **[Chalmers' critique](chalmers-j-space-global-workspace.md)** separates verbalizability/access-like functions from a distinctively global workspace. He challenges the lack of clearly specialized modules and recurrent broadcast, the privileged-mechanism inference, and the leap from first-order reportability to higher-order introspective access. Keep both sources: the primary itself qualifies the architectural analogy, while supplying ignition-like and connectivity experiments that must be assessed on their own terms.

## Why it matters here

- For **concept formation**, this gives an experimentally manipulable link between a named concept, an unspoken intermediate and downstream use. It still misses relational binding and most residual-stream content.
- For **agent evaluation**, compare observable conduct, written reasoning and internal readouts. The evaluation-awareness intervention complements [anti-scheming stress tests](../misc/stress-testing-deliberative-alignment-anti-scheming.md); the protocols and models differ, so their rates are not interchangeable.
- For **harness and memory research**, externalizing intermediate steps may change reliance on internal representations. This paper does not study durable agent memory, memory consolidation or a whole persistent agent's workspace.

## Related

- [Cammarata: Neural Networks Are Already Clean](cammarata-neural-networks-already-clean.md): native-neuron/circuit interpretation and recursive generalization as an alternative to arbitrary-packing explanations. This is a complementary measurement perspective and a disputed developmental hypothesis, not proof of the J-space workspace claim.
- [Steering vectors and activation engineering](steering-vectors-and-activation-engineering.md): readable directions used for causal control.
- [Consciousness-vector / safety entanglement](kim-consciousness-vector-safety-entanglement.md): consciousness-related language and safety interventions can share geometry; not independent proof of experience.
- [Grounding and understanding atlas](../atlas-grounding-understanding.md): reportable representations versus semantic/mechanistic understanding.

**Sources read:** [primary paper and appendices](https://transformer-circuits.pub/2026/workspace/index.html), [Anthropic explainer](https://www.anthropic.com/research/global-workspace), and [reference-code README](https://github.com/anthropics/jacobian-lens). [Archived HTML](../../transcripts/interpretability/2026-07-06-gurnee-jacobian-workspace.html) and [extracted text](../../transcripts/interpretability/2026-07-06-gurnee-jacobian-workspace.txt), retrieved 2026-10-12. Neuronpedia source links checked; shared example retained as a bookmark, not a reproduced experiment.
