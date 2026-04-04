---
title: "MemCtrl: Using MLLMs as Active Memory Controllers on Embodied Agents"
authors:
  - Vishnu Sashank Dorbala
  - Dinesh Manocha
arxiv_id: "2601.20831"
arxiv_url: "https://arxiv.org/abs/2601.20831"
published: "2026-01-28"
updated: "2026-01-28"
source: "arXiv"
project: "memory"
scope_note: "borderline include: the runtime memory problem is central, but the controller is trained rather than purely hand-designed."
agent_setting: "embodied agents operating under strict online memory and compute constraints"
memory_mechanism: "Uses an active memory controller to decide which observations or reflections to retain, update, or discard during exploration."
icl_relevance: "medium"
tags:
  - agent-memory
  - embodied-agent
  - memory-budgeting
  - borderline-trained
categories:
  - cs.AI
  - cs.RO
---

- **One-line take:** A useful reminder that deployed memory is also a budgeting problem: what should survive online when context is scarce.
- **What it stores:** Selected observations and reflections deemed worth keeping for later embodied decision making.
- **How memory is used at inference time:** Uses an active memory controller to decide which observations or reflections to retain, update, or discard during exploration.
- **Why it matters for this sub-project:** Relevant for memory under embodied constraints, where every retained token competes with future perception and planning needs.
- **Caveats / limits:** Borderline for this corpus because part of the contribution is training the controller, not only inference-time memory design.
- **Abstract-level summary:** Foundation models rely on in-context learning for personalized decision making. The limited size of this context window necessitates memory compression and retrieval systems like RAG. These systems however often treat memory as large offline storage spaces, which is unfavorable for embodied agents that are expected to operate under strict memory and compute constraints, online. In this work, we propose MemCtrl, a novel framework that uses Multimodal Large Language Models (MLLMs) for pruning memory online. MemCtrl augments MLLMs with a trainable memory head μthat acts as a gate to determine which observations or reflections to retain, update, or discard during exploration. We evaluate with training two types of μ, 1) via an offline expert, and 2) via online RL, and observe significant improvement in overall embodied task completion ability on μ-augmented MLLMs. In particular, on augmenting two low performing MLLMs with MemCtrl on multiple subsets of the EmbodiedBench benchmark, we observe that μ-augmented MLLMs show an improvement of around 16% on average, with over 20% on specific instruction subsets. Finally, we present a qualitative analysis on the memory fragments collected by μ, noting the superior performance of μaugmented MLLMs on long and complex instruction types.
