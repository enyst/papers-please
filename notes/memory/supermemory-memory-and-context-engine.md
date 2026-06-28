---
title: "Supermemory — memory and context engine for AI"
authors:
  - Supermemory team (Dhravya Shah, et al.)
source: "GitHub / docs"
repo: "https://github.com/supermemoryai/supermemory"
project: "memory"
scope_note: "context include — tool"
agent_setting: "personal/company brain and per-app memory API for AI agents"
memory_mechanism: "Ingests conversations and connected sources, extracts facts, builds user profiles, reconciles contradictions, expires stale info, and serves the right context on demand (pull memory)."
icl_relevance: "high"
tags:
  - agent-memory
  - memory-api
  - contradiction-handling
  - forgetting
  - benchmarks
  - tool
categories:
  - retrieval
  - consolidation
---

# Supermemory — memory/context engine

`github.com/supermemoryai/supermemory` (TypeScript, MIT, ~27.7k★). "The memory
and context layer for AI" — usable as a personal or company brain. Self-hostable;
ships an SDK, an **MCP server**, and a local binary, with connectors into Drive,
Gmail, Notion, GitHub.

## Mechanism / claims

- Automatically **extracts facts** from conversations, **builds user profiles**,
  **handles knowledge updates and contradictions**, and **forgets expired
  information** — i.e. consolidation + eviction as a managed service.
- Full context stack in one system: RAG, connectors, file processing, over a
  single memory structure / ontology.
- **Benchmark posture:** claims #1 on the three major AI-memory benchmarks —
  **LongMemEval, LoCoMo, and ConvoMem**. Useful pointers for evaluating dreamem
  against a recognized suite rather than only our synthetic recall bench.

## Why it matters to us

A direct "pull memory" product in the field Van Horn maps (gbrain / supermemory /
mem0 / Letta / Zep / Cognee). The contradiction-reconciliation + expiry feature
set is exactly dreamem's promote/prune/restructure territory, productized. The
three named benchmarks (LongMemEval, LoCoMo, ConvoMem) are the most actionable
takeaway — candidate external evals for our work. Related: `mem0`, `zep`,
`letta`, `cognee`.
