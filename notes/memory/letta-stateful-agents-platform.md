---
title: "Letta (formerly MemGPT) — platform for stateful agents"
authors:
  - Letta team (Charles Packer, Sarah Wooders, et al.)
source: "GitHub / docs"
repo: "https://github.com/letta-ai/letta"
related_paper: "https://arxiv.org/abs/2310.08560"
project: "memory"
scope_note: "context include — tool (productizes MemGPT)"
agent_setting: "stateful agents with self-editing memory, run via API or local CLI"
memory_mechanism: "OS-inspired memory hierarchy: a small in-context 'core memory' the agent edits itself, plus larger out-of-context archival/recall memory paged in on demand via tools."
icl_relevance: "high"
tags:
  - agent-memory
  - stateful-agents
  - self-editing-memory
  - context-management
  - tool
categories:
  - consolidation
  - retrieval
---

# Letta — the productized MemGPT

`github.com/letta-ai/letta` (Python, Apache-2.0, ~23.5k★). The commercial/OSS
platform built by the **MemGPT** authors (see
`memgpt-towards-llms-as-operating-systems.md` for the paper). "Build AI with
advanced memory that can learn and self-improve over time."

## Mechanism

Letta operationalizes the MemGPT "LLM-as-OS" idea:

- **Core memory** — a small, always-in-context block (persona + key user facts)
  that the agent **edits itself** with tools. This is the always-loaded layer.
- **Archival / recall memory** — larger out-of-context stores the agent **pages
  in on demand** (pull memory), so history doesn't bloat the window.
- Model-agnostic; ships **Letta Code** (a terminal agent CLI), a full agents
  API, Python/TS SDKs, skills, and subagents. Notably authored the **Context
  Constitution** that smolpaws' dreaming protocol is adapted from.

## Why it matters to us

Letta is the most direct intellectual lineage for smolpaws/dreamem: the
core-vs-archival split is exactly the push-vs-pull distinction (small always-on
memory + queryable store), and their Context Constitution is the source of our
"index don't copy / cache-friendly ordering / learning generalizes" principles.
Main competitor on agent memory and a north star for the self-editing-memory
design. Related: `memgpt`, `mylm`, `zep`, `mem0`.
