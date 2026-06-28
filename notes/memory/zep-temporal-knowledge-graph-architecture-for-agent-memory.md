---
title: "Zep: A Temporal Knowledge Graph Architecture for Agent Memory"
authors:
  - Preston Rasmussen
  - Pavlo Paliychuk
  - Travis Beauvais
  - Jack Ryan
  - Daniel Chalef
arxiv_id: "2501.13956"
arxiv_url: "https://arxiv.org/abs/2501.13956"
published: "2025-01-20"
source: "arXiv"
repo: "https://github.com/getzep/graphiti"
project: "memory"
scope_note: "core include — tool + paper"
agent_setting: "production conversational and business agents over evolving data"
memory_mechanism: "Temporal knowledge graph (Graphiti) that ingests messages and business data into time-aware, provenance-tracked fact triples; retrieval is pull-based via graph + semantic + keyword search."
icl_relevance: "high"
tags:
  - agent-memory
  - knowledge-graph
  - temporal
  - pull-memory
  - production
  - tool
categories:
  - retrieval
  - knowledge-graph
---

# Zep / Graphiti — temporal knowledge graph for agent memory

**Tool + paper.** Zep is a production memory layer; its open-source engine is
**Graphiti** (`github.com/getzep/graphiti`, Python, Apache-2.0, ~4.7k★). The
paper reports beating MemGPT on the Deep Memory Retrieval benchmark and strong
results on LongMemEval with large latency reductions.

## Mechanism

- **Temporal knowledge graph, not static.** Facts are stored as triples with
  **validity intervals** — Graphiti tracks *when* a fact became true and when it
  was superseded, instead of overwriting. This is first-class **eviction /
  contradiction handling**: a changed fact (user moved cities) doesn't clobber
  history, it closes the old edge's time range and opens a new one.
- **Provenance to source data** — every fact links back to the message/document
  it came from (index-not-copy in graph form).
- **Hybrid retrieval** — semantic + keyword + graph traversal, pulled on demand
  rather than force-loaded into context.
- Supports both prescribed and learned ontology; ships an **MCP server** so
  Claude/Cursor/other clients get graph memory.

## Why it matters to us

The temporal-validity model is the cleanest published answer to the
"timely forgetting of outdated information" problem (the Qwen MemoryAgent track
ask, and dreamem's contradiction case). Where dreamem marks a fact `superseded`,
Zep closes a time interval — same idea, richer representation. Strong reference
for dreamem's competitive landscape and for the "pull memory" half of the
push-vs-pull distinction (cf. Van Horn's "Your AI's Memory Is Quietly Making It
Dumber"). Related local notes: `mem0`, `memgpt`, `memorywire`.
