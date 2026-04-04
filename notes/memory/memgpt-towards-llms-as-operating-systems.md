---
title: "MemGPT: Towards LLMs as Operating Systems"
authors:
  - Charles Packer
  - Sarah Wooders
  - Kevin Lin
  - Vivian Fang
  - Shishir G. Patil
  - Ion Stoica
  - Joseph E. Gonzalez
arxiv_id: "2310.08560"
arxiv_url: "https://arxiv.org/abs/2310.08560"
published: "2023-10-12"
updated: "2024-02-12"
source: "arXiv"
project: "memory"
scope_note: "core include"
agent_setting: "long-context document analysis and multi-session chat agents"
memory_mechanism: "Uses OS-inspired virtual context management with fast working context and slower archival memory, plus explicit context swapping."
icl_relevance: "high"
tags:
  - agent-memory
  - tiered-memory
  - context-management
  - system-design
categories:
  - cs.AI
---

- **One-line take:** Frames long-term agent memory as a systems problem: who decides what stays in active context and what gets paged out.
- **What it stores:** Active context, archival memory, and control metadata that governs movement between the tiers.
- **How memory is used at inference time:** Uses OS-inspired virtual context management with fast working context and slower archival memory, plus explicit context swapping.
- **Why it matters for this sub-project:** Important for any deployed-agent memory stack because it focuses on context budgeting and memory orchestration, not just retrieval quality.
- **Caveats / limits:** It is orchestration-heavy and can be brittle if the memory manager makes poor paging decisions.
- **Abstract-level summary:** Large language models (LLMs) have revolutionized AI, but are constrained by limited context windows, hindering their utility in tasks like extended conversations and document analysis. To enable using context beyond limited context windows, we propose virtual context management, a technique drawing inspiration from hierarchical memory systems in traditional operating systems that provide the appearance of large memory resources through data movement between fast and slow memory. Using this technique, we introduce MemGPT (Memory-GPT), a system that intelligently manages different memory tiers in order to effectively provide extended context within the LLM's limited context window, and utilizes interrupts to manage control flow between itself and the user. We evaluate our OS-inspired design in two domains where the limited context windows of modern LLMs severely handicaps their performance: document analysis, where MemGPT is able to analyze large documents that far exceed the underlying LLM's context window, and multi-session chat, where MemGPT can create conversational agents that remember, reflect, and evolve dynamically through long-term interactions with their users. We release MemGPT code and data for our experiments at https://memgpt.ai.
