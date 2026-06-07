---
title: "Agent Memory: Characterization and System Implications of Stateful Long-Horizon Workloads"
authors:
  - Yasmine Omri
  - Ziyu Gan
  - Zachary Broveak
  - Robin Geens
  - Zexue He
  - Alex Pentland
  - Marian Verhelst
  - Tsachy Weissman
  - Thierry Tambe
arxiv_id: "2606.06448"
arxiv_url: "https://arxiv.org/abs/2606.06448"
published: "2026-06-04"
updated: "2026-06-04"
source: "arXiv"
project: "memory"
scope_note: "pass-four include (Q2 2026 sweep)"
agent_setting: "systems-level analysis of stateful long-horizon agent workloads"
memory_mechanism: "Characterizes agent memory as a workload class with distinct access patterns, latency profiles, and resource requirements."
icl_relevance: "medium"
tags:
  - agent-memory
  - systems-memory
  - workload-characterization
  - benchmark
categories:
  - cs.AI
---

- **One-line take:** Treats agent memory as a systems workload to be characterized and optimized, not just an AI capability.
- **What it stores:** See memory_mechanism above.
- **How memory is used at inference time:** Characterizes agent memory as a workload class with distinct access patterns, latency profiles, and resource requirements.
- **Why it matters for this sub-project:** Provides the systems-level view that most mechanism papers lack — how memory actually behaves at scale.
- **Caveats / limits:** Newly published (Q2 2026); peer validation pending.
- **Abstract-level summary:** LLM agents are increasingly deployed on long-horizon tasks requiring sustained reasoning over extended interaction histories. Realizing this at scale requires agents to persistently store, retrieve, and update their own memory across sessions. A rich ecosystem of agent memory systems has emerged spanning flat retrieval, LLM-mediated extraction, consolidating fact stores, and agentic control flows. Yet, their system-level behavior remains uncharacterized. We present the first systems characterization of agent memory. First, we introduce a system-oriented taxonomy classifying agent memory systems along four axes. Second, we build a phase-aware profiling harness attributing cost to construction, retrieval, and generation. Third, we characterize ten representative systems across two benchmark suites, uncovering how design choices shift cost across the write and read paths. Finally, we derive 10 system recommendations covering construction scheduling, capability floors, amortization via query volume, freshness-latency tradeoffs, and fleet-scale management.
