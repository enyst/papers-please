---
title: "M2A: Multimodal Memory Agent with Dual-Layer Hybrid Memory for Long-Term Personalized Interactions"
authors:
  - Junyu Feng
  - Binxiao Xu
  - Jiayi Chen
  - Mengyu Dai
  - Cenyang Wu
  - Haodong Li
  - Bohan Zeng
  - Yunliu Xie
  - Hao Liang
  - Ming Lu
  - Wentao Zhang
arxiv_id: "2602.07624"
arxiv_url: "https://arxiv.org/abs/2602.07624"
published: "2026-02-07"
updated: "2026-02-07"
source: "arXiv"
project: "memory"
scope_note: "core include"
agent_setting: "long-term personalized multimodal interactions"
memory_mechanism: "Pairs a raw message store with a semantic memory store and lets a chat agent decide when to query or update memory through a memory manager."
icl_relevance: "high"
tags:
  - agent-memory
  - multimodal-memory
  - personalization
  - dual-layer-memory
categories:
  - cs.AI
---

- **One-line take:** A clean multimodal extension of the persistent-memory pattern: keep both raw evidence and abstracted semantic memory.
- **What it stores:** Immutable multimodal interaction logs plus higher-level semantic observations about the user.
- **How memory is used at inference time:** Pairs a raw message store with a semantic memory store and lets a chat agent decide when to query or update memory through a memory manager.
- **Why it matters for this sub-project:** Useful when the memory problem is not purely text-based and personalization needs to evolve over long spans of use.
- **Caveats / limits:** The framing is heavily personalization-oriented, so transfer to generic task agents is not automatic.
- **Abstract-level summary:** This work addresses the challenge of personalized question answering in long-term human-machine interactions: when conversational history spans weeks or months and exceeds the context window, existing personalization mechanisms struggle to continuously absorb and leverage users' incremental concepts, aliases, and preferences. Current personalized multimodal models are predominantly static-concepts are fixed at initialization and cannot evolve during interactions. We propose M2A, an agentic dual-layer hybrid memory system that maintains personalized multimodal information through online updates. The system employs two collaborative agents: ChatAgent manages user interactions and autonomously decides when to query or update memory, while MemoryManager breaks down memory requests from ChatAgent into detailed operations on the dual-layer memory bank, which couples a RawMessageStore (immutable conversation log) with a SemanticMemoryStore (high-level observations), providing memories at different granularities. In addition, we develop a reusable data synthesis pipeline that injects concept-grounded sessions from Yo'LLaVA and MC-LLaVA into LoCoMo long conversations while preserving temporal coherence. Experiments show that M2A significantly outperforms baselines, demonstrating that transforming personalization from one-shot configuration to a co-evolving memory mechanism provides a viable path for high-quality individualized responses in long-term multimodal interactions. The code is available at https://github.com/Little-Fridge/M2A.
