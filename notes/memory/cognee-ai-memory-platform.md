---
title: "Cognee — open-source AI memory platform for agents"
authors:
  - topoteretes (Vasilije Markovic, et al.)
source: "GitHub / docs"
repo: "https://github.com/topoteretes/cognee"
project: "memory"
scope_note: "context include — tool"
agent_setting: "self-hosted persistent long-term memory / knowledge graph for agents"
memory_mechanism: "ECL (Extract, Cognify, Load) pipeline: ingest data in any format, build a self-hosted knowledge graph + vector store, then let agents recall and connect facts with full context."
icl_relevance: "medium"
tags:
  - agent-memory
  - knowledge-graph
  - vector-store
  - self-hosted
  - ECL
  - tool
categories:
  - retrieval
  - knowledge-graph
---

# Cognee — open-source AI memory platform

`github.com/topoteretes/cognee` (Python, Apache-2.0, ~24k★). "Gives AI agents
persistent long-term memory across sessions." Self-hosted; has an active
community (r/AIMemory, plugins). No dedicated arXiv paper as of mid-2026 — it's a
tool/platform, not a paper (related concept work: "Distilling Feedback into
Memory-as-a-Tool", arXiv:2601.05960, is adjacent but not Cognee's own).

## Mechanism

- **ECL pipeline — Extract, Cognify, Load:** ingest data in any format → build a
  **knowledge graph + vector store** ("cognify") → load it so agents recall,
  connect, and act with full context.
- Combines graph + vector retrieval (hybrid, pull-based); integrations with
  OpenSearch/Haystack and others in the community.

## Why it matters to us

The sixth tool in Van Horn's pull-memory map (gbrain / supermemory / mem0 /
Letta / Zep / Cognee). Graph+vector hybrid puts it near Zep and gbrain in
approach. Lighter on the eviction/temporal story than Zep, so a useful contrast:
strong on *building* the graph, less explicit on *forgetting*. Related: `zep`,
`cognee` vs `gbrain` (graph approaches), `mem0`.
