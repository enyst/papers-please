---
title: "Rethinking How to Remember: Beyond Atomic Facts in Lifelong LLM Agent Memory"
authors:
  - Jingwei Sun
  - Jianing Zhu
  - Jiangchao Yao
  - Tongliang Liu
  - Bo Han
arxiv_id: "2605.19952"
arxiv_url: "https://arxiv.org/abs/2605.19952"
published: "2026-05-19"
updated: "2026-05-19"
source: "arXiv"
project: "memory"
scope_note: "pass-four include (Q2 2026 sweep)"
agent_setting: "lifelong LLM agents that accumulate memory across sessions"
memory_mechanism: "Argues against storing atomic facts in favor of richer, structured memory units that preserve context, relationships, and temporal anchoring."
icl_relevance: "medium"
tags:
  - agent-memory
  - memory-extraction
  - lifelong-memory
  - structured-memory
categories:
  - cs.CL
---

- **One-line take:** Atomic facts are the wrong unit of memory — richer representations that preserve context outperform.
- **What it stores:** See memory_mechanism above.
- **How memory is used at inference time:** Argues against storing atomic facts in favor of richer, structured memory units that preserve context, relationships, and temporal anchoring.
- **Why it matters for this sub-project:** Directly challenges the dominant extract-facts-and-retrieve pattern with evidence for richer memory units.
- **Caveats / limits:** Newly published (Q2 2026); peer validation pending.
- **Abstract-level summary:** To enable reliable long-term interaction, LLM agents require a memory system that can faithfully store, efficiently retrieve, and deeply reason over accumulated dialogue history. Most existing methods adopt an extracted fact based paradigm: handcrafted static prompts compress raw dialogues into atomic facts, which are then stored, matched, and injected into downstream reasoning. Nevertheless, such fact-centric designs inevitably discard fine-grained details in original dialogues and fail to support deep reasoning over scattered isolated facts. Moreover, static prompts cannot maintain consistent extraction granularity across diverse dialogue styles. To address these limitations, we propose TriMem, which maintains three coexisting representation granularities, including raw dialogue segments anchored by source identifiers for storage fidelity, extracted atomic facts for efficient memory retrieval, synthesized profiles that aggregate dispersed facts into holistic semantic understanding for deep reasoning. We further adopt TextGrad-based prompt optimization, which iteratively refines extraction and profiling prompts via response quality feedback, achieving lifelong evolution without any parameter updating. Extensive experiments on LoCoMo and PerLTQA across multiple LLM backbones demonstrate that TriMem consistently outperforms strong memory baselines. The code is available at https://TMLR-TriMem.github.io .
