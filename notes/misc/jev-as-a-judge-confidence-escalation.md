---
title: "JEV-as-a-Judge: Accept When Confident, Escalate When Unsure"
authors: [Yubo Li, Yidi Miao, Ramayya Krishnan, Rema Padman]
published: 2026-09-22
source: arXiv
arxiv_id: "2609.26550"
arxiv_url: https://arxiv.org/abs/2609.26550
source_pdf: https://arxiv.org/pdf/2609.26550v5
version_read: v5 (2026-10-09)
mechanism: "Accept a decision-only judge's verdict above a locally fitted confidence threshold; independently judge the remaining items with a stronger reasoning model."
read_depth: full
tags: [evaluation, decision-models, jev, selective-prediction, calibration, cascades, judge-bias]
---

**Take:** A cheap judge can preserve a stronger judge's accuracy by escalating uncertain decisions, but local labels, error complementarity and workload-specific thresholds determine the savings. Typed probabilities alone establish none of these.

## Mechanism and protocol

- **JEV 1.13.0 is a proprietary hosted decision service**, not a new architecture proposed here. It takes state, instructions and label criteria; returns probabilities without a generated rationale. Size, training data and recipe are unknown. Most requests use `Choice`; the paper's confidence is **maximum label probability**, not the service's separate undocumented native-confidence field.
- For a pair, judge both candidate orders. Map probabilities to candidate identity before averaging: `p(A) = (p_first(A,B) + 1 - p_first(B,A))/2`. Accept the most probable candidate when `max(p(A),1-p(A)) >= tau`; otherwise call GPT-6 Astra independently, without showing JEV's answer. The fallback replaces the verdict rather than voting with it. Invalid first-stage outputs escalate; invalid fallback outputs count as errors.
- Generative judges receive the same verdict-and-probability contract, **without explanations**, mostly with low reasoning effort. This is not a comparison against unrestricted chain-of-thought evaluators. Hidden labels, generator identities and split metadata are excluded; payload perturbation tests check that exclusion.
- **Base evaluation:** 5,172 judgments: RewardBench 1,500 pairs, JudgeBench GPT-4o split 350 pairs, HaluEval 3,000 evidence-grounded answers, 150 final-answer replies and 172 positive/synthetic controls. The 4,850 public judgments define the pooled ranking. Compare 15 LLM judges including JEV and two reward models; the open-decision appendix adds another 21 models.
- A 642-item pilot precedes 4,530 held-out base judgments. The **96 preference selection pairs** (64 RewardBench, 32 JudgeBench) fit the original cascade thresholds; 1,610 preference pairs test them without refitting. Source-question clustering keeps repeated answers together. Multi-family comparisons and most follow-ups are exploratory; frozen policies, the primary adjudication outcome and the prospective live protocol were specified before their evaluation data.

## Accuracy, cost and the boundary of competence

- On supplied labels, **JEV / GPT-6 accuracy** is RewardBench **92.5 / 92.5%**, JudgeBench **78.6 / 93.1%**, HaluEval **87.3 / 88.4%**, final-answer agreement **94.0 / 96.7%**. JEV ranks eighth of fifteen LLM judges on the public pool; GPT-5.6 Sol is more accurate than GPT-6 overall at about half the fee. GPT-6 is a reference comparator, not a universal optimum.
- On a separate matched **120-judgment timing panel**, JEV costs **$0.044 per 1,000**, GPT-6 **$12.182** (~277×). Median latency **0.15 / 1.89 s**, p95 **0.24 / 3.86 s**. Fees estimate token usage at collection-time prices, including cache/reasoning accounting and conservative reservations for missing usage; they are not invoices. Latency includes network/provider/retries from one client setup, not intrinsic inference or throughput.
- The authors' useful distinction is **read a verdict from supplied text versus derive/check a result**. Skill-pooled gaps are ~7 points on expert knowledge, ~13 on code, ~14 on math and ~28 on logic. JEV nearly saturates items all other judges solve; the gap is concentrated at middle difficulty. Length-matched JudgeBench pairs still leave a ~19-point gap, so generic verbosity preference does not explain it.
- **Style can defeat confidence.** On RM-Bench, JEV falls from **85.4%** on matched-style pairs to **76.6%** when the wrong answer is more elaborate; GPT-6 falls **91.8 → 90.1%**. Two-order JEV error-detection AUROC drops **0.839 → 0.764**. At confidence ≥0.9 its hard-pair error rate is **7.9%**, versus **3.0%** on matched styles. Strict thresholds recover accuracy by escalating many more cases.
- **Reference-free prose is a separate failure:** on 200 balanced HaluEval general responses, JEV / GPT-4.1 mini / GPT-5.4 agree with labels **53.5 / 54.0 / 56.0%**, despite mean confidence **0.91 / 0.94 / 0.96**. JEV error AUROC **0.498** means thresholding cannot locate mistakes here. These are not GPT-6 results. Grounded summaries score ~69–70%; samples differ in content and label provenance, so this does not isolate a causal benefit of providing evidence.

