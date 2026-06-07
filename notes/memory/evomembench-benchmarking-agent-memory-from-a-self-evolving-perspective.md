---
title: "EvoMemBench: Benchmarking Agent Memory from a Self-Evolving Perspective"
authors:
  - Yuyao Wang
  - Zhongjian Zhang
  - Mo Chi
  - Kaichi Yu
  - Yuhan Li
  - Miao Peng
  - Bing Tong
  - Chen Zhang
  - Yan Zhou
  - Jia Li
arxiv_id: "2605.18421"
arxiv_url: "https://arxiv.org/abs/2605.18421"
published: "2026-05-18"
updated: "2026-05-18"
source: "arXiv"
project: "memory"
scope_note: "pass-four include (Q2 2026 sweep)"
agent_setting: "self-evolving agents that learn from experience across sessions"
memory_mechanism: "Benchmarks memory from a self-evolution perspective: can the agent improve its own capabilities through accumulated memory?"
icl_relevance: "medium"
tags:
  - agent-memory
  - benchmark
  - self-evolution
  - evaluation
categories:
  - cs.CL
  - cs.AI
  - cs.LG
---

- **One-line take:** Does memory actually make the agent better over time? This benchmark tests self-evolution, not just recall.
- **What it stores:** See memory_mechanism above.
- **How memory is used at inference time:** Benchmarks memory from a self-evolution perspective: can the agent improve its own capabilities through accumulated memory?
- **Why it matters for this sub-project:** Asks the question that matters most: does accumulated memory translate to improved agent capability?
- **Caveats / limits:** Newly published (Q2 2026); peer validation pending.
- **Abstract-level summary:** Recent benchmarks for Large Language Model (LLM) agents mainly evaluate reasoning, planning, and execution. However, memory is also essential for agents, as it enables them to store, update, and retrieve information over time. This ability remains under-evaluated, largely because existing benchmarks do not provide a systematic way to assess memory mechanisms. In this paper, we study agent memory from a self-evolving perspective and introduce EvoMemBench, a unified benchmark organized along two axes: memory scope (in-episode vs. cross-episode) and memory content (knowledge-oriented vs. execution-oriented). We compare 15 representative memory methods with strong long-context baselines under a standardized protocol. Results show that current memory systems are still far from a general solution: long-context baselines remain highly competitive, memory helps most when the current context is insufficient or tasks are difficult, and no single memory form works consistently across all settings. Retrieval-based methods remain strong for knowledge-intensive settings, whereas procedural and long-term memory methods are more effective for execution-oriented tasks when their stored experience matches the task structure. We hope EvoMemBench facilitates future research on more effective memory systems for LLM-based agents. Our code is available at https://github.com/DSAIL-Memory/EvoMemBench.
