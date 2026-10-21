---
title: How To Use Decision Models for Evals
authors: [Hamel Husain, Antaripa Saha]
published: 2026-10-20
source: blog
url: https://hamel.dev/blog/posts/decision-model-evals/
mechanism: "Fit classification thresholds to labeled traces and explicit precision/recall requirements; separately validate whether score calibration improves probability estimates."
read_depth: full
tags: [evaluation, decision-models, calibration, cross-validation, precision-recall, jev]
---

**Take:** Tune the decision threshold before comparing judges. Separately test whether their scores deserve a probability interpretation. The worked example does not prove its cheaper candidate models meet the advertised precision/recall minimums on new traces.

## What was tested

- Six configurations: Jev 1.13, Perplexity Decider 1.1 27B, Liquid d1/d1-ultra, Cloudflare Clef Flash, OpenAI Decisions using GPT-6 Luna. OpenAI's typed Decisions API is separate from Structured Outputs; this comparison groups interfaces serving the same classification task, not six identical architectures.
- Each scores whether an apartment-leasing agent's complete production trace contains **at least one substantive failure**: contradictions, unsupported claims, missing/misused tools, false completion, unresolved requests, harmful leaked internals. No outside policies may be assumed. Other models get the same prompt and serialized inputs; Jev gets equivalent criteria through its structured API.
- Body says 100 traces; footnotes specify **98 scored after excluding two internal QA examples**, with **61 failures and 37 traces without a labeled failure**. Reference failures comprise **39 from original human review + 22 automated-eval discoveries manually validated**. Inputs mask labels/reviewer notes. This is a small private dataset with an expanded reference, not a fresh large blind human test set; score/label JSON is public but conversations are not.

## Thresholds, metrics and actual validation

- Failure probability `s >= t` flags a trace. A score of 0.4 can separate failures perfectly from passes at 0.1 while the default 0.5 catches none. Ranking, chosen operating point and calibration must be evaluated separately.
- **Precision** asks how many flags are true failures; **recall** asks how many known failures were caught. F1 weights the two equally for illustration. Choose costs, minimums or F-beta for the actual use case; F1 is not automatically the product objective.
- The full-sample precision–recall curves identify Perplexity, d1-ultra and OpenAI as candidates reaching **80% precision AND 80% recall somewhere**. Threshold fitting then chooses the highest training F1 satisfying both minimums when possible. **If infeasible, the worked analysis falls back to unconstrained F1 and retains those validation predictions.** Non-candidates always use unconstrained F1.
- Footnote reports **36/100 training splits infeasible for Perplexity, 29/100 for d1-ultra, 0/100 for OpenAI**; archived audit agrees. Its 100 rows/model are **20 repeats × five folds**, not 100 repeated five-fold experiments. Shared splits choose thresholds on training examples and measure performance on the remaining traces.
- **Resulting held-out averages** from published chart JSON:

  | Candidate | Precision | Recall | F1 | API cost / 100 runs |
  |---|---:|---:|---:|---:|
  | Perplexity | 0.754 | 0.825 | 0.787 | $0.008204 (0.82 cents) |
  | Liquid d1-ultra | 0.759 | 0.817 | 0.787 | $0.015208 (1.52 cents) |
  | OpenAI Decisions | 0.869 | 0.862 | 0.865 | $0.037232 (3.72 cents) |

