---
title: "Can a Language Model Learn Facts Continually in Its Weights?"
authors:
  - Charles O'Neill
arxiv_id: "2607.11020"
arxiv_url: "https://arxiv.org/abs/2607.11020"
published: "2026-07-13"
updated: "2026-07-14"
source: "arXiv"
project: "memory"
scope_note: "post-cutoff targeted addition — weight memory / continual-learning contrast"
agent_setting: "Post-training continual fact writing into Qwen3 weights; directly relevant as a contrast to external agent memory"
memory_mechanism: "Writes invented facts with sequential LoRA or full-parameter updates, then measures whether later writes preserve usable access; compares every write with the same fact supplied in context."
icl_relevance: "high"
tags:
  - agent-memory
  - weight-memory
  - continual-learning
  - catastrophic-forgetting
  - knowledge-editing
  - lora
  - context-vs-weights
  - retrieval
categories:
  - cs.CL
  - cs.LG
---

- **One-line take:** Broad training can write a usable fact into weights, but later writes capture the questions that reached it; context remains the reliable, addressable channel for composition and durable recall.
- **Method:** Write invented facts into Qwen3-4B (plus selected 8B/full-tuning replications), evaluate five kinds of held-out questions, and follow facts through 20–100 later writes against an original-model floor and a fact-in-prompt ceiling.
- **Strongest result:** After 20 writes, bare-statement facts retain 1% strict accuracy and broad-study facts 46%; forgotten facts still retain most of the log-probability lift created by their write.
- **Why it matters here:** It turns the practitioner-level “weights make eviction hard” warning into a controlled access-versus-storage result. Weight memory lacks a general address for retrieving, composing, updating, or deleting facts.
- **Code/data:** The paper links `https://github.com/basetenlabs/cortex` and `https://huggingface.co/datasets/baseten/cortex`; both were unavailable without access when checked on 2026-07-17.

## Core question

Continual learning needs to do three different things:

1. write knowledge that can be *used*, not merely recited;
2. preserve the model's unrelated capabilities;
3. keep earlier knowledge reachable after later updates.

The paper separates these requirements rather than treating “accuracy after fine-tuning” as one outcome. Its central claim is that the third remains unsolved: a fact can leave a durable trace in the weights while losing the routes by which questions retrieve it.

## Evaluation design

The primary experiments use Qwen3-4B with frozen base weights and rank-16 LoRA adapters unless stated otherwise. The dataset contains 247 one-sentence facts about invented entities, usually contradicting a familiar prior—for example, a metal that melts when cooled below −10°C.

Every fact receives held-out questions of five types:

- recall;
- paraphrase;
- one-step application;
- composition with unstated world knowledge;
- counterfactual choice against the model's default belief.

The original model forms the floor; the same model with the fact in its prompt forms the ceiling. A strict grader requires the requested conclusion, while a lenient grader also credits an answer that merely states a premise entailing it. Their difference is the **entailment gap**, a recitation-to-use measure.

The instrument is explicitly certified before use: floor below 20%, prompt ceiling above 80%, truncation checks, leakage audit, and pass/failure audits. The final dual-grading pipeline reports a 4% floor and 91% lenient in-prompt ceiling.

## What breadth changes

**Bare-statement training** presents a fact in two trivial framings. **Study training** uses 24 paraphrases, Q&A pairs, worked implications, and contrasts with the prior.

Bare statements quickly produce excellent recitation—97% recall and 95% paraphrase—but little use. Counterfactual accuracy remains 21–23% even with more optimization. Study data reaches 45–50%. Composition is roughly 40% for bare statements, 60% for study, and 83% when the fact is in context.

In the controlled factorization, diverse recall/paraphrase prompts reduce the entailment gap from **27.4 to 5.4 points** even though none supplies a derived conclusion. Prompt breadth, rather than an explicit reasoning step or simply more trainable parameters, is the supported causal factor.

Context distillation also produces usable writes. Across SFT and several distillation objectives, bare-statement training is the only family with a large gap. No weight-based method matches the fact-in-prompt ceiling on composition.

## What survives later writes

After 20 sequential writes at the main operating point:

| Write method | Earlier-fact strict accuracy |
|---|---:|
| Bare statement | 1% |
| Broad study data | 46% |
| Offline context distillation | 14% |
| Online context distillation | 27–32% |

