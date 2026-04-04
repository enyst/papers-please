---
title: "DeltaMem: Towards Agentic Memory Management via Reinforcement Learning"
authors:
  - Qi Zhang
  - Shen Huang
  - Chu Liu
  - Shouqing Yang
  - Junbo Zhao
  - Haobo Wang
  - Pengjun Xie
arxiv_id: "2604.01560"
arxiv_url: "https://arxiv.org/abs/2604.01560"
published: "2026-04-02"
updated: "2026-04-02"
source: "arXiv"
project: "memory"
scope_note: "borderline include: the runtime memory manager is relevant, but RL training is a core part of the proposal."
agent_setting: "persona-centric conversational agents"
memory_mechanism: "Treats memory editing as an end-to-end agentic task with operation-level updates and RL-tuned memory-management policies."
icl_relevance: "medium"
tags:
  - agent-memory
  - persona-memory
  - memory-management
  - borderline-trained
categories:
  - cs.CL
---

- **One-line take:** Focuses on memory management actions themselves—what to add, edit, or keep—rather than just on retrieval.
- **What it stores:** Persona-centric conversational memory with explicit update operations.
- **How memory is used at inference time:** Treats memory editing as an end-to-end agentic task with operation-level updates and RL-tuned memory-management policies.
- **Why it matters for this sub-project:** Useful if you want to study memory maintenance as an action policy, especially in personalization-heavy assistants.
- **Caveats / limits:** Borderline for this corpus because the paper leans heavily on training the manager, not just on inference-time memory structure.
- **Abstract-level summary:** Recent advances in persona-centric memory have revealed the powerful capability of multi-agent systems in managing persona memory, especially in conversational scenarios. However, these complex frameworks often suffer from information loss and are fragile across varying scenarios, resulting in suboptimal performance. In this paper, we propose DeltaMem, an agentic memory management system that formulates persona-centric memory management as an end-to-end task within a single-agent setting. To further improve the performance of our agentic memory manager, we draw inspiration from the evolution of human memory and synthesize a user-assistant dialogue dataset along with corresponding operation-level memory updating labels. Building on this, we introduce a novel Memory-based Levenshtein Distance to formalize the memory updating reward, and propose a tailored reinforcement learning framework to further enhance the management capabilities of DeltaMem. Extensive experiments show that both training-free and RL-trained DeltaMem outperform all product-level baselines across diverse long-term memory benchmarks, including LoCoMo, HaluMem, and PersonaMem.
