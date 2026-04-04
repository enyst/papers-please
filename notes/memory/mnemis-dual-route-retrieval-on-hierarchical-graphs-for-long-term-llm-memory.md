---
title: "Mnemis: Dual-Route Retrieval on Hierarchical Graphs for Long-Term LLM Memory"
authors:
  - Zihao Tang
  - Xin Yu
  - Ziyu Xiao
  - Zengxuan Wen
  - Zelin Li
  - Jiaxi Zhou
  - Hualei Wang
  - Haohua Wang
  - Haizhen Huang
  - Weiwei Deng
  - Feng Sun
  - Qi Zhang
arxiv_id: "2602.15313"
arxiv_url: "https://arxiv.org/abs/2602.15313"
published: "2026-02-17"
updated: "2026-02-17"
source: "arXiv"
project: "memory"
scope_note: "core include"
agent_setting: "long-term LLM memory systems that need both local similarity and global reasoning"
memory_mechanism: "Combines fast similarity retrieval with top-down global selection over a hierarchical graph so memory can be both semantically and structurally relevant."
icl_relevance: "high"
tags:
  - agent-memory
  - hierarchical-graph
  - dual-route-retrieval
  - long-term-memory
categories:
  - cs.CL
---

- **One-line take:** A clean “System 1 plus System 2” memory retrieval design for long-term agent memory.
- **What it stores:** Memories organized in both a base graph for similarity search and a hierarchical graph for deliberate traversal.
- **How memory is used at inference time:** Combines fast similarity retrieval with top-down global selection over a hierarchical graph so memory can be both semantically and structurally relevant.
- **Why it matters for this sub-project:** Strong addition because it directly addresses a common failure mode of memory systems: nearest-neighbor retrieval misses the globally relevant context.
- **Caveats / limits:** The graph-building pipeline adds complexity, and retrieval quality depends on how well the hierarchy is constructed in the first place.
- **Abstract-level summary:** AI Memory, specifically how models organizes and retrieves historical messages, becomes increasingly valuable to Large Language Models (LLMs), yet existing methods (RAG and Graph-RAG) primarily retrieve memory through similarity-based mechanisms. While efficient, such System-1-style retrieval struggles with scenarios that require global reasoning or comprehensive coverage of all relevant information. In this work, We propose Mnemis, a novel memory framework that integrates System-1 similarity search with a complementary System-2 mechanism, termed Global Selection. Mnemis organizes memory into a base graph for similarity retrieval and a hierarchical graph that enables top-down, deliberate traversal over semantic hierarchies. By combining the complementary strength from both retrieval routes, Mnemis retrieves memory items that are both semantically and structurally relevant. Mnemis achieves state-of-the-art performance across all compared methods on long-term memory benchmarks, scoring 93.9 on LoCoMo and 91.6 on LongMemEval-S using GPT-4.1-mini.