## Frozen, retrospective and live cascades are different evidence

- **Frozen offline policy, tau=0.9:** on 1,610 held-out pairs, cascade **93.4%** versus GPT-6 **92.5%**, difference **+0.93 pp [0.24,1.66]**, escalating **31.5%** at **41.4% of GPT-6's fee** (44.0% conservative). Both JEV calls are included.
- Split that headline: RewardBench **93.7 vs 92.4%**, 24.8% escalation, 26.7% fee; JudgeBench **92.2 vs 93.0%**, 64.8% escalation, 66.8% fee. **83% of the held-out pool is RewardBench.** Earlier versions' 510-pair result (99.4% accuracy retained at 56.8% fee) is unchanged; the larger headline improves mainly because added easy pairs change the mixture (Appendix B).
- **Live replication on 510 already-analyzed pairs** confirms execution, not new-workload generalization: **92.5 vs 93.1%**, 46.5% escalation, 57.2% fee. Median **0.27 vs 2.10 s**, but p95 **4.26 vs 4.49 s**. Escalated pairs wait for both stages; JudgeBench's median saving is small and its cascade p95 is worse in Table 37.
- **Prospective live test:** 500 PPE correctness pairs plus 270 JudgeBench Claude-split pairs. Fit a separate threshold on **100 labels per workload**, then run on **400 + 170 held-out pairs**. The conservative rule selects **tau=0.95 / 0.99**. Cascade and GPT-6 match exactly at **88.2 / 94.7%** within the respective workloads; pooled **90.2%**, versus JEV **76.1%** alone. Escalate **74.2%**, pay **75.5%** of GPT-6's fee; pooled median **1.87 vs 1.91 s**, p95 **4.95 vs 5.58 s**. Accuracy equality on these samples is not a guarantee of identical future errors.
- Prospective JudgeBench keeps 91 questions seen in the earlier GPT-4o split, with different candidate answers. Reported held-out parity holds on both **57 seen-question** and **113 unseen-question** pairs. PPE excludes overlap before sampling. “Two new workloads” does not mean every question in both was unseen.
- **Post hoc sweeps** suggest additional savings, including a GPT-5.6 fallback, but choose/read thresholds on the evaluated outcomes. The frozen GPT-5.6 policy actually loses **4.81 points on held-out JudgeBench** despite its acceptable pooled result. Do not cite the attractive sweep as prospective validation.

## Selecting a threshold and checking probabilities

