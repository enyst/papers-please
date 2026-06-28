---
title: "GBrain — Garry Tan's opinionated OpenClaw/Hermes agent brain"
authors:
  - Garry Tan
source: "GitHub"
repo: "https://github.com/garrytan/gbrain"
evals_repo: "https://github.com/garrytan/gbrain-evals"
project: "memory"
scope_note: "context include — tool"
agent_setting: "personal/company brain daemon for OpenClaw/Hermes agents"
memory_mechanism: "Markdown-and-git knowledge base with vector + keyword + self-wiring knowledge-graph retrieval, a synthesis-with-gap-analysis layer, and a 24/7 'dream cycle' daemon that ingests, enriches, and consolidates overnight."
icl_relevance: "high"
tags:
  - agent-memory
  - knowledge-graph
  - synthesis
  - consolidation
  - dreaming
  - company-brain
  - tool
categories:
  - retrieval
  - consolidation
  - knowledge-graph
---

# GBrain — markdown-and-git brain with a dream cycle

`github.com/garrytan/gbrain` (TypeScript, MIT, ~24k★). Built by Garry Tan (YC
president/CEO) to run his own OpenClaw/Hermes agents; pitched as a "company brain"
matching YC's company-brain RFS. Evals live in the sibling `gbrain-evals` repo.

## Mechanism

Two things most personal-knowledge tools don't ship together:

1. **Synthesis + gap analysis, not chunks.** Queries return a *synthesized,
   cited answer* across people/companies/deals/ideas, plus an explicit note on
   *what the brain doesn't know yet* — the gap analysis is the differentiator.
2. **Self-wiring knowledge graph.** Every page write extracts entity refs and
   creates typed edges (`attended`, `works_at`, `invested_in`, `founded`) with
   **zero LLM calls**, enabling relational queries vector search can't reach.
   Benchmarked P@5 49.1 / R@5 97.9, +31.4 P@5 over its graph-disabled variant.
3. **24/7 "dream cycle" daemon** — ingests meetings/emails/tweets/calls, enriches
   every person/company, fixes its own citations, and **consolidates memory
   overnight**. Runs on your hardware/DB/keys. Per-user scoping with fuzz-tested
   read isolation.

## Why it matters to us

The single closest external system to smolpaws + dreamem: it literally has a
nightly **consolidation ("dream") cycle**, and it's from a very visible builder.
Two things it has that our flat-file memory doesn't: a **zero-LLM typed-edge
graph** and a **synthesis-with-gap-analysis** retrieval layer — both worth
stealing. Strongest "dreaming daemon" prior art for dreamem's competitive
landscape, and directly in our OpenClaw/Hermes family. Cited by Matt Van Horn as
the pull-memory layer he runs inside Hermes. Related: `zep`, `cognee`,
`supermemory`, `letta`; blog note `using-local-coding-agents` (OpenClaw/Hermes).
