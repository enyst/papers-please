---
title: "Selective Forgetting: A Graph-Based Memory Framework for Long-Term LLM Agents"
authors:
  - Theo Rusu
  - Sourena Khanzadeh
  - Manar Alalfi
arxiv_id: "2608.28978"
arxiv_url: "https://arxiv.org/abs/2608.28978"
published: "2026-08-29"
source: "arXiv"
project: "memory"
scope_note: "post-cutoff targeted addition (requested 2026-09-08 via @dair_ai top-papers list)"
agent_setting: "long-term conversational agent memory; graph vs. flat retrieval, with periodic pruning"
memory_mechanism: "Extract each turn into typed nodes + attributed edges, answer from a two-hop subgraph, and periodically prune nodes scored on recency + access frequency + degree centrality + age. Directly tests whether graph memory beats flat vector retrieval at matched budget."
icl_relevance: "high"
tags:
  - agent-memory
  - graph-memory
  - forgetting
  - memory-pruning
  - retrieval
  - myth-busting
  - longmemeval
categories:
  - cs.AI
---

# Selective Forgetting: A Graph-Based Memory Framework for Long-Term LLM Agents

**Paper:** [arXiv:2608.28978](https://arxiv.org/abs/2608.28978) · **Authors:** Theo Rusu, Sourena Khanzadeh, Manar Alalfi · **Date:** 2026-08-29
**Flagged by:** @dair_ai top-papers-of-the-week (#9).

## One-Line Summary

Tests the popular assumption that **graph memory beats flat retrieval** for long-term agents — and, at a *matched* retrieval budget, **it doesn't**: on LongMemEval the knowledge graph scores **token F1 0.417 vs 0.468** for a flat vector baseline (paired bootstrap Δ = −0.050, 95% CI [−0.085, −0.016]). The **forgetting** half, though, works: prune ~10% of a 27k-node graph with F1 essentially unchanged.

## The Setup (why the comparison is fair)

- Extract each conversational turn into **typed nodes + attributed edges**; answer questions from a **two-hop subgraph**.
- **Periodic pruning** ("selective forgetting"): score each node on a weighted combination of **recency + access frequency + degree centrality + age**, drop the low scorers.
- **Matched candidate-generation budget** — both graph and flat baseline get **five retrieval roots**. This is the honest bit: the comparison isn't rigged by giving the graph more retrieval.

## Key Findings

- **Graph loses at matched budget.** Token F1 **0.417 (graph) vs 0.468 (flat vector)**; Δ = −0.050, CI [−0.085, −0.016] over 500 questions.
- **Where it loses worst:** questions needing a **specific prior *assistant* turn** — judged correctness **0.911 → 0.607**. Diagnosis: **decomposing a turn into entities discards the surface form** those questions depend on. (Structure throws away the literal wording you sometimes need.)
- **Forgetting works.** One pass on a persistent **27,021-node** graph removes **9.8% of nodes / 9.5% of bytes**; token F1 change **+0.001** (CI [−0.015, +0.016]), judged correctness −1.6 pts (worst-case bound −3.8). So you *can* shrink memory materially with negligible quality loss.
- **Authors' own caveat (rare and honest):** "a single small extractor, one benchmark — this characterises *this extraction-based pipeline*, not graph-structured memory in general."

## Why It Matters To Us (SmolPaws)

- **Myth-busting is exactly what a memory corpus needs.** Graph memory is fashionable; this is a *controlled* result saying it can be *worse* than plain vectors when you don't hand it extra retrieval. Counterweight to the many pro-graph papers in `notes/memory/`.
- **"Structure discards surface form" is a real design warning.** For SmolPaws, some things must be kept **verbatim** (the exact wording of a prior turn, a rule, a command) — the same lesson as the Compaction Cliff paper. Entity-decomposition is lossy for recall-the-exact-turn queries. Don't over-structure memory that will be needed literally.
- **The forgetting module is directly reusable for dreaming.** A cheap, principled prune (recency + frequency + centrality + age) that removes ~10% with no measurable quality loss is a concrete algorithm our nightly consolidation could borrow — pruning that's *validated* not to hurt.
- **Matched-budget discipline.** The paper's method — hold retrieval budget fixed before comparing memory designs — is the right way to evaluate any memory change we make.

## Where It's Thin / Skeptic's Notes

- **Single small extractor, one benchmark** — the authors say so. This is evidence against *this pipeline*, not a general proof that graphs lose. A stronger extractor might narrow or flip the gap.
- **LongMemEval-specific.** The "recall a specific assistant turn" weakness is real but benchmark-shaped; different task mixes weight surface-form vs. relational recall differently.
- **It's a modest negative result**, not a new SOTA — its value is the *controlled comparison* + the forgetting algorithm, not headline numbers.

## Related

- `the-compaction-cliff-in-long-running-ai-agent-memory.md` — "exact wording matters"; both warn against lossy restructuring of recall-critical content.
- `wikiskill-...md`, `recuris-...md` — consolidation/curation; this adds a *validated pruning* method and a graph-skeptic data point.
- Other graph-memory notes in this dir (GAAMA, Mnemis, graph-memory taxonomy) — read against this as the skeptical control.
