---
title: "TraceMem: Weaving Narrative Memory Schemata from User Conversational Traces"
authors:
  - Yiming Shu
  - Pei Liu
  - Tiange Zhang
  - Ruiyang Gao
  - Jun Ma
  - Chen Sun
arxiv_id: "2602.09712"
arxiv_url: "https://arxiv.org/abs/2602.09712"
published: "2026-02-10"
updated: "2026-02-10"
source: "arXiv"
project: "memory"
scope_note: "core include"
agent_setting: "long-horizon conversational agents"
memory_mechanism: "Segments conversation into episodes, consolidates those into user traces, clusters them into narrative threads, and searches them agentically at answer time."
icl_relevance: "high"
tags:
  - agent-memory
  - narrative-memory
  - conversation-memory
  - episodic-memory
categories:
  - cs.CL
---

- **One-line take:** Turns long conversation history into evolving narrative structure instead of a bag of snippets.
- **What it stores:** Episode summaries, user traces, and higher-level narrative memory cards organized under themes.
- **How memory is used at inference time:** Segments conversation into episodes, consolidates those into user traces, clusters them into narrative threads, and searches them agentically at answer time.
- **Why it matters for this sub-project:** Especially interesting for temporal and multi-hop reasoning, where the relation between memories matters as much as the individual facts.
- **Caveats / limits:** Pipeline complexity is high, and most benefits are shown in conversation-style memory benchmarks.
- **Abstract-level summary:** Sustaining long-term interactions remains a bottleneck for Large Language Models (LLMs), as their limited context windows struggle to manage dialogue histories that extend over time. Existing memory systems often treat interactions as disjointed snippets, failing to capture the underlying narrative coherence of the dialogue stream. We propose TraceMem, a cognitively-inspired framework that weaves structured, narrative memory schemata from user conversational traces through a three-stage pipeline: (1) Short-term Memory Processing, which employs a deductive topic segmentation approach to demarcate episode boundaries and extract semantic representation; (2) Synaptic Memory Consolidation, a process that summarizes episodes into episodic memories before distilling them alongside semantics into user-specific traces; and (3) Systems Memory Consolidation, which utilizes two-stage hierarchical clustering to organize these traces into coherent, time-evolving narrative threads under unifying themes. These threads are encapsulated into structured user memory cards, forming narrative memory schemata. For memory utilization, we provide an agentic search mechanism to enhance reasoning process. Evaluation on the LoCoMo benchmark shows that TraceMem achieves state-of-the-art performance with a brain-inspired architecture. Analysis shows that by constructing coherent narratives, it surpasses baselines in multi-hop and temporal reasoning, underscoring its essential role in deep narrative comprehension. Additionally, we provide an open discussion on memory systems, offering our perspectives and future outlook on the field. Our code implementation is available at: https://github.com/YimingShu-teay/TraceMem
