---
title: "Neural Networks Are Already Clean"
authors:
  - Nick Cammarata
published: "2026"
source: "Goodfire — informal research essay / working hypothesis"
url: "https://already-clean.goodfire.com/"
source_text: "https://already-clean.goodfire.com/essay.md"
source_local: "transcripts/interpretability/2026-cammarata-neural-networks-already-clean.md"
retrieved: "2026-10-16"
read_depth: full
read_scope: "Complete author-provided text version, all appendices, footnotes and references; HTML checked for provenance and linked artifacts. Interactive galleries, 1,000 neuron papers and experiments not independently audited."
mechanism: "Study native neurons, their positive/negative and gated regimes, local circuits and training trajectories; explain many apparent arbitrary mixtures through measurement failures and recursively branching generalization."
tags: [interpretability, goodfire, neurons, polysemanticity, superposition, recursive-generalization, composition, swiglu, circuit-tracing, automated-science, concept-formation]
---

# Neural Networks Are Already Clean

**Take:** Cammarata argues that native neurons and circuits are often directly legible once tools, architecture and developmental history are understood; his evidence challenges arbitrary-packing explanations without disproving mathematical superposition or establishing comprehensive frontier-model understanding.

## What kind of source this is

- An **informal research essay and working hypothesis**, by Nick Cammarata at Goodfire. Curt Tigges contributed much of the language-model work. The citation specifies **2026**; no exact publication day is given in the text, so the retrieval date is not used as publication date.
- **Why take it seriously:** Cammarata coauthored the early circuits and multimodal-neuron work, helped interpret the canonical examples he now revisits, and started OpenAI’s automated-neuron-interpretability project. This is an experienced practitioner revising his own picture through further experiments, not a claim that earlier researchers simply failed to look. His strongest contribution here is a set of concrete alternative explanations and ways to test them.
- This is both a research argument and an explorable collection of model evidence. The essay promises a **forthcoming technical companion paper** with fuller language-neuron methods/results. The linked [1,000 neuron papers](https://already-clean.goodfire.com/neuron-scientist/papers/) are individual automated investigations, not that promised technical report.
- Full author-provided [text version](https://already-clean.goodfire.com/essay.md) read, including appendices and footnotes. Figures there are textual descriptions. The archived HTML preserves additional interactive-page material, but no claim here that every gallery, data panel or linked investigation was inspected or reproduced.

## The thesis, with definitions kept separate

- **Polysemanticity** describes observed multiple apparent meanings. It does not by itself identify why those responses share a neuron. Candidate causes include a poor microscope, a poor explanation, poorly learned architecture, recursive generalization, or arbitrary packing.
- **Recursive generalization:** a neuron grows from a useful local pattern into related branches, and branches of those branches. Example: `iy → diy → do it yourself`, with a separate route toward Miyazaki. Endpoints can look unrelated if the developmental steps are hidden. The predicted local path through semantic space and training time is evidence to seek, not an automatic explanation for every mixture.
- **“Superposition” in this essay** chiefly means learning unrelated computations in shared mechanisms because they rarely interfere. It does **not** chiefly mean more predefined features than dimensions, any distributed representation, or rotation away from the neuron basis. Those claims are different.
- The author accepts the experiments in [Toy Models of Superposition](https://transformer-circuits.pub/2022/toy_model/index.html). He questions their transfer from reconstructing predefined features to growing reusable computations on structured natural data. “Toy superposition is real” and “arbitrary packing need not explain these natural-model neurons” can both hold.
- **“Clean” means organized and understandable through downstream readers**, not every neuron matching one familiar human noun. A neuron may gate a distinction, summarize a context, suppress an output, or do several locally related jobs. The essay favors exploratory, question-driven investigation over requiring an exhaustive feature list first.

## Vision evidence: reinterpretation, tools and architecture

- **The canonical cat/car neuron (InceptionV1 4e:55):** the proposed commonality is a **V shape**, with O-shaped objects at its negative pole. Flames, jets and fox faces provide checks beyond cats/cars. This revises the author's own earlier reading of the example as unrelated categories.
- **The car-through-dogs circuit:** generalized pose detectors and biased feature visualization can make a car route look like unrelated dogs storing a hidden car code. Optimized images fell into easy dog-generating routes; steering optimization toward paths taken by natural examples recovered car/pose structure. A synthetic maximizing image is not a full account of a neuron's normal role.
- **Architecture and tools are separate interventions.** The essay estimates old final-layer InceptionV1 readability around 0–5%; better tools around 50% on the original model; retraining the old architecture with modern regularization around 70%; a same-sized modern ConvNeXt around 99%. These are the author's rough interpretability assessments, not one standardized controlled metric. Architecture changes are not merely a better view of unchanged weights.
- Trained ConvNeXts span **92k, 7.06M and 28.6M parameters**, about 300×. Smaller models reportedly use coarser distinctions; larger ones differentiate them. Following a neuron through training shows local branching rather than sudden unrelated jobs in the inspected examples.
- **Compression tests:** cut InceptionV1 layer 3b from **480 neurons to 10**, with no residual bypass; the displayed model retains **58.35% top-1 / 81.14% top-5 ImageNet** accuracy. Its neurons remain broadly interpretable but coarse. An SAE does not recover the original set of fine curve detectors. A separate final-layer ConvNeXt bottleneck shrinks 1,024 neurons to 13. These are examples against a predicted failure mode, not an exhaustive characterization of compressed networks.
- **SAE comparison:** on the studied final layer, the essay reports **88% of SAE activity** consists of near-copies of native neurons. Removing dictionary directions matching no neuron leaves accuracy unchanged, apart from near-tie flips. Added features often group existing mechanisms by context. This is evidence from those models/layers, not a universal statement about dictionary learning.
- **Rare cases, memorization and adversarial inputs:** an umbrella relabeled as a bee changes through existing routes in nine training steps, with the last three blocks sufficient to transfer the changed answer. Some adversarial examples recruit recognizable wrong-class circuits. These demonstrate available ordinary routes; they do not rule out rare unrelated mechanisms elsewhere.

## Language evidence and the measurement lessons

- **Preliminary Qwen3-32B audit:** roughly **90% of neuron poles** have one main job with related offshoots; about **7%** have two related jobs; **2–4%** remain unexplained. These are approximate judgments sensitive to thresholds, depth, activation regime and what counts as one job; the ranges need not form a precise partition.
- A footnote gives closer to **97% non-arbitrary mixtures** on smaller, more closely inspected strong-activation samples. Do not substitute this for the broad 90% estimate. A “pole” and a whole neuron are not interchangeable units of evaluation.
- GPT-2 XL is revisited with **500 neuron papers**: about **70%** appear roughly one thing, but only about **5%** pristine. The scoring differs from the 2023 automated-interpretability project, so the old sub-2% and new 70% figures are not directly comparable accuracy measurements.
- **Positive and negative poles matter.** In the Santa example, removing eight neurons with relevant **negative** poles drops the target probability to **6%**; removing twenty neurons labeled Christmas/Santa from their usual positive examples leaves **76%**. A top-positive-only label can identify the wrong causal mechanisms.
- **SwiGLU sign regimes:** an output `SiLU(gate) × value` can be positive through either positive/positive or negative/negative factors. The latter can mix a negative-pole pattern into a positive-output list. For about **4% of neurons**, the essay says this regime dominates the top list. Whole-network removal reportedly improves several benchmarks but harms some reasoning tasks; the explanation remains underinvestigated, not a blanket optimization recommendation.
- **Attention placement:** “comma neurons” may hold accumulated context at punctuation; an apparent Colorado/comma mixture becomes a Colorado-context summary. Short text windows, insufficiently broad corpora, neglecting subsequent tokens and ignoring sign regimes can each manufacture apparent polysemanticity.
- **Language circuits:** native-neuron diagnosis graphs in Qwen3-32B and a found-wallet graph in **Kimi K3** illustrate interpretable routes without replacing MLPs with learned dictionaries. The trillion-parameter example is exploratory: the essay explicitly says full audits at that scale have not begun.
- **Experts:** the [Qwen3.6 expert map](https://already-clean.goodfire.com/#expert-organization) covers **10,240 experts**, sorted using agents' judgments of neuron summaries. Later experts reportedly become narrower. The suggestion that specialized routing discourages arbitrary packing is a plausible architectural argument; it is not a proof that MoE experts cannot pack unrelated functions.

## Explanations must survive tests

- **Blind maximum:** one investigator explains a neuron; a second sees only that explanation and writes text expected to maximize it. Such text can beat corpus examples drawn from **10 billion tokens**. That tests a hypothesized center, not full coverage of all jobs. An explanation can succeed on one facet while missing another.
- **Bundle tests:** cluster incoming attribution into subcircuits, then repeat the blind-maximum test for each with other bundles ablated. This tests more of the neuron's breadth, still without guaranteeing completeness.
- **Near misses:** for 200 randomly selected gallery neurons, an agent generates five positives and five plausible negatives per explanation. Among **183 explanations describing the positive side**, **76%** of positive examples versus **11%** of near misses cross the chosen strong-response threshold (**30% of corpus maximum**); explanations win on **164**, tie on **15**, lose on **4** neurons.
- Texts about an agent-chosen distant concept fire strongly about **1%** of the time; **179/183** neurons never fire strongly on those examples. This only tests chosen alternatives. It cannot exclude arbitrary undiscovered secondary functions, and the essay notes near misses alone cannot distinguish a well-described X-or-Y mixture from recursive generalization.
- **Simulation score is not explanation quality.** Precise activation prediction also measures attention's placement/timing, weak-response amplitudes and the simulator's numerical skill. A story can predict many observations and still miss a shared mechanism. Use adversarial examples, novel-domain tests, ablation, upstream/downstream consistency and training trajectories together.
- The author reports agents reviewing **100,000 attribution graphs**, with thousands inspected personally, but explicitly calls this qualitative evidence rather than a trusted cleanliness score. The linked 1,000 neuron investigations were not independently audited for this note.

## Weak activations, residual stream and remaining scope

- **Weak is not uniformly useless.** Early vision layers can act as graded dials; late language layers can suppress specific output tokens. Preserving final-layer InceptionV1's strongest quarter of positive activations gives **69.47% accuracy versus 70.08%** originally. ConvNeXt experiments retain a residual bypass; do not describe those interventions as erasing all weak computation everywhere.
- Weak responses often broaden into related contexts in inspected cases, but the appendix explicitly says there is **no trusted general semantic test**; wider category screening is mixed. Near-zero unrelated examples and unresolved responses remain. Average accuracy preservation cannot establish safety for rare contexts.
- **Residual-stream geometry:** a large, unread coordinate can interact with LayerNorm as a saliency control and dominate a vision projection. Removing that coordinate **from the visualization** reveals structure without changing recorded network behavior. Visualization cleanup and causal ablation are distinct operations.
- Narrowing a ConvNeXt residual stream four/eightfold lowers accuracy **72% → 60% / 39%**, while maps reportedly remain broadly organized. This is qualitative evidence about organization, not a proof of no interference or no overcomplete representation.
- **Attention remains less understood.** Local reading/writing can be followed through neuron routes; global head labels are incomplete. The author's approximately 5% “explanatory residual” estimate is explicitly low-confidence, not a measured fraction of all computation.
- **Circuit ecology / circuit racing** is the proposed developmental explanation: reusable, already-active routes capture gradients first, so new related computations grow nearby. Single-example color generalization, grokking connections and competition experiments motivate it. The essay does not derive a general theorem or rule out memorization-first regimes.

## How far the conclusion reaches

- **Supported as a research direction:** several influential messy-neuron examples deserve reinspection with natural examples, full contexts, signed/gated activations, circuit interventions and training checkpoints. Native neurons should remain part of the toolkit, not be discarded simply because early tools struggled.
- **Not established:** every neural network is legible, arbitrary packing never occurs, SAEs are obsolete, all frontier circuits have been mapped, or interpretability/safety is solved. The author explicitly acknowledges incomplete audits and that the title overstates the evidence.
- The essay's roughly **85% confidence** is the author's belief in a developmental picture, not “85% of mechanisms are understood” or an experimentally calibrated confidence interval.
- Finding plausible semantic relatives is easier than proving a complete causal explanation. Broad labels, adaptive hypothesis search and automated judging need independent held-out tests and clear failure criteria. The essay offers some such tests, but leaves much language-model methodology to the promised technical report.
- Scaling ordinary automated science into a near-term solution, and using readable circuits to make alignment straightforward, are **speculative extensions**. Human-readable mechanisms can still be numerous, hard to compose into behavioral predictions, or absent from a limited audit. An interpretable route need not be safe.

## Connections worth keeping

- **[Interpretability lineage](README.md):** this directly contests the default extrapolation from toy superposition to natural-model polysemanticity. Retain both sources and their definitions. The historical results remain; the inference about why native units look mixed is disputed.
- **[Jacobian Lens](gurnee-jacobian-lens-global-workspace.md):** vocabulary-based lens directions and native neuron mechanisms offer different views. The J-lens can help interpret what a neuron reads/writes, but token-aligned J-space is neither all neurons nor all residual content. Neither essay independently proves the other's global claim.
- **[Chalmers on J-space](chalmers-j-space-global-workspace.md):** both discussions require care when moving from a readable representation to a privileged mechanism. Here the author includes native interventions and developmental checks; labels alone still do not settle causality or completeness.
- **[Grounding / understanding atlas](../atlas-grounding-understanding.md):** recursive branching is a concrete hypothesis about **concept formation**, including paths from spelling fragments to abstract meanings. A useful shared computation may cut across human categories; language-like labels are hypotheses about it.
- **The closing motivation:** alongside safety, Cammarata wants agents to be able to understand their own mechanisms. He treats giving created systems that opportunity as valuable in itself. This is a stated motivation, not evidence for consciousness; it helps explain why he values exploratory understanding beyond an alignment checklist.
- **[Harness atlas](../atlas-harness.md):** automated investigators need broad datasets, sufficient context, signed-activation tools, interventions and durable source-linked explanations. Better model capability alone does not repair a biased microscope or weak test protocol.

## Source and exploration links

- [Essay / interactive page](https://already-clean.goodfire.com/) · [complete author text](https://already-clean.goodfire.com/essay.md).
- [Native-neuron microscope](https://already-clean.goodfire.com/microscope/medium.html) · [circuit atlas](https://already-clean.goodfire.com/circuit-atlas/index.html) · [early-training map](https://already-clean.goodfire.com/training-map.html) · [1,000 individual neuron investigations](https://already-clean.goodfire.com/neuron-scientist/papers/). Retained as exploration links, not audited artifacts.
- [Olah, *Distributed Representations: Composition & Superposition* (2023)](https://transformer-circuits.pub/2023/superposition-composition/index.html) read as terminology context. It explicitly distinguishes composition, superposition and trivial rotation, and allows mixtures. [*Toy Models* (2022)](https://transformer-circuits.pub/2022/toy_model/index.html) introduction/definitions checked: genuine synthetic demonstrations, with uncertainty about transfer to natural networks; full paper not reread for this ingest.
- [Archived author Markdown](../../transcripts/interpretability/2026-cammarata-neural-networks-already-clean.md) · [archived HTML](../../transcripts/interpretability/2026-cammarata-neural-networks-already-clean.html). Relative interactive assets in the archives require the live site; no offline mirror is claimed.

**Source:** [Nick Cammarata, Goodfire, *Neural Networks Are Already Clean*](https://already-clean.goodfire.com/), full author text and appendices read; retrieved 2026-10-16. Research essay, not independently replicated or a completed frontier-model audit.
