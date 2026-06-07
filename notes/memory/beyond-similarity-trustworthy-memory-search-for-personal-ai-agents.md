---
title: "Beyond Similarity: Trustworthy Memory Search for Personal AI Agents"
authors:
  - Jiawen Zhang
  - Kejia Chen
  - Jiachen Ma
  - Yangfan Hu
  - Lipeng He
  - Yechao Zhang
  - Jian Liu
  - Xiaohu Yang
  - Tianwei Zhang
  - Ruoxi Jia
arxiv_id: "2606.06054"
arxiv_url: "https://arxiv.org/abs/2606.06054"
published: "2026-06-04"
updated: "2026-06-04"
source: "arXiv"
project: "memory"
scope_note: "pass-four include (Q2 2026 sweep)"
agent_setting: "personal AI agents with long-term memory"
memory_mechanism: "Adds trust dimensions to memory search beyond semantic similarity — provenance, recency, confidence, and user verification status."
icl_relevance: "medium"
tags:
  - agent-memory
  - trustworthy-retrieval
  - personalization
  - security
categories:
  - cs.AI
---

- **One-line take:** Memory search should consider trust, not just relevance — a key insight for secure memory systems.
- **What it stores:** See memory_mechanism above.
- **How memory is used at inference time:** Adds trust dimensions to memory search beyond semantic similarity — provenance, recency, confidence, and user verification status.
- **Why it matters for this sub-project:** Bridges the gap between retrieval quality and security by making trust a first-class retrieval dimension.
- **Caveats / limits:** Newly published (Q2 2026); peer validation pending.
- **Abstract-level summary:** Personal AI agents increasingly rely on long-term memory to provide persistent personalization across sessions. However, existing memory pipelines are largely driven by semantic similarity: memory data close to the current query is retrieved and injected into the model context. This creates a critical trustworthiness gap, since a semantically related memory may still be contextually inappropriate, leading to threats such as cross-domain leakage, sycophancy, tool-call drift, or memory-induced jailbreaks.   In this paper, we study memory search as a trust boundary in personal AI agents. We evaluate representative agentic memory frameworks, including A-Mem, Mem0, and MemOS, together with OpenClaw, a real-world personal-agent environment with persistent state and tool-use capability. Our results show that long-term memory is not merely a utility layer, but a durable control channel that can reshape how agents interpret tasks and execute actions, leaving them highly susceptible to the aforementioned threats. To mitigate these vulnerabilities, we propose MemGate, a lightweight and deployable memory plug-in for trustworthy memory search, with only 9M parameters and a 35.1MB footprint. MemGate is inserted between the vector memory store and the backbone LLM, requiring no LLM modification, memory-database rewriting, or inference-time LLM judge. It applies a query-conditioned neural gate to candidate memory representations, turning raw similarity search into task-conditioned memory admission. Across multiple mainstream memory frameworks, real-world agent settings, and diverse LLM backbones, MemGate reduces memory-induced threats while preserving long-term memory utility.
