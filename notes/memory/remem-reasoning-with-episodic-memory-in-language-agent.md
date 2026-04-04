---
title: "REMem: Reasoning with Episodic Memory in Language Agent"
authors:
  - Yiheng Shu
  - Saisri Padmaja Jonnalagedda
  - Xiang Gao
  - Bernal Jiménez Gutiérrez
  - Weijian Qi
  - Kamalika Das
  - Huan Sun
  - Yu Su
arxiv_id: "2602.13530"
arxiv_url: "https://arxiv.org/abs/2602.13530"
published: "2026-02-13"
updated: "2026-02-28"
source: "arXiv"
project: "memory"
scope_note: "core include"
agent_setting: "language agents that must recollect and reason over temporally grounded events"
memory_mechanism: "Indexes experiences into a hybrid episodic memory graph and uses a tool-using retriever for iterative recollection and reasoning."
icl_relevance: "high"
tags:
  - agent-memory
  - episodic-memory
  - memory-graph
  - reasoning-over-memory
categories:
  - cs.AI
---

- **One-line take:** One of the clearest episodic-memory papers in the set: it is not just retrieval, but reasoning over remembered events.
- **What it stores:** Time-aware event gists, facts, and links between them in a hybrid memory graph.
- **How memory is used at inference time:** Indexes experiences into a hybrid episodic memory graph and uses a tool-using retriever for iterative recollection and reasoning.
- **Why it matters for this sub-project:** Useful if you care about episodicity specifically rather than generic long-term memory, especially for temporal and unanswerable-question handling.
- **Caveats / limits:** Requires fairly elaborate offline indexing and graph maintenance before online retrieval can work well.
- **Abstract-level summary:** Humans excel at remembering concrete experiences along spatiotemporal contexts and performing reasoning across those events, i.e., the capacity for episodic memory. In contrast, memory in language agents remains mainly semantic, and current agents are not yet capable of effectively recollecting and reasoning over interaction histories. We identify and formalize the core challenges of episodic recollection and reasoning from this gap, and observe that existing work often overlooks episodicity, lacks explicit event modeling, or overemphasizes simple retrieval rather than complex reasoning. We present REMem, a two-phase framework for constructing and reasoning with episodic memory: 1) Offline indexing, where REMem converts experiences into a hybrid memory graph that flexibly links time-aware gists and facts. 2) Online inference, where REMem employs an agentic retriever with carefully curated tools for iterative retrieval over the memory graph. Comprehensive evaluation across four episodic memory benchmarks shows that REMem substantially outperforms state-of-the-art memory systems such as Mem0 and HippoRAG 2, showing 3.4% and 13.4% absolute improvements on episodic recollection and reasoning tasks, respectively. Moreover, REMem also demonstrates more robust refusal behavior for unanswerable questions.
