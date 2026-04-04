---
title: "Mem2ActBench: A Benchmark for Evaluating Long-Term Memory Utilization in Task-Oriented Autonomous Agents"
authors:
  - Yiting Shen
  - Kun Li
  - Wei Zhou
  - Songlin Hu
arxiv_id: "2601.19935"
arxiv_url: "https://arxiv.org/abs/2601.19935"
published: "2026-01-13"
updated: "2026-01-13"
source: "arXiv"
project: "memory"
scope_note: "pass-two meta include: benchmark"
agent_setting: "tool-using autonomous assistants that must apply remembered preferences and state to actions"
memory_mechanism: "Benchmark paper focused on whether agents actively use long-term memory to select tools and ground tool arguments during tasks."
icl_relevance: "medium"
tags:
  - agent-memory
  - benchmark
  - tool-using-agents
  - memory-to-action
categories:
  - cs.CL
  - cs.AI
---

- **One-line take:** Moves memory evaluation from “can you recall?” to “can you act correctly because you remembered?”.
- **What it stores:** The benchmark targets systems that store preferences, interrupted task state, and prior user choices across sessions.
- **How memory is used at inference time:** Benchmark paper focused on whether agents actively use long-term memory to select tools and ground tool arguments during tasks.
- **Why it matters for this sub-project:** Useful because many agent-memory papers optimize QA-style recall, while real assistants need memory-conditioned action selection and parameter grounding.
- **Caveats / limits:** As a benchmark it diagnoses a gap rather than closing it; gains still depend on whatever external memory system is plugged into the agent.
- **Abstract-level summary:** Large Language Model (LLM)-based agents are increasingly deployed for complex, tool-based tasks where long-term memory is critical to driving actions. Existing benchmarks, however, primarily test a angent's ability to passively retrieve isolated facts in response to explicit questions. They fail to evaluate the more crucial capability of actively applying memory to execute tasks. To address this gap, we introduce \textsc{Mem2ActBench}, a benchmark for evaluating whether agents can proactively leverage long-term memory to execute tool-based actions by selecting appropriate tools and grounding their parameters. The benchmark simulates persistent assistant usage, where users mention the same topic across long, interrupted interactions and expect previously established preferences and task states to be implicitly applied. We build the dataset with an automated pipeline that merges heterogeneous sources (ToolACE, BFCL, Oasst1), resolves conflicts via consistency modeling, and synthesizes 2,029 sessions with 12 user--assistant--tool turns on average. From these memory chains, a reverse-generation method produces 400 tool-use tasks, with human evaluation confirming 91.3\% are strongly memory-dependent. Experiments on seven memory frameworks show that current systems remain inadequate at actively utilizing memory for parameter grounding, highlighting the need for more effective approaches to evaluate and improve memory application in task execution.
