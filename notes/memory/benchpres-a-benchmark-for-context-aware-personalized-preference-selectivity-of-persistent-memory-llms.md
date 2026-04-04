---
title: "BenchPreS: A Benchmark for Context-Aware Personalized Preference Selectivity of Persistent-Memory LLMs"
authors:
  - Sangyeon Yoon
  - Sunkyoung Kim
  - Hyesoo Hong
  - Wonje Jeung
  - Yongil Kim
  - Wooseok Seo
  - Heuiyeen Yeen
  - Albert No
arxiv_id: "2603.16557"
arxiv_url: "https://arxiv.org/abs/2603.16557"
published: "2026-03-17"
updated: "2026-03-17"
source: "arXiv"
project: "memory"
scope_note: "pass-three meta include: benchmark/evaluation"
agent_setting: "persistent-memory assistants that personalize communication under social or institutional constraints"
memory_mechanism: "Benchmark paper testing whether persistent user preferences are applied or suppressed appropriately across contexts."
icl_relevance: "medium"
tags:
  - agent-memory
  - benchmark
  - personalization
  - preference-memory
categories:
  - cs.AI
  - cs.CL
---

- **One-line take:** Shows that remembering a preference is easier than knowing when not to use it.
- **What it stores:** The benchmark assumes agents store persistent user preferences that may or may not be contextually appropriate to apply.
- **How memory is used at inference time:** Benchmark paper testing whether persistent user preferences are applied or suppressed appropriately across contexts.
- **Why it matters for this sub-project:** Useful because it probes a real deployment question for personalized memory agents: selective application, not just correct recall.
- **Caveats / limits:** As a benchmark it diagnoses contextual misuse rather than proposing a concrete fix.
- **Abstract-level summary:** Large language models (LLMs) increasingly store user preferences in persistent memory to support personalization across interactions. However, in third-party communication settings governed by social and institutional norms, some user preferences may be inappropriate to apply. We introduce BenchPreS, which evaluates whether memory-based user preferences are appropriately applied or suppressed across communication contexts. Using two complementary metrics, Misapplication Rate (MR) and Appropriate Application Rate (AAR), we find even frontier LLMs struggle to apply preferences in a context-sensitive manner. Models with stronger preference adherence exhibit higher rates of over-application, and neither reasoning capability nor prompt-based defenses fully resolve this issue. These results suggest current LLMs treat personalized preferences as globally enforceable rules rather than as context-dependent normative signals.
