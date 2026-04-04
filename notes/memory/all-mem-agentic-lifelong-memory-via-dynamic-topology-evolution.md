---
title: "All-Mem: Agentic Lifelong Memory via Dynamic Topology Evolution"
authors:
  - Can Lv
  - Heng Chang
  - Yuchen Guo
  - Shengyu Tao
  - Shiji Zhou
arxiv_id: "2603.19595"
arxiv_url: "https://arxiv.org/abs/2603.19595"
published: "2026-03-20"
updated: "2026-03-20"
source: "arXiv"
project: "memory"
scope_note: "core include"
agent_setting: "lifelong interactive agents operating under latency and context-budget constraints"
memory_mechanism: "Maintains a topology-structured memory bank with bounded online retrieval and periodic offline edits using split, merge, and update operators."
icl_relevance: "high"
tags:
  - agent-memory
  - lifelong-memory
  - topology-evolution
  - online-offline-memory
categories:
  - cs.IR
  - cs.CL
---

- **One-line take:** Treats lifelong memory as a topology that can evolve without destructively collapsing old evidence.
- **What it stores:** Anchored visible memories plus archived evidence connected through typed, budget-aware links.
- **How memory is used at inference time:** Maintains a topology-structured memory bank with bounded online retrieval and periodic offline edits using split, merge, and update operators.
- **Why it matters for this sub-project:** This is a good pass-two mechanism paper because it tackles long-run memory drift and redundancy without relying only on summarization compression.
- **Caveats / limits:** The design assumes periodic offline maintenance, which may complicate fully online deployments or low-ops settings.
- **Abstract-level summary:** Lifelong interactive agents are expected to assist users over months or years, which requires continually writing long term memories while retrieving the right evidence for each new query under fixed context and latency budgets. Existing memory systems often degrade as histories grow, yielding redundant, outdated, or noisy retrieved contexts. We present All-Mem, an online/offline lifelong memory framework that maintains a topology structured memory bank via explicit, non destructive consolidation, avoiding the irreversible information loss typical of summarization based compression. In online operation, it anchors retrieval on a bounded visible surface to keep coarse search cost bounded. Periodically offline, an LLM diagnoser proposes confidence scored topology edits executed with gating using three operators: SPLIT, MERGE, and UPDATE, while preserving immutable evidence for traceability. At query time, typed links enable hop bounded, budgeted expansion from active anchors to archived evidence when needed. Experiments on LOCOMO and LONGMEMEVAL show improved retrieval and QA over representative baselines.
