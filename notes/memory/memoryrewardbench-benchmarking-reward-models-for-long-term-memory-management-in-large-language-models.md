---
title: "MemoryRewardBench: Benchmarking Reward Models for Long-Term Memory Management in Large Language Models"
authors:
  - Zecheng Tang
  - Baibei Ji
  - Ruoxi Sun
  - Haitian Wang
  - WangJie You
  - Zhang Yijun
  - Wenpeng Zhu
  - Ji Qi
  - Juntao Li
  - Min Zhang
arxiv_id: "2601.11969"
arxiv_url: "https://arxiv.org/abs/2601.11969"
published: "2026-01-17"
updated: "2026-01-24"
source: "arXiv"
project: "memory"
scope_note: "pass-three meta include: benchmark/evaluation"
agent_setting: "meta-evaluation of memory management quality across long-context and long-form generation settings"
memory_mechanism: "Benchmark paper evaluating whether reward models can reliably score long-term memory-management processes across varied settings."
icl_relevance: "low"
tags:
  - agent-memory
  - benchmark
  - reward-models
  - memory-evaluation
categories:
  - cs.CL
  - cs.AI
---

- **One-line take:** Asks a second-order question: can we even evaluate memory management well with current reward models?
- **What it stores:** Not a new storage scheme; instead it benchmarks reward-model judgments over memory-management behavior.
- **How memory is used at inference time:** Benchmark paper evaluating whether reward models can reliably score long-term memory-management processes across varied settings.
- **Why it matters for this sub-project:** Useful for the corpus because evaluation quality shapes which memory methods will look good in future automated optimization loops.
- **Caveats / limits:** It is an evaluation artifact, not a deployed memory mechanism, so its value is mostly methodological.
- **Abstract-level summary:** Existing works increasingly adopt memory-centric mechanisms to process long contexts in a segment manner, and effective memory management is one of the key capabilities that enables large language models to effectively propagate information across the entire sequence. Therefore, leveraging reward models (RMs) to automatically and reliably evaluate memory quality is critical. In this work, we introduce MemoryRewardBench, the first benchmark to systematically study the ability of RMs to evaluate long-term memory management processes. MemoryRewardBench covers both long-context comprehension and long-form generation tasks, featuring 10 distinct settings with different memory management patterns, with context length ranging from 8K to 128K tokens. Evaluations on 13 cutting-edge RMs indicate a diminishing performance gap between open-source and proprietary models, with newer-generation models consistently outperforming their predecessors regardless of parameter count. We further expose the capabilities and fundamental limitations of current RMs in evaluating LLM memory management across diverse settings.
