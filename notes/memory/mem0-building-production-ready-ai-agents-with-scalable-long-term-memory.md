---
title: "Mem0: Building Production-Ready AI Agents with Scalable Long-Term Memory"
authors:
  - Prateek Chhikara
  - Dev Khant
  - Saket Aryan
  - Taranjeet Singh
  - Deshraj Yadav
arxiv_id: "2504.19413"
arxiv_url: "https://arxiv.org/abs/2504.19413"
published: "2025-04-28"
updated: "2025-04-28"
source: "arXiv"
project: "memory"
scope_note: "core include"
agent_setting: "multi-session conversational agents"
memory_mechanism: "Extracts salient facts from ongoing conversations, consolidates them into persistent memory, and retrieves them instead of replaying full history."
icl_relevance: "high"
tags:
  - agent-memory
  - long-term-memory
  - production
  - conversation-memory
categories:
  - cs.CL
  - cs.AI
---

- **One-line take:** A production-leaning memory architecture built around selective extraction and retrieval of salient conversational facts.
- **What it stores:** Distilled user facts, preferences, and relational memory, optionally in a graph representation.
- **How memory is used at inference time:** Extracts salient facts from ongoing conversations, consolidates them into persistent memory, and retrieves them instead of replaying full history.
- **Why it matters for this sub-project:** Strong practical reference point because it explicitly optimizes the accuracy/latency/token-cost tradeoff for persistent agents.
- **Caveats / limits:** Most evidence is from long-conversation benchmarks, so broader agent settings still need separate validation.
- **Abstract-level summary:** Large Language Models (LLMs) have demonstrated remarkable prowess in generating contextually coherent responses, yet their fixed context windows pose fundamental challenges for maintaining consistency over prolonged multi-session dialogues. We introduce Mem0, a scalable memory-centric architecture that addresses this issue by dynamically extracting, consolidating, and retrieving salient information from ongoing conversations. Building on this foundation, we further propose an enhanced variant that leverages graph-based memory representations to capture complex relational structures among conversational elements. Through comprehensive evaluations on LOCOMO benchmark, we systematically compare our approaches against six baseline categories: (i) established memory-augmented systems, (ii) retrieval-augmented generation (RAG) with varying chunk sizes and k-values, (iii) a full-context approach that processes the entire conversation history, (iv) an open-source memory solution, (v) a proprietary model system, and (vi) a dedicated memory management platform. Empirical results show that our methods consistently outperform all existing memory systems across four question categories: single-hop, temporal, multi-hop, and open-domain. Notably, Mem0 achieves 26% relative improvements in the LLM-as-a-Judge metric over OpenAI, while Mem0 with graph memory achieves around 2% higher overall score than the base configuration. Beyond accuracy gains, we also markedly reduce computational overhead compared to full-context method. In particular, Mem0 attains a 91% lower p95 latency and saves more than 90% token cost, offering a compelling balance between advanced reasoning capabilities and practical deployment constraints. Our findings highlight critical role of structured, persistent memory mechanisms for long-term conversational coherence, paving the way for more reliable and efficient LLM-driven AI agents.
