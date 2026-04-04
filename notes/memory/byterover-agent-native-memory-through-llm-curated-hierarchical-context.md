---
title: "ByteRover: Agent-Native Memory Through LLM-Curated Hierarchical Context"
authors:
  - Andy Nguyen
  - Danh Doan
  - Hoang Pham
  - Bao Ha
  - Dat Pham
  - Linh Nguyen
  - Hieu Nguyen
  - Thien Nguyen
  - Cuong Do
  - Phat Nguyen
  - Toan Nguyen
arxiv_id: "2604.01599"
arxiv_url: "https://arxiv.org/abs/2604.01599"
published: "2026-04-02"
updated: "2026-04-02"
source: "arXiv"
project: "memory"
scope_note: "core include"
agent_setting: "persistent agents that need long-context reasoning without external memory infrastructure"
memory_mechanism: "Lets the same LLM curate and retrieve a hierarchical Context Tree with provenance, lifecycle metadata, and progressive retrieval."
icl_relevance: "high"
tags:
  - agent-memory
  - agent-native-memory
  - hierarchical-context
  - markdown-memory
categories:
  - cs.AI
---

- **One-line take:** A notable agent-native design where memory is stored as human-readable files instead of delegated to a separate retrieval stack.
- **What it stores:** Hierarchical knowledge entries with provenance, relations, importance, maturity, and recency metadata.
- **How memory is used at inference time:** Lets the same LLM curate and retrieve a hierarchical Context Tree with provenance, lifecycle metadata, and progressive retrieval.
- **Why it matters for this sub-project:** Especially relevant for lightweight local agents because it avoids dependence on vector DBs or graph DBs while keeping memory inspectable.
- **Caveats / limits:** Very new; long-run reliability of LLM-curated writes and hierarchy maintenance still needs more validation.
- **Abstract-level summary:** Memory-Augmented Generation (MAG) extends large language models with external memory to support long-context reasoning, but existing approaches universally treat memory as an external service that agents call into, delegating storage to separate pipelines of chunking, embedding, and graph extraction. This architectural separation means the system that stores knowledge does not understand it, leading to semantic drift between what the agent intended to remember and what the pipeline actually captured, loss of coordination context across agents, and fragile recovery after failures. In this paper, we propose ByteRover, an agent-native memory architecture that inverts the memory pipeline: the same LLM that reasons about a task also curates, structures, and retrieves knowledge. ByteRover represents knowledge in a hierarchical Context Tree, a file-based knowledge graph organized as Domain, Topic, Subtopic, and Entry, where each entry carries explicit relations, provenance, and an Adaptive Knowledge Lifecycle (AKL) with importance scoring, maturity tiers, and recency decay. Retrieval uses a 5-tier progressive strategy that resolves most queries at sub-100 ms latency without LLM calls, escalating to agentic reasoning only for novel questions. Experiments on LoCoMo and LongMemEval demonstrate that ByteRover achieves state-of-the-art accuracy on LoCoMo and competitive results on LongMemEval while requiring zero external infrastructure, no vector database, no graph database, no embedding service, with all knowledge stored as human-readable markdown files on the local filesystem.