- **Two candidates miss 80% validation precision.** “Meets requirements” describes a full-sample curve/training selection possibility, not validated deployment eligibility. Candidate selection uses the full sample before CV, so end-to-end model selection is not fully nested. Repeated folds reuse 98 traces; they do not create independent new evidence or future guarantees.
- **The example coding-agent prompt is stricter than the implemented comparison:** it says report infeasibility instead of relaxing either requirement. Preserve that difference when copying the recipe; specify whether no feasible threshold disables the judge, escalates everything, or explicitly enters an experimental fallback.
- Published audit's `feasible` field is inconsistent with selected-threshold precision for some **non-candidate** rows (e.g. Jev). It may describe existence of a feasible threshold rather than the chosen unconstrained one; do not interpret that field as proof the selected non-candidate threshold passes. Candidate rows' feasibility/fallback flags match the reported counts.
- Density displays use **unconstrained** F1 fitting before minimums are introduced. Dashed optimized threshold is the **mean selected threshold**; displayed held-out metrics come from individual split thresholds, not applying the mean to all traces. Gaussian smoothing (bandwidth 0.07, reflected at boundaries, each class area one) affects visualization only.

## Calibration and cost

- Reliability plots compare groups of similar predicted failure probability against observed failures; five groups of **19–20** examples each. Clef's lowest-score group predicts ~8% failure risk but contains **60%** failures. This is local empirical calibration, not an intrinsic property of the API or output format.
- Fit **Platt scaling on clipped log-odds**, training-only within the same folds; each trace's adjusted score is its mean out-of-fold probability across repeats. Re-sort into probability groups for plotting. This small-sample display does not establish an exact risk for a future trace.
- Brier scores, raw → adjusted: **Jev 0.187→0.188**, **d1-ultra 0.173→0.172**, **OpenAI 0.159→0.164**. OpenAI's log-odds adjustment worsens the score. An exploratory direct-probability fit gives **0.154** using the same folds; selecting that form post hoc needs new validation. Brier mixes discrimination and calibration, not calibration alone.
- Tune thresholds/calibration from **saved scores**, with no new model calls. Cost covers **100 runs**, while accuracy excludes the two QA traces. Liquid prices are repriced at 2026-10-17 rates. OpenAI is ~4.5× Perplexity's fee here. A candidate-only Pareto frontier is conditional on the chosen candidate set, not a universal market frontier.
- Latency is deliberately excluded from the main comparison. Footnote mean times come from **separate runs**, with different batching/location/provider conditions; do not turn them into throughput or tail-latency rankings.

## Practical scope and related reading

- The broad failure-finding task exposes differences, but authors recommend a **separate narrow judge per failure mode** in practice. Smaller performance gaps on narrower tasks are an expectation, not demonstrated here.
- Prompt optimization needs reliable labels and a final test set outside development. Their manual Jev prompt experiment raises default-threshold F1 **0.78→0.80**. It **did not use GEPA** and cannot establish GEPA's effect; GEPA is linked as an optional method.
- [JEV-as-a-Judge](jev-as-a-judge-confidence-escalation.md) independently tests confidence-gated escalation. It uses **max label probability**, whereas this guide's score means **probability of failure**. Do not transplant one threshold into the other.
- [Olson's linked explainer](https://www.randalolson.com/2026/10/14/when-to-use-a-decision-model-instead-of-an-llm/) separates classification/routing from knowledge/reasoning in a broader leaderboard snapshot. Different tasks, serving and models; agreement with this paper's reading-versus-deriving distinction is a useful hypothesis, not a matched replication.
- **For our evals:** lock the failure definition, collect local human labels, freeze model/prompt/interface, keep model selection and prompt development away from the final test, choose explicit infeasibility behavior, and track operating-point precision/recall plus risk calibration separately.

Source: [complete author blog](https://hamel.dev/blog/posts/decision-model-evals/), appendix prompts and all 13 footnotes, read 2026-10-21; [raw HTML](../../transcripts/evaluation/2026-10-21-hamel-decision-evals.html), [score/label JSON](../../transcripts/evaluation/2026-10-21-hamel-chart-data.json), [threshold audit](../../transcripts/evaluation/2026-10-21-hamel-threshold-audit.json), [calibration plot data](../../transcripts/evaluation/2026-10-21-hamel-calibration.json) archived. Parsed supplied data to check counts and reported metrics; did not rerun fitting code, call models, render interactive charts or audit private traces.
