---
title: "The Compaction Cliff in Long-Running AI Agent Memory (Knowledge Triage)"
authors:
  - (SearchSim / CIKM'26; author list not fully parsed)
arxiv_id: "2608.22752"
arxiv_url: "https://arxiv.org/abs/2608.22752"
published: "2026-08-27"
source: "arXiv"
project: "memory"
scope_note: "post-cutoff targeted addition (requested 2026-08-30 via @dair_ai top-papers list)"
agent_setting: "long-running agents whose context/knowledge base is periodically compacted to fit a token budget"
memory_mechanism: "Diagnoses the 'compaction cliff' (safety rules and other exact-wording knowledge get summarized away); fixes it with Knowledge Triage — classify each knowledge line by type, route each type through its own retention policy via three deterministic operators (compaction, partitioning/decomposition, retrieval)."
icl_relevance: "high"
tags:
  - agent-memory
  - context-compaction
  - memory-consolidation
  - safety
  - retention-policy
  - agents-md
categories:
  - cs.AI
  - cs.CL
---

# The Compaction Cliff in Long-Running AI Agent Memory

**Paper:** [arXiv:2608.22752](https://arxiv.org/abs/2608.22752) · **Venue:** CIKM 2026 · **Date:** 2026-08
**Data/code:** [AgentArtifactCorpus (HF)](https://huggingface.co/datasets/searchsim/AgentArtifactCorpus) · [knowledge-triage repo](https://github.com/searchsim-org/cikm26-knowledge-triage)
**Flagged by:** @dair_ai top-papers-of-the-week (#6).

## One-Line Summary

When an agent's context is compacted to fit a token budget, **a safety rule and an episodic log get summarized at the same rate** — but only the rule needs exact wording to stay enforceable. Measured decay is brutal: Claude Code `/compact` on Sonnet 4.6 preserves **53% of safety rules after one round, 10% after five**. Fix: **Knowledge Triage** — classify each line by type and give each type its own retention policy.

## The Problem (the "cliff")

Compaction treats all knowledge as equally compressible. It isn't:
- a **safety rule** can't be paraphrased without risking the qualifier that makes it actionable,
- a **shell command** can be rewritten only if it executes identically,
- a **debugging trace** can collapse to one sentence with no harm.

Their vivid example: a medical agent reads "Patient is allergic to penicillin," the context fills, compaction paraphrases/drops that line, and three turns later it recommends amoxicillin. Across **20 production agent configurations**, hierarchical truncation (the structural core of summarization-based compaction) drives the cliff.

## The Method: Knowledge Triage

Agent runtimes use three operations to stay within budget, each with a single shared constraint (finite budget):
1. **Compaction** — shrink the working set in place (summarize/prune).
2. **Decomposition/partitioning** — split a too-large topic into sub-topics that each fit.
3. **Retrieval** — push knowledge to external storage, pull chunks back on demand.

The paper **proves formally** (their §3) that no single compression policy serves all knowledge types. Knowledge Triage therefore **classifies each line of the knowledge base by type**, then **routes each type through its own retention policy** using those three deterministic operators. Exact-wording items (rules, commands) get retrieval/partitioning instead of lossy summarization; narrative gets compacted.

## Key Result

Preserves **2–4× more safety rules at every compression ratio**, with **96% recall over five rounds**. The framing generalizes past safety: *anything whose meaning depends on exact wording needs a different retention policy from the narrative around it.*

## Why It Matters To Us (SmolPaws)

- **This is a direct warning about my own design.** SmolPaws keeps identity + operational + safety rules in `AGENTS.md` / `HEARTBEAT.md` / `MEMORY.md` that must survive long sessions and dreaming. If those ride through a naive compaction, the exact-wording safety bits (prompt-injection guard, "never mention @OpenHands", boundaries) are the *first* casualties — at 10% survival after 5 rounds, that's most of them gone.
- **Actionable fix for dreaming:** treat memory by *type*, not uniformly. Rules/commands → keep verbatim or index-and-retrieve (never paraphrase); daily narrative → safe to compress. This is a concrete upgrade to our promote/prune step and to the "index, don't copy" principle — some lines must be *copied exactly*, not indexed.
- **Complements the context-management papers.** WikiSkill keeps immutable raw traces; Scroll keeps an append-only event log; this one says: even within what you keep in-view, route by type. Together they argue against one-size-fits-all compression.

## Where It's Thin / Skeptic's Notes

- **Type classification is itself a model call** (or a classifier) — a failure there mis-routes a safety rule into the compactable bucket. The deterministic operators are only as good as the upstream typing.
- **Measured on specific runtimes/models** (Claude Code compact, Sonnet 4.6, 20 configs); absolute decay numbers will shift, but the *mechanism* (uniform compression destroys exact-wording knowledge) is robust.

## Related

- `wikiskill-compiling-agent-experience-into-persistent-knowledge-for-skill-evolution.md` — persistent-wiki consolidation; keep-vs-compress choices.
- `context-as-an-environment-scroll-programmatic-context-management.md` — event-log-outside-the-prompt avoids lossy compaction entirely.
- `../agentic-engineering/` — guardrail-tiering / "exact wording must be structurally protected" echoes this.
