---
title: "MemCog: From Memory-as-Tool to Memory-as-Cognition in Conversational Agents"
authors:
  - Zihan Li
  - Xingyu Fan
  - Feifei Li
  - Wenhui Que
arxiv_id: "2605.28046"
arxiv_url: "https://arxiv.org/abs/2605.28046"
published: "2026-05-27"
updated: "2026-05-27"
source: "arXiv"
project: "memory"
scope_note: "pass-four include (Q2 2026 sweep)"
agent_setting: "conversational agents with structured memory"
memory_mechanism: "Replaces one-shot retrieval with reasoning-driven multi-step memory traversal over associative link graphs, with proactive memory triggering."
icl_relevance: "medium"
tags:
  - agent-memory
  - memory-as-cognition
  - associative-memory
  - proactive-retrieval
categories:
  - cs.AI
  - cs.CL
---

- **One-line take:** Memory is not a tool you call — it is cognition you do. A paradigm shift from retrieval to reasoning-over-memory.
- **What it stores:** See memory_mechanism above.
- **How memory is used at inference time:** Replaces one-shot retrieval with reasoning-driven multi-step memory traversal over associative link graphs, with proactive memory triggering.
- **Why it matters for this sub-project:** Proposes a fundamental rethinking of how memory integrates with reasoning, not just retrieval.
- **Caveats / limits:** Newly published (Q2 2026); peer validation pending.
- **Abstract-level summary:** Existing agent memory systems universally follow what we term a Memory-as-Tool paradigm where a single query triggers one-shot retrieval of flat passage lists, suffering from passive invocation, reasoning-retrieval decoupling, and structural mismatch between retrieved fragments and the agent's navigational needs. We propose MemCog, a Memory-as-Cognition system that makes memory access an integral part of the reasoning process. MemCog organizes user knowledge as Navigable Memory Store with associative link graphs, exposes Cross-Dimensional Navigation Interface for multi-step reasoning-driven traversal, and employs Proactive Reasoning Protocol that drives agents to spontaneously initiate memory exploration from conversational context. We additionally construct ProactiveMemBench, the first benchmark for evaluating proactive memory triggering. Experiments show that MemCog achieves state-of-the-art on passive QA benchmarks (92.98 on LoCoMo, 95.8 on LongMemEval) while substantially outperforming baselines on ProactiveMemBench, demonstrating the advantage of Memory-as-Cognition.