A second prior-conflict evaluation finds the same split at matched budgets: study facts retain 31–49%, bare-statement facts 1–7%, with bare facts already near zero after five writes.

At 100 writes, study retention reaches a **25–28% plateau** rather than zero. Re-distilling all accumulated facts into a fresh copy of the original model every 20 writes preserves general capability but does not restore retention: 25% with consolidation versus 28% without it at the endpoint.

The single-write entailment gap predicts later survival across methods (Spearman ρ = −0.526), but the crossed experiments reveal a more important causal result: **the incoming write determines interference**. Changing later writes from bare statements to study data improves retention by 37.6 points; changing how the earlier fact was stored has no detectable effect (−2.4 points, interval spanning zero).

## Forgetting is lost access, not erasure

The paper reconstructs each checkpoint and tracks the written statement's likelihood. Facts that fail every strict question after 20 writes still retain a median:

- 69% (bare) and 79% (study) of their original log-probability lift;
- 57% and 67% after a drift correction.

They are behaviorally gone but measurably present. Under bare-statement writing, **70% of wrong answers about a forgotten fact contain the newest fact's content**. The old question now routes to the latest write. Study failures show this only 1% of the time.

The paper calls this **question-keyed** storage. The model can answer some questions that already reach the fact, but has no general handle for asking “what facts have I learned?” or retrieving one for a new computation.

That limitation exists before overwriting. When a question requires two learned facts, accuracy is 32% with both facts in weights versus 91% with both in the prompt. Self-retrieval produces correct fact content only 34% of the time and closes little of the gap. Supplying the true statements in context recovers performance to 63%.

After continued study writes, placing forgotten facts back in context restores their question accuracy to **77–80%**. The stale weighted copy does not block the contextual copy; what failed was the route from question to stored trace.

## Capability preservation is a separate problem

Across 12 conditions, unrelated capability loss orders strongly with KL divergence from the original model (ρ = 0.83); the larger factorial gives ρ = 0.946. But retention and capability can move in opposite directions, so KL is a cost coordinate rather than a complete mechanism.

The distillation teacher matters sharply:

- sequential distillation from a frozen original teacher: +2 points capability, KL 0.48, 54% retention;
- distillation through the model's accumulated merges: −31 points capability, KL 1.70, 21% retention.

A per-write KL penalty also rescues capability and improves retention, but does not systematically reduce measured endpoint KL. These interventions stop broad model collapse; none keeps every earlier fact reachable.

A linearized gradient calculation predicts the *next update's* immediate effect (ρ = 0.795) but not final forgetting after the sequence (ρ = −0.258). Activation-guided edits, bridging recipes, and conflict-gradient projection also miss their predeclared rescue thresholds.

## Implications for agent memory

This is unusually direct evidence for keeping an authoritative memory store outside the weights.

Weights can be a **cache or consolidation target** when a canonical copy exists elsewhere. Broad data and a frozen teacher make that cache more usable and less damaging. But the weights do not provide the operations an agent memory system needs:

- a stable address for retrieval;
- composition of multiple memories;
- provenance and auditability;
- contradiction replacement;
- selective deletion or eviction;
- reliable survival through later consolidation.

The result strengthens the local [`mylm`](./mylm-self-personalizing-lm-weight-memory.md) note while refining its explanation. The problem is not only that old content is “baked in.” It can remain stored yet become unreachable because later writes capture its queries. External/context memory supplies both content and an address.

For dreamem/SmolPaws-style memory, the practical conclusion is strong: keep durable facts in editable external memory; use retrieval to place the needed facts in context; treat any weight consolidation as a derived optimization, never the system of record.

## Caveats

- Most experiments use one model family, Qwen3-4B; only the entailment-gap result is replicated at 8B.
- Facts are invented, discrete, and stylistically uniform. Fine-tuned skills may behave differently.
- Most updates use LoRA; full fine-tuning appears only in selected factorial/extension cells.
- Several causal experiments use 5–32 stored facts and repeated measures, not large independent samples.
- The storage probe measures the statement's log-probability, not a complete mechanistic representation of the fact.
- Only three study facts were fully forgotten in the main relearning probe.
- The 100-write factorial extension is descriptive and partly post hoc.
- Model-generated facts, questions, and judging remain possible sources of shared bias despite the paper's unusually careful certification and audits.
