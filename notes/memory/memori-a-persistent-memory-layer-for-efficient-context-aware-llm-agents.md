---
title: "Memori: A Persistent Memory Layer for Efficient, Context-Aware LLM Agents"
authors:
  - Luiz C. Borro
  - Luiz A. B. Macarini
  - Gordon Tindall
  - Michael Montero
  - Adam B. Struck
arxiv_id: "2603.19935"
arxiv_url: "https://arxiv.org/abs/2603.19935"
published: "2026-03-20"
updated: "2026-03-20"
source: "arXiv"
project: "memory"
scope_note: "core include"
agent_setting: "LLM-agnostic agents and assistants that need multi-session context-awareness"
memory_mechanism: "Transforms dialogue into semantic triples and summaries so retrieval works over compact structured memory instead of raw history replay."
icl_relevance: "high"
tags:
  - agent-memory
  - persistent-memory
  - structured-triples
  - api-layer
categories:
  - cs.LG
---

- **One-line take:** Frames persistent memory as a data-structuring layer that can sit above whichever LLM API you use.
- **What it stores:** Semantic triples and conversation summaries distilled from raw dialogue.
- **How memory is used at inference time:** Transforms dialogue into semantic triples and summaries so retrieval works over compact structured memory instead of raw history replay.
- **Why it matters for this sub-project:** Useful for practical deployments because it explicitly targets vendor-agnostic, low-token persistent memory rather than model-specific tricks.
- **Caveats / limits:** Its abstraction may omit details that matter in tasks requiring verbatim or nuance-heavy recollection.
- **Abstract-level summary:** As large language models (LLMs) evolve into autonomous agents, persistent memory at the API layer is essential for enabling context-aware behavior across LLMs and multi-session interactions. Existing approaches force vendor lock-in and rely on injecting large volumes of raw conversation into prompts, leading to high token costs and degraded performance. We introduce Memori, an LLM-agnostic persistent memory layer that treats memory as a data structuring problem. Its Advanced Augmentation pipeline converts unstructured dialogue into compact semantic triples and conversation summaries, enabling precise retrieval and coherent reasoning. Evaluated on the LoCoMo benchmark, Memori achieves 81.95% accuracy, outperforming existing memory systems while using only 1,294 tokens per query (~5% of full context). This results in substantial cost reductions, including 67% fewer tokens than competing approaches and over 20x savings compared to full-context methods. These results show that effective memory in LLM agents depends on structured representations instead of larger context windows, enabling scalable and cost-efficient deployment.
