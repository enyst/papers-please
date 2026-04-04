---
title: "GAAMA: Graph Augmented Associative Memory for Agents"
authors:
  - Swarna Kamal Paul
  - Shubhendu Sharma
  - Nitin Sareen
arxiv_id: "2603.27910"
arxiv_url: "https://arxiv.org/abs/2603.27910"
published: "2026-03-29"
updated: "2026-03-29"
source: "arXiv"
project: "memory"
scope_note: "core include"
agent_setting: "persistent multi-session agents that need coherent personalized behavior"
memory_mechanism: "Builds a concept-mediated hierarchical graph linking episodes, facts, reflections, and concepts, then retrieves with semantic search plus graph ranking."
icl_relevance: "high"
tags:
  - agent-memory
  - graph-memory
  - associative-memory
  - hierarchical-reflection
categories:
  - cs.AI
  - cs.IR
  - cs.MA
---

- **One-line take:** A graph-memory system that tries to preserve both verbatim evidence and higher-order reflective structure.
- **What it stores:** Episode nodes, atomic facts, higher-order reflections, and cross-cutting concept nodes.
- **How memory is used at inference time:** Builds a concept-mediated hierarchical graph linking episodes, facts, reflections, and concepts, then retrieves with semantic search plus graph ranking.
- **Why it matters for this sub-project:** Useful because it combines several strong memory motifs in one design: preservation, abstraction, reflection, and associative traversal.
- **Caveats / limits:** Like other graph-heavy methods, its upside depends on robust extraction and graph maintenance, which may be costly or brittle in noisier deployments.
- **Abstract-level summary:** AI agents that interact with users across multiple sessions require persistent long-term memory to maintain coherent, personalized behavior. Current approaches either rely on flat retrieval-augmented generation (RAG), which loses structural relationships between memories, or use memory compression and vector retrieval that cannot capture the associative structure of multi-session conversations. There are few graph-based techniques proposed in the literature, however they still suffer from hub-dominated retrieval and poor hierarchical reasoning over evolving memory. We propose GAAMA, a graph-augmented associative memory system that constructs a concept-mediated hierarchical knowledge graph through a three-step pipeline: (1)~verbatim episode preservation from raw conversations, (2)~LLM-based extraction of atomic facts and topic-level concept nodes, and (3)~synthesis of higher-order reflections. The resulting graph uses four node types (episode, fact, reflection, concept) connected by five structural edge types, with concept nodes providing cross-cutting traversal paths that complement semantic similarity. Retrieval combines cosine-similarity-based $k$-nearest neighbor search with edge-type-aware Personalized PageRank (PPR) through an additive scoring function. On the LoCoMo-10 benchmark (1,540 questions across 10 multi-session conversations), GAAMA achieves 78.9\% mean reward, outperforming a tuned RAG baseline (75.0\%), HippoRAG (69.9\%), A-Mem (47.2\%), and Nemori (52.1\%). Ablation analysis shows that augmenting graph-traversal-based ranking (Personalized PageRank) with semantic search consistently improves over pure semantic search on graph nodes (+1.0 percentage point overall).
