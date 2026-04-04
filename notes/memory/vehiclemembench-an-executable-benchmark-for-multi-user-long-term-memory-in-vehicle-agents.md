---
title: "VehicleMemBench: An Executable Benchmark for Multi-User Long-Term Memory in In-Vehicle Agents"
authors:
  - Yuhao Chen
  - Yi Xu
  - Xinyun Ding
  - Xiang Fang
  - Shuochen Liu
  - Luxi Lin
  - Qingyu Zhang
  - Ya Li
  - Quan Liu
  - Tong Xu
arxiv_id: "2603.23840"
arxiv_url: "https://arxiv.org/abs/2603.23840"
published: "2026-03-25"
updated: "2026-03-25"
source: "arXiv"
project: "memory"
scope_note: "pass-three meta include: benchmark/evaluation"
agent_setting: "in-vehicle agents that must balance multi-user preferences, tool use, and evolving habits over time"
memory_mechanism: "Executable benchmark that measures long-term multi-user memory by comparing tool-driven environment state changes against target states."
icl_relevance: "medium"
tags:
  - agent-memory
  - benchmark
  - multi-user-memory
  - tool-using-agents
categories:
  - cs.AI
  - cs.CL
---

- **One-line take:** Adds an executable, multi-user benchmark where memory quality is judged by real environment outcomes, not just answers.
- **What it stores:** The benchmark assumes long histories of multi-user preference events and memory-sensitive tool interactions.
- **How memory is used at inference time:** Executable benchmark that measures long-term multi-user memory by comparing tool-driven environment state changes against target states.
- **Why it matters for this sub-project:** Useful because it brings multi-user conflict and action-grounded evaluation into the corpus, which many memory benchmarks still miss.
- **Caveats / limits:** The domain is specialized, so some findings may not transfer directly beyond in-vehicle assistants.
- **Abstract-level summary:** With the growing demand for intelligent in-vehicle experiences, vehicle-based agents are evolving from simple assistants to long-term companions. This evolution requires agents to continuously model multi-user preferences and make reliable decisions in the face of inter-user preference conflicts and changing habits over time. However, existing benchmarks are largely limited to single-user, static question-answer settings, failing to capture the temporal evolution of preferences and the multi-user, tool-interactive nature of real vehicle environments. To address this gap, we introduce VehicleMemBench, a multi-user long-context memory benchmark built on an executable in-vehicle simulation environment. The benchmark evaluates tool use and memory by comparing the post-action environment state with a predefined target state, enabling objective and reproducible evaluation without LLM-based or human scoring. VehicleMemBench includes 23 tool modules, and each sample contains over 80 historical memory events. Experiments show that powerful models perform well on direct instruction tasks but struggle in scenarios involving memory evolution, particularly when user preferences change dynamically. Even advanced memory systems struggle to handle domain-specific memory requirements in this environment. These findings highlight the need for more robust and specialized memory management mechanisms to support long-term adaptive decision-making in real-world in-vehicle systems. To facilitate future research, we release the data and code.
