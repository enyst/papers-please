---
title: "Hippocampus: An Efficient and Scalable Memory Module for Agentic AI"
authors:
  - Yi Li
  - Lianjie Cao
  - Faraz Ahmed
  - Puneet Sharma
  - Bingzhe Li
arxiv_id: "2602.13594"
arxiv_url: "https://arxiv.org/abs/2602.13594"
published: "2026-02-14"
updated: "2026-02-14"
source: "arXiv"
project: "memory"
scope_note: "core include"
agent_setting: "long-horizon agentic deployments where retrieval latency and storage cost matter"
memory_mechanism: "Uses compact binary signatures and lossless token-ID streams inside a dynamic wavelet matrix to support fast compressed-domain retrieval."
icl_relevance: "medium"
tags:
  - agent-memory
  - efficient-memory
  - scalable-memory
  - retrieval-systems
categories:
  - cs.AI
---

- **One-line take:** Brings systems-level efficiency thinking to agent memory instead of assuming vector stores are good enough.
- **What it stores:** Compressed semantic signatures plus exact token streams that reconstruct stored memories on demand.
- **How memory is used at inference time:** Uses compact binary signatures and lossless token-ID streams inside a dynamic wavelet matrix to support fast compressed-domain retrieval.
- **Why it matters for this sub-project:** Useful for pass two because it broadens the corpus from memory quality to the practical cost and scaling profile of deployed memory infrastructure.
- **Caveats / limits:** Its main novelty is retrieval/storage efficiency; it says less about higher-level memory organization or reflective reasoning than some other papers.
- **Abstract-level summary:** Agentic AI require persistent memory to store user-specific histories beyond the limited context window of LLMs. Existing memory systems use dense vector databases or knowledge-graph traversal (or hybrid), incurring high retrieval latency and poor storage scalability. We introduce Hippocampus, an agentic memory management system that uses compact binary signatures for semantic search and lossless token-ID streams for exact content reconstruction. Its core is a Dynamic Wavelet Matrix (DWM) that compresses and co-indexes both streams to support ultra-fast search in the compressed domain, thus avoiding costly dense-vector or graph computations. This design scales linearly with memory size, making it suitable for long-horizon agentic deployments. Empirically, our evaluation shows that Hippocampus reduces end-to-end retrieval latency by up to 31$\times$ and cuts per-query token footprint by up to 14$\times$, while maintaining accuracy on both LoCoMo and LongMemEval benchmarks.
