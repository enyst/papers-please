---
title: "AMA: Adaptive Memory via Multi-Agent Collaboration"
authors:
  - Weiquan Huang
  - Zixuan Wang
  - Hehai Lin
  - Sudong Wang
  - Bo Xu
  - Qian Li
  - Beier Zhu
  - Linyi Yang
  - Chengwei Qin
arxiv_id: "2601.20352"
arxiv_url: "https://arxiv.org/abs/2601.20352"
published: "2026-01-28"
updated: "2026-02-02"
source: "arXiv"
project: "memory"
scope_note: "core include"
agent_setting: "LLM agents that need long-term memory consistency and task-matched retrieval granularity"
memory_mechanism: "Uses coordinated agents to construct, retrieve, judge, and refresh memory at multiple granularities, with conflict-triggered updates."
icl_relevance: "high"
tags:
  - agent-memory
  - multi-agent-memory
  - adaptive-retrieval
  - memory-consistency
categories:
  - cs.AI
---

- **One-line take:** A multi-agent memory manager that adapts retrieval granularity and actively repairs inconsistent memory.
- **What it stores:** Hierarchical memories at multiple granularities plus consistency signals used to refresh or remove outdated entries.
- **How memory is used at inference time:** Uses coordinated agents to construct, retrieve, judge, and refresh memory at multiple granularities, with conflict-triggered updates.
- **Why it matters for this sub-project:** A good pass-three addition because it goes beyond retrieval into explicit memory verification and refresh behavior.
- **Caveats / limits:** The multi-agent control loop is more complex than simpler memory stacks and may be costly to maintain in production.
- **Abstract-level summary:** The rapid evolution of Large Language Model (LLM) agents has necessitated robust memory systems to support cohesive long-term interaction and complex reasoning. Benefiting from the strong capabilities of LLMs, recent research focus has shifted from simple context extension to the development of dedicated agentic memory systems. However, existing approaches typically rely on rigid retrieval granularity, accumulation-heavy maintenance strategies, and coarse-grained update mechanisms. These design choices create a persistent mismatch between stored information and task-specific reasoning demands, while leading to the unchecked accumulation of logical inconsistencies over time. To address these challenges, we propose Adaptive Memory via Multi-Agent Collaboration (AMA), a novel framework that leverages coordinated agents to manage memory across multiple granularities. AMA employs a hierarchical memory design that dynamically aligns retrieval granularity with task complexity. Specifically, the Constructor and Retriever jointly enable multi-granularity memory construction and adaptive query routing. The Judge verifies the relevance and consistency of retrieved content, triggering iterative retrieval when evidence is insufficient or invoking the Refresher upon detecting logical conflicts. The Refresher then enforces memory consistency by performing targeted updates or removing outdated entries. Extensive experiments on challenging long-context benchmarks show that AMA significantly outperforms state-of-the-art baselines while reducing token consumption by approximately 80% compared to full-context methods, demonstrating its effectiveness in maintaining retrieval precision and long-term memory consistency.
