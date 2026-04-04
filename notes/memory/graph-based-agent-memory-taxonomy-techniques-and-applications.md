---
title: "Graph-based Agent Memory: Taxonomy, Techniques, and Applications"
authors:
  - Chang Yang
  - Chuang Zhou
  - Yilin Xiao
  - Su Dong
  - Luyao Zhuang
  - Yujing Zhang
  - Zhu Wang
  - Zijin Hong
  - Zheng Yuan
  - Zhishang Xiang
  - Shengyuan Chen
  - Huachi Zhou
  - Qinggang Zhang
  - Ninghao Liu
  - Jinsong Su
  - Xinrun Wang
  - Yi Chang
  - Xiao Huang
arxiv_id: "2602.05665"
arxiv_url: "https://arxiv.org/abs/2602.05665"
published: "2026-02-05"
updated: "2026-02-05"
source: "arXiv"
project: "memory"
scope_note: "pass-two meta include: taxonomy"
agent_setting: "broad survey across long-horizon LLM agent settings"
memory_mechanism: "Survey and taxonomy paper covering graph-based memory extraction, storage, retrieval, and evolution across agent lifecycles."
icl_relevance: "medium"
tags:
  - agent-memory
  - survey
  - taxonomy
  - graph-memory
categories:
  - cs.AI
---

- **One-line take:** A useful map of the graph-memory subfield rather than a single new memory system.
- **What it stores:** Not applicable as a mechanism paper; it organizes prior graph-memory approaches by memory type and lifecycle stage.
- **How memory is used at inference time:** Survey and taxonomy paper covering graph-based memory extraction, storage, retrieval, and evolution across agent lifecycles.
- **Why it matters for this sub-project:** Helpful for orienting the growing literature because several pass-one and pass-two systems now rely on graphs, hierarchies, or structured retrieval over memories.
- **Caveats / limits:** Because it is a survey, it should guide reading and comparison rather than be treated as direct empirical evidence for one design choice.
- **Abstract-level summary:** Memory emerges as the core module in the Large Language Model (LLM)-based agents for long-horizon complex tasks (e.g., multi-turn dialogue, game playing, scientific discovery), where memory can enable knowledge accumulation, iterative reasoning and self-evolution. Among diverse paradigms, graph stands out as a powerful structure for agent memory due to the intrinsic capabilities to model relational dependencies, organize hierarchical information, and support efficient retrieval. This survey presents a comprehensive review of agent memory from the graph-based perspective. First, we introduce a taxonomy of agent memory, including short-term vs. long-term memory, knowledge vs. experience memory, non-structural vs. structural memory, with an implementation view of graph-based memory. Second, according to the life cycle of agent memory, we systematically analyze the key techniques in graph-based agent memory, covering memory extraction for transforming the data into the contents, storage for organizing the data efficiently, retrieval for retrieving the relevant contents from memory to support reasoning, and evolution for updating the contents in the memory. Third, we summarize the open-sourced libraries and benchmarks that support the development and evaluation of self-evolving agent memory. We also explore diverse application scenarios. Finally, we identify critical challenges and future research directions. This survey aims to offer actionable insights to advance the development of more efficient and reliable graph-based agent memory systems. All the related resources, including research papers, open-source data, and projects, are collected for the community in https://github.com/DEEP-PolyU/Awesome-GraphMemory.
