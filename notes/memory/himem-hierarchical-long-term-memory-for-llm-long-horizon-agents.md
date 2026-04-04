---
title: "HiMem: Hierarchical Long-Term Memory for LLM Long-Horizon Agents"
authors:
  - Ningning Zhang
  - Xingxing Yang
  - Zhizhong Tan
  - Weiping Deng
  - Wenyong Wang
arxiv_id: "2601.06377"
arxiv_url: "https://arxiv.org/abs/2601.06377"
published: "2026-01-10"
updated: "2026-01-10"
source: "arXiv"
project: "memory"
scope_note: "core include"
agent_setting: "long-horizon conversational agents that must update memory over sustained interaction"
memory_mechanism: "Combines episode memory and note memory in a hierarchy, then updates them through conflict-aware reconsolidation."
icl_relevance: "high"
tags:
  - agent-memory
  - hierarchical-memory
  - conversation-memory
  - reconsolidation
categories:
  - cs.AI
---

- **One-line take:** A strong hierarchical design that explicitly bridges concrete episodes and more stable abstract notes.
- **What it stores:** Episode-level interaction events plus higher-level note memory that captures persistent user knowledge.
- **How memory is used at inference time:** Combines episode memory and note memory in a hierarchy, then updates them through conflict-aware reconsolidation.
- **Why it matters for this sub-project:** This is a clean pass-two addition because it pushes beyond flat recall toward memory self-evolution and hierarchical abstraction.
- **Caveats / limits:** Like many long-dialogue systems, it assumes a fairly elaborate write/update pipeline whose operational cost in production still needs scrutiny.
- **Abstract-level summary:** Although long-term memory systems have made substantial progress in recent years, they still exhibit clear limitations in adaptability, scalability, and self-evolution under continuous interaction settings. Inspired by cognitive theories, we propose HiMem, a hierarchical long-term memory framework for long-horizon dialogues, designed to support memory construction, retrieval, and dynamic updating during sustained interactions. HiMem constructs cognitively consistent Episode Memory via a Topic-Aware Event--Surprise Dual-Channel Segmentation strategy, and builds Note Memory that captures stable knowledge through a multi-stage information extraction pipeline. These two memory types are semantically linked to form a hierarchical structure that bridges concrete interaction events and abstract knowledge, enabling efficient retrieval without sacrificing information fidelity. HiMem supports both hybrid and best-effort retrieval strategies to balance accuracy and efficiency, and incorporates conflict-aware Memory Reconsolidation to revise and supplement stored knowledge based on retrieval feedback. This design enables continual memory self-evolution over long-term use. Experimental results on long-horizon dialogue benchmarks demonstrate that HiMem consistently outperforms representative baselines in accuracy, consistency, and long-term reasoning, while maintaining favorable efficiency. Overall, HiMem provides a principled and scalable design paradigm for building adaptive and self-evolving LLM-based conversational agents. The code is available at https://github.com/jojopdq/HiMem.
