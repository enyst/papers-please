---
title: "SuperLocalMemory: Privacy-Preserving Multi-Agent Memory with Bayesian Trust Defense Against Memory Poisoning"
authors:
  - Varun Pratap Bhardwaj
arxiv_id: "2603.02240"
arxiv_url: "https://arxiv.org/abs/2603.02240"
published: "2026-02-17"
updated: "2026-02-17"
source: "arXiv"
project: "memory"
scope_note: "pass-three security include"
agent_setting: "multi-agent local-first systems where persistent memory must remain private and robust to poisoning"
memory_mechanism: "Implements a local-first memory layer with provenance separation, Bayesian trust scoring, and adaptive re-ranking to resist memory poisoning."
icl_relevance: "medium"
tags:
  - agent-memory
  - security
  - privacy
  - memory-poisoning
categories:
  - cs.AI
  - cs.CR
---

- **One-line take:** Pushes the security slice toward practical local-first memory infrastructure instead of pure attack papers.
- **What it stores:** Local persistent memories with provenance, trust signals, knowledge-graph structure, and separate behavioral data stores.
- **How memory is used at inference time:** Implements a local-first memory layer with provenance separation, Bayesian trust scoring, and adaptive re-ranking to resist memory poisoning.
- **Why it matters for this sub-project:** Important because privacy, provenance, and trust scoring are all likely to matter in real multi-agent memory deployments.
- **Caveats / limits:** This is more systems/security engineering than a pure memory-reasoning paper, and some claims are highly implementation-specific.
- **Abstract-level summary:** We present SuperLocalMemory, a local-first memory system for multi-agent AI that defends against OWASP ASI06 memory poisoning through architectural isolation and Bayesian trust scoring, while personalizing retrieval through adaptive learning-to-rank -- all without cloud dependencies or LLM inference calls. As AI agents increasingly rely on persistent memory, cloud-based memory systems create centralized attack surfaces where poisoned memories propagate across sessions and users -- a threat demonstrated in documented attacks against production systems. Our architecture combines SQLite-backed storage with FTS5 full-text search, Leiden-based knowledge graph clustering, an event-driven coordination layer with per-agent provenance, and an adaptive re-ranking framework that learns user preferences through three-layer behavioral analysis (cross-project technology preferences, project context detection, and workflow pattern mining). Evaluation across seven benchmark dimensions demonstrates 10.6ms median search latency, zero concurrency errors under 10 simultaneous agents, trust separation (gap =0.90) with 72% trust degradation for sleeper attacks, and 104% improvement in NDCG@5 when adaptive re-ranking is enabled. Behavioral data is isolated in a separate database with GDPR Article 17 erasure support. SuperLocalMemory is open-source (MIT) and integrates with 17+ development tools via Model Context Protocol.
