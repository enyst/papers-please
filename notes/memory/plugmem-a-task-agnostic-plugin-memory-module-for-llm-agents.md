---
title: "PlugMem: A Task-Agnostic Plugin Memory Module for LLM Agents"
authors:
  - Ke Yang
  - Zixi Chen
  - Xuan He
  - Jize Jiang
  - Michel Galley
  - Chenglong Wang
  - Jianfeng Gao
  - Jiawei Han
  - ChengXiang Zhai
arxiv_id: "2603.03296"
arxiv_url: "https://arxiv.org/abs/2603.03296"
published: "2026-02-06"
updated: "2026-02-06"
source: "arXiv"
project: "memory"
scope_note: "core include"
agent_setting: "heterogeneous LLM agents across conversation, retrieval, and web tasks"
memory_mechanism: "Transforms episodic experience into a compact knowledge-centric memory graph that stores propositional and prescriptive knowledge as the unit of access."
icl_relevance: "high"
tags:
  - agent-memory
  - task-agnostic-memory
  - knowledge-graph
  - plugin-memory
categories:
  - cs.CL
  - cs.AI
  - cs.IR
---

- **One-line take:** A strong argument that the right memory unit is often abstract knowledge, not raw trajectory text.
- **What it stores:** Compact knowledge assertions and prescriptions abstracted from episodes, organized in a memory graph.
- **How memory is used at inference time:** Transforms episodic experience into a compact knowledge-centric memory graph that stores propositional and prescriptive knowledge as the unit of access.
- **Why it matters for this sub-project:** Promising as a general-purpose memory plugin because it tries to travel across tasks without task-specific redesign.
- **Caveats / limits:** Abstraction can discard low-level details that still matter for some downstream tasks or edge cases.
- **Abstract-level summary:** Long-term memory is essential for large language model (LLM) agents operating in complex environments, yet existing memory designs are either task-specific and non-transferable, or task-agnostic but less effective due to low task-relevance and context explosion from raw memory retrieval. We propose PlugMem, a task-agnostic plugin memory module that can be attached to arbitrary LLM agents without task-specific redesign. Motivated by the fact that decision-relevant information is concentrated as abstract knowledge rather than raw experience, we draw on cognitive science to structure episodic memories into a compact, extensible knowledge-centric memory graph that explicitly represents propositional and prescriptive knowledge. This representation enables efficient memory retrieval and reasoning over task-relevant knowledge, rather than verbose raw trajectories, and departs from other graph-based methods like GraphRAG by treating knowledge as the unit of memory access and organization instead of entities or text chunks. We evaluate PlugMem unchanged across three heterogeneous benchmarks (long-horizon conversational question answering, multi-hop knowledge retrieval, and web agent tasks). The results show that PlugMem consistently outperforms task-agnostic baselines and exceeds task-specific memory designs, while also achieving the highest information density under a unified information-theoretic analysis. Code and data are available at https://github.com/TIMAN-group/PlugMem.
