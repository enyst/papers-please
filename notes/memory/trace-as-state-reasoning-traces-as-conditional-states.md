---
title: "Trace as State: Reasoning Traces as Conditional States for Long-Context Transformers"
authors:
  - Xu Zou
  - Jie Tang
arxiv_id: "2609.02702"
arxiv_url: "https://arxiv.org/abs/2609.02702"
published: "2026-09-02"
source: "arXiv"
project: "memory"
scope_note: "post-cutoff targeted addition (requested 2026-09-08 via @dair_ai top-papers list)"
agent_setting: "long-context reasoning where the task state is discovered only late in the context"
memory_mechanism: "Use the model's own reasoning trace as a textual proxy for task state, and place it BEFORE the long-context block on a fresh pass (not appended after), so already-derived information can guide re-reading. Training-free, no architecture change."
icl_relevance: "high"
tags:
  - context-management
  - long-context
  - reasoning-traces
  - prompt-ordering
  - training-free
categories:
  - cs.CL
---

# Trace as State: Reasoning Traces as Conditional States for Long-Context Transformers

**Paper:** [arXiv:2609.02702](https://arxiv.org/abs/2609.02702) · **Authors:** Xu Zou, Jie Tang (Tsinghua) · **Date:** 2026-09-02
**Flagged by:** @dair_ai top-papers-of-the-week (#8).

## One-Line Summary

**Where you put a reasoning trace changes long-context accuracy by up to ~50 points.** Transformers process causally, so a task state discovered *late* can't guide reading that already happened. Fix: collect the reasoning trace, then **place it *before* the long-context block on a fresh pass** (not appended after) — so information derived earlier steers the re-read. Training-free, no weights or architecture touched.

## The Mechanism

- **The asymmetry (formalized).** For a "conditional state update task" — start from a state given by a *condition*, then apply an information sequence — a causal processor that sees the **condition first** can update state as each item arrives. If the **condition arrives last**, it must retain *how the whole sequence would act on any state* — worst case **exponentially more memory**. Causal order matters.
- **The trick.** The model's own **reasoning trace** is a cheap textual proxy for "task state." On a second pass, prepend the trace **before** the long context (`Trace as State`), so the context is re-encoded *with* that state available.
- **The control.** `Trace Append` uses the *same* trace but places it *after* the context — it can guide later answer tokens but **cannot influence the representations already formed** for the preceding context. The whole result is that placement gap.

## Key Results

Three frontier models (DeepSeek V4 Pro Preview, GLM-5.2, Qwen 3.7 Max) × three long-context suites (GraphWalks 256K, MRCRv2 8-needle, NUB-1M). **Trace as State beats Trace Append in 26 of 27** model×task×metric combinations.
- **GraphWalks Parents:** DeepSeek 29.2% (initial) / 43.0% (append) → **81.8%** (as-state); GLM-5.2 66.4% / 83.2% → **100.0%**.
- The benefit is purely from **placement** — same trace text, different position.

## Why It Matters To Us (SmolPaws / OpenHands)

- **Cheapest possible context-engineering win, and it's an ordering rule.** No new system to adopt — it's "put the derived state *before* the raw context." Directly relevant to how we assemble prompts for long-repo / long-conversation work.
- **Sharpens the "history out of the prompt" family.** SKILL.state (bounded state), Scroll (event-log), WikiSkill (persistent wiki) all move history *out*. This adds an orthogonal, mechanistic point: even *within* one pass, **the order of state vs. raw context is causally load-bearing.** Our `MEMORY.md`/context-index sits at the top of context for cache reasons; this says it also matters for *reasoning*, because the model re-reads everything below it conditioned on it.
- **A cache-friendly-ordering cousin.** Our dreaming principle "put stable/consolidated content first" was justified by KV-cache; Trace-as-State gives a *second, independent* reason: putting the consolidated state first lets it condition the re-read. Two motivations, same layout.

## Where It's Thin / Skeptic's Notes

- **Two passes = extra compute.** It re-encodes the long context a second time with the trace prepended; that's not free (though cheaper than being wrong on a million-token task).
- **Needs a good trace to prepend.** The proxy is only as good as the reasoning trace collected on pass one; garbage state → garbage re-read.
- **Benchmarks are synthetic-ish long-context reasoning** (GraphWalks/MRCR/NUB); the "up to 50 points" is on the hardest state-tracking tasks, not every workload.

## Related

- `../harness/skill-state-scalable-long-horizon-agent-skills.md` — explicit state vs. history; sibling "state, not narration" idea.
- `context-as-an-environment-scroll-programmatic-context-management.md`, `wikiskill-compiling-agent-experience-into-persistent-knowledge-for-skill-evolution.md` — history-out-of-prompt family.
- `the-compaction-cliff-in-long-running-ai-agent-memory.md` — what to keep; this is where to *place* it.