- Original **point rule:** maximize coverage on local labels subject to mean cascade-minus-fallback accuracy ≥−2 pp. Improved **lower-bound rule:** require `mean(d) - 1.645 * sd(d)/sqrt(n) >= -0.02`, with `d` in {−1,0,1}; use the most permissive qualifying threshold, stricter on ties, or escalate everything if none qualifies.
- In 2,000 resampling draws from the existing preference pool, with 96 total selection labels, the point rule's held-out loss exceeds two points in **44.0%** of draws; lower-bound rule **5.2%**; lower-bound **per-workload** thresholds **0.6%**. These are empirical simulations over one reused pool, not formal distribution-shift or multiple-threshold-selection guarantees. “About 100 labels” is a starting recipe, not a universal sufficient sample.
- **Calibration, error ranking and classification accuracy differ.** Human-label substitutions reverse the apparent HaluEval probability-quality ordering. Temperature scaling fitted on pilot labels improves HaluEval held-out NLL **0.496→0.304**, but worsens RewardBench **0.192→0.216** and JudgeBench **0.449→0.475**. Fit and validate locally; no universal temperature.
- Repetition is stable (0/96 JEV verdict changes), but rubric paraphrases change **4/48**. Only **3/95** reversal flips have confidence ≥0.9. Equivalent `Choice`, `Noul`, `Score` questions nevertheless give different probabilities: Choice–Noul mean difference **0.055**, one close verdict flips. Freeze **prompt, output type, model version, order treatment and workload** when validating a gate.
- Order averaging is a robustness choice, not a proven general accuracy boost: JEV's pairwise gain **+0.76 pp [0.00,1.57]**; four-way averaging **72→70%**, ECE **0.046→0.106**, although error AUROC improves. Four-way and binary confidence thresholds are not interchangeable.

## Human audit, open models and limits

- “Blinded human adjudication” means **183 selectively audited items from a 990-item subset**, not human relabeling of the full benchmark. One team member labels all items; a planned second human pass is replaced by **Claude Fable 5.1**, which flags 39 disagreements for an author to adjudicate. All final decisions are human, but raters are not independent external annotators; 36 outcomes remain indecisive.
- On 69 JudgeBench disagreements, the audit sides with GPT-6 **57** times, JEV **1**, undecided **11**: difficult-correctness gaps survive label scrutiny. On HaluEval, **24/26** both-wrong items instead favor the judges. Human-corrected sensitivity on 240 answers changes JEV/GPT-6 Brier **0.176/0.245 → 0.062/0.032**. Keep the audit's selective scope and supplied-label primary results separate.
- **Appendix A matters:** Perplexity Decider v1.1 27B and Eikos-27B reach **89.0%** pooled public accuracy versus JEV **88.3%**, within sampling error; several other open models are comparable. Decision Index rank barely predicts this evaluation (rank correlation **0.12**). Local H100 versus hosted timing compares deployments, not architectures. **Their cascades, prospective transfer and calibration under escalation were not tested.**
- Laya provides a useful negative control: valid, fast typed outputs, but chance-level pairwise judgments and uninformative confidence even on context-complete examples. ModernBERT weights are not JEV weights; neither Laya's failure nor JEV's success establishes that the interface causes quality.
- Final-answer labels lack complete annotator provenance; all-positive GSM8K trajectories are only positive controls. Unknown training overlap, unequal compute, restricted professional-domain coverage and correlated judge errors remain. Finished-output judging **does not test tool selection or online agent control**. No model is trained here; supplementary offline scripts are described but not run in this ingest.

## Why it matters for us

- Use a cheap tier for evidence-visible checks only after measuring it against local labels. Log accept/escalate decisions, judge version, order handling and fallback results. Keep uncertainty deferral separate from deterministic approval rules for consequential actions.
- Compare with [Husain/Saha's production-trace guide](decision-model-evals-thresholds-calibration.md): their score is **failure probability**, while this paper gates **confidence in whichever verdict wins**. High failure risk and high decision confidence are different signals.
- Qualifies the [two-gap assurance framework](../agentic-engineering/reality-is-the-final-verifier-two-gap-framework.md): a cascade can preserve a fallback's measured accuracy cheaply; shared errors still require outside evidence or human authority. Its benchmark cannot authorize autonomous high-impact actions.

Source: [arXiv v5 PDF](https://arxiv.org/pdf/2609.26550v5), full 53-page text including references and Appendices A–Q, read 2026-10-21. [Archived PDF](../../pdfs/2609.26550v5-jev-as-a-judge.pdf) · [extracted text](../../pdfs/2609.26550v5-jev-as-a-judge.txt). Discovered via [Elvis Saravia](https://x.com/omarsar0/status/2112632133357346889); no experiments or supplementary code rerun.
