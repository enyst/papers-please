---
title: "Mem-Gallery: Benchmarking Multimodal Long-Term Conversational Memory for MLLM Agents"
authors:
  - Yuanchen Bei
  - Tianxin Wei
  - Xuying Ning
  - Yanjun Zhao
  - Zhining Liu
  - Xiao Lin
  - Yada Zhu
  - Hendrik Hamann
  - Jingrui He
  - Hanghang Tong
arxiv_id: "2601.03515"
arxiv_url: "https://arxiv.org/abs/2601.03515"
published: "2026-01-07"
updated: "2026-01-07"
source: "arXiv"
project: "memory"
scope_note: "pass-two meta include: benchmark"
agent_setting: "multimodal conversational MLLM agents operating across long interaction horizons"
memory_mechanism: "Benchmark paper that evaluates how systems extract, adapt, reason over, and manage multimodal long-term conversational memory."
icl_relevance: "medium"
tags:
  - agent-memory
  - benchmark
  - multimodal-memory
  - evaluation
categories:
  - cs.CL
  - cs.AI
---

- **One-line take:** A benchmark for the gap between text-only memory evaluation and truly multimodal long-term conversational memory.
- **What it stores:** The benchmark tests systems that store and evolve visual and textual conversational memories across many sessions rather than defining one new memory store itself.
- **How memory is used at inference time:** Benchmark paper that evaluates how systems extract, adapt, reason over, and manage multimodal long-term conversational memory.
- **Why it matters for this sub-project:** Useful for pass two because it expands the corpus from memory mechanisms into the evaluation infrastructure needed to compare multimodal memory systems seriously.
- **Caveats / limits:** It is an evaluation paper, not a new deployed memory architecture, so its value is primarily in measurement rather than direct system design.
- **Abstract-level summary:** Long-term memory is a critical capability for multimodal large language model (MLLM) agents, particularly in conversational settings where information accumulates and evolves over time. However, existing benchmarks either evaluate multi-session memory in text-only conversations or assess multimodal understanding within localized contexts, failing to evaluate how multimodal memory is preserved, organized, and evolved across long-term conversational trajectories. Thus, we introduce Mem-Gallery, a new benchmark for evaluating multimodal long-term conversational memory in MLLM agents. Mem-Gallery features high-quality multi-session conversations grounded in both visual and textual information, with long interaction horizons and rich multimodal dependencies. Building on this dataset, we propose a systematic evaluation framework that assesses key memory capabilities along three functional dimensions: memory extraction and test-time adaptation, memory reasoning, and memory knowledge management. Extensive benchmarking across thirteen memory systems reveals several key findings, highlighting the necessity of explicit multimodal information retention and memory organization, the persistent limitations in memory reasoning and knowledge management, as well as the efficiency bottleneck of current models.
