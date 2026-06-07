---
title: "RecMem: Recurrence-based Memory Consolidation for Efficient and Effective Long-Running LLM Agents"
authors:
  - Zijie Dai
  - Shiyuan Deng
  - Sheng Guan
  - Yizhou Tian
  - Xin Yao
  - Xiao Yan
  - James Cheng
arxiv_id: "2605.16045"
arxiv_url: "https://arxiv.org/abs/2605.16045"
published: "2026-05-15"
updated: "2026-05-15"
source: "arXiv"
project: "memory"
scope_note: "pass-four include (Q2 2026 sweep)"
agent_setting: "long-running LLM agents with growing memory stores"
memory_mechanism: "Uses recurrence-based consolidation that periodically compresses and reorganizes memory through iterative passes."
icl_relevance: "medium"
tags:
  - agent-memory
  - memory-consolidation
  - long-running-agents
  - compression
categories:
  - cs.CL
  - cs.AI
  - cs.LG
---

- **One-line take:** Iterative consolidation passes that compress memory like a recurrent network — each pass distills further.
- **What it stores:** See memory_mechanism above.
- **How memory is used at inference time:** Uses recurrence-based consolidation that periodically compresses and reorganizes memory through iterative passes.
- **Why it matters for this sub-project:** An alternative consolidation strategy to single-pass summarization — multiple passes extract more.
- **Caveats / limits:** Newly published (Q2 2026); peer validation pending.
- **Abstract-level summary:** Memory systems often organize user-agent interactions as retrievable external memory and are crucial for long-running agents by overcoming the limited context windows of LLMs. However, existing memory systems invoke LLMs to process every incoming interaction for memory extraction, and such an eager memory consolidation scheme leads to substantial token consumption. To tackle this problem, we propose RecMem by rethinking when memory consolidation should be conducted. RecMem stores incoming interactions in a subconscious memory layer and encode them using lightweight embedding models for retrieval. LLMs are only invoked to extract episodic and semantic memory when sustained recurrence are observed for semantically similar interactions. Such recurrence-based consolidation works because these interactions correspond to a semantic cluster with rich information and thus are worth extraction and summarization. To improve accuracy, RecMem also incorporates a semantic refinement mechanism that recovers the fine-grained facts omitted by memory extraction. Experiments show that RecMem reduces the memory construction token cost of three SOTA memory systems by up to 87% while exceeding their accuracy.
