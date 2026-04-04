---
title: "A-MEM: Agentic Memory for LLM Agents"
authors:
  - Wujiang Xu
  - Zujie Liang
  - Kai Mei
  - Hang Gao
  - Juntao Tan
  - Yongfeng Zhang
arxiv_id: "2502.12110"
arxiv_url: "https://arxiv.org/abs/2502.12110"
published: "2025-02-17"
updated: "2025-10-08"
source: "arXiv"
project: "memory"
scope_note: "core include"
agent_setting: "general LLM agents across multiple models and task settings"
memory_mechanism: "Creates structured notes with contextual attributes, keywords, and tags, then dynamically links and updates them in a growing memory network."
icl_relevance: "high"
tags:
  - agent-memory
  - graph-memory
  - zettelkasten
  - structured-notes
categories:
  - cs.CL
  - cs.HC
---

- **One-line take:** A memory-first design that pushes beyond flat retrieval by letting the agent build and revise a linked note graph over time.
- **What it stores:** Structured note-like memories plus semantic links between related memories.
- **How memory is used at inference time:** Creates structured notes with contextual attributes, keywords, and tags, then dynamically links and updates them in a growing memory network.
- **Why it matters for this sub-project:** Useful if you care about memory organization as much as memory retrieval; it is closer to an externalized notebook than a plain vector store.
- **Caveats / limits:** The write path is more complex than simple extract-and-retrieve systems, and long-term maintenance cost is an open question.
- **Abstract-level summary:** While large language model (LLM) agents can effectively use external tools for complex real-world tasks, they require memory systems to leverage historical experiences. Current memory systems enable basic storage and retrieval but lack sophisticated memory organization, despite recent attempts to incorporate graph databases. Moreover, these systems' fixed operations and structures limit their adaptability across diverse tasks. To address this limitation, this paper proposes a novel agentic memory system for LLM agents that can dynamically organize memories in an agentic way. Following the basic principles of the Zettelkasten method, we designed our memory system to create interconnected knowledge networks through dynamic indexing and linking. When a new memory is added, we generate a comprehensive note containing multiple structured attributes, including contextual descriptions, keywords, and tags. The system then analyzes historical memories to identify relevant connections, establishing links where meaningful similarities exist. Additionally, this process enables memory evolution - as new memories are integrated, they can trigger updates to the contextual representations and attributes of existing historical memories, allowing the memory network to continuously refine its understanding. Our approach combines the structured organization principles of Zettelkasten with the flexibility of agent-driven decision making, allowing for more adaptive and context-aware memory management. Empirical experiments on six foundation models show superior improvement against existing SOTA baselines. The source code for evaluating performance is available at https://github.com/WujiangXu/A-mem, while the source code of the agentic memory system is available at https://github.com/WujiangXu/A-mem-sys.
