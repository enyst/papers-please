---
title: "memorywire: A Vendor-Neutral Wire Format for Agent Memory Operations"
authors:
  - Thamilvendhan Munirathinam
arxiv_id: "2606.01138"
arxiv_url: "https://arxiv.org/abs/2606.01138"
published: "2026-05-31"
updated: "2026-06-03"
source: "arXiv"
project: "memory"
scope_note: "pass-four include (Q2 2026 sweep)"
agent_setting: "interoperability across agent memory frameworks"
memory_mechanism: "Defines a vendor-neutral wire format for agent memory operations — read, write, search, consolidate — enabling framework interoperability."
icl_relevance: "medium"
tags:
  - agent-memory
  - standardization
  - interoperability
  - wire-format
categories:
  - cs.CR
  - cs.AI
  - cs.DC
---

- **One-line take:** The MIME type for agent memory — a standard wire format so frameworks can interoperate.
- **What it stores:** See memory_mechanism above.
- **How memory is used at inference time:** Defines a vendor-neutral wire format for agent memory operations — read, write, search, consolidate — enabling framework interoperability.
- **Why it matters for this sub-project:** An infrastructure play: if agent memory gets a standard format, it becomes composable across frameworks.
- **Caveats / limits:** Newly published (Q2 2026); peer validation pending.
- **Abstract-level summary:** Agent-memory frameworks -- mem0, Letta/MemGPT, Cognee, Zep/Graphiti, MemoryOS, MemTensor -- each ship their own SDK, storage layout, and operational vocabulary. There is no shared wire format: every integration is bespoke, every migration rebuilds memory from scratch, and no framework ships a governance surface that lets a human review writes before they enter long-term storage. We present memorywire, a JSON-Schema 2020-12 wire format for five memory operations (remember, recall, forget, merge, expire) over four memory types (semantic, episodic, procedural, emotional), with a MemoryStore interface, a fan-out router, and an optional HITL governance channel. We describe an open-source reference implementation with five backend adapters (sqlite-vec, mem0, Letta, Cognee, pgvector); a microbenchmark on a 100-fact / 50-query labelled corpus (42 with non-empty gold ids + 8 no-match probes) achieving recall@5 = 1.000 on the 42 gold-id queries with ingest p50 = 37.8 ms and recall p50 = 40.6 ms; an adversarial-fusion experiment showing Reciprocal Rank Fusion holds recall@5 = 1.000 across a 1-of-N rank-0 injection sweep (K in {0, 5, ..., 50}) where max fusion collapses to 0.500 with 80% leak at K >= 5; and a 16-scenario cross-adapter conformance suite passing 68 of 80 cells with zero failures. The contribution is not a new algorithm; it is a packaging of established components (RRF, FSMs, STM/LTM consolidation, diff-and-approve workflows) into a venue-neutral protocol with an empirically validated reference, positioned to compose with the Model Context Protocol rather than compete with it.
