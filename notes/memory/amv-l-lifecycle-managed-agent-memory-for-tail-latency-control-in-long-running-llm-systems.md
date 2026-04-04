---
title: "AMV-L: Lifecycle-Managed Agent Memory for Tail-Latency Control in Long-Running LLM Systems"
authors:
  - Emmanuel Bamidele
arxiv_id: "2603.04443"
arxiv_url: "https://arxiv.org/abs/2603.04443"
published: "2026-02-22"
updated: "2026-02-22"
source: "arXiv"
project: "memory"
scope_note: "core include"
agent_setting: "long-running LLM systems where memory growth threatens latency and throughput stability"
memory_mechanism: "Assigns utility scores to memory items and manages promotion, demotion, and eviction so retrieval stays bounded and tail latency remains controlled."
icl_relevance: "medium"
tags:
  - agent-memory
  - systems-memory
  - latency
  - lifecycle-management
categories:
  - cs.DC
  - cs.AI
  - cs.LG
  - eess.SY
---

- **One-line take:** A memory-systems paper focused on working-set control and tail-latency stability rather than just answer quality.
- **What it stores:** Tiered memory items with continuously updated utility scores and bounded retrieval-set membership.
- **How memory is used at inference time:** Assigns utility scores to memory items and manages promotion, demotion, and eviction so retrieval stays bounded and tail latency remains controlled.
- **Why it matters for this sub-project:** Strong pass-three addition because it reframes persistent memory as an operating resource with lifecycle policies, not just a knowledge store.
- **Caveats / limits:** It emphasizes serving behavior and retrieval bounds more than semantic quality of remembered content.
- **Abstract-level summary:** Long-running LLM agents require persistent memory to preserve state across interactions, yet most deployed systems manage memory with age-based retention (e.g., TTL). While TTL bounds item lifetime, it does not bound the computational footprint of memory on the request path: as retained items accumulate, retrieval candidate sets and vector similarity scans can grow unpredictably, yielding heavy-tailed latency and unstable throughput. We present AMV-L (Adaptive Memory Value Lifecycle), a memory-management framework that treats agent memory as a managed systems resource. AMV-L assigns each memory item a continuously updated utility score and uses value-driven promotion, demotion, and eviction to maintain lifecycle tiers; retrieval is restricted to a bounded, tier-aware candidate set that decouples the request-path working set from total retained memory. We implement AMV-L in a full-stack LLM serving system and evaluate it under identical long-running workloads against two baselines: TTL and an LRU working-set policy, with fixed prompt-injection caps. Relative to TTL, AMV-L improves throughput by 3.1x and reduces latency by 4.2x (median), 4.7x (p95), and 4.4x (p99), while reducing the fraction of requests exceeding 2s from 13.8% to 0.007%. Compared to LRU, AMV-L trades a small regression in median/p95 latency (+26% / +3%) for improved extreme-tail behavior (-15% p99; -98% >2s) and lower token overhead (approximately 6% fewer tokens/request), while matching retrieval quality (value means within approximately 0-2%). The gains arise primarily from bounding retrieval-set size and vector-search work, not from shortening prompts. Our results show that predictable performance for long-running LLM agents requires explicit control of memory working-set size and value-driven lifecycle management, rather than retention time alone.
