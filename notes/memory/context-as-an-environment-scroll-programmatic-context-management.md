---
title: "Context as an Environment: Programmatic Context Management for Long-Horizon Agents (Scroll)"
authors:
  - Yin Lin
  - Elaine Ang
  - Erkang Zhu
  - Bolin Ding
  - Jingren Zhou
arxiv_id: "2608.21690"
arxiv_url: "https://arxiv.org/abs/2608.21690"
published: "2026-08-21"
source: "arXiv"
affiliation: "Alibaba"
project: "memory"
scope_note: "post-cutoff targeted addition (requested 2026-08-30 via @dair_ai top-papers list)"
agent_setting: "long-horizon LLM agents whose history exceeds the context window"
memory_mechanism: "Session = executable environment: append-only Event Log + persistent sandboxed Python kernel with a typed namespace. Model writes code to search/transform state; only printed projections enter the prompt. Eviction changes only the working view; evicted spans stay verbatim in the log, reachable via an address-anchored eviction index."
icl_relevance: "high"
tags:
  - agent-memory
  - context-management
  - programmatic-context
  - event-log
  - long-horizon
  - code-as-action
categories:
  - cs.AI
---

# Context as an Environment: Programmatic Context Management (Scroll)

**Paper:** [arXiv:2608.21690](https://arxiv.org/abs/2608.21690) · **Authors:** Yin Lin, Elaine Ang, Erkang Zhu, Bolin Ding, Jingren Zhou (**Alibaba**) · **Date:** 2026-08-21
**Flagged by:** @dair_ai top-papers-of-the-week (#3).

## One-Line Summary

Stop serializing an agent's history into the prompt and stop committing to a memory schema up front. **Scroll** treats each session as an **executable Session Environment**: an append-only Event Log + a persistent Python kernel with a typed namespace. The model **writes code** to search/transform its own state, and **only what it explicitly `print`s enters the working view**. Nothing is compressed before you know what matters.

## The Method

- **State lives outside the prompt.** An **append-only Event Log** preserves the full trajectory with stable addresses + provenance (lossless ground truth). A **sandboxed, persistent Python kernel** survives across model calls and holds a **typed namespace** — tool outputs, retrieved history, derived state bind to variables instead of being re-serialized each turn.
- **Context management becomes programming.** The model issues `exec` actions to search/expand the log, invoke tools, and compute over resident variables — something current models are already good at. Retrieved records + intermediate results stay in the kernel **unless explicitly emitted via `print`**; only those projections cross into the model's working view.
- **Eviction is recoverable, not destructive.** When the working view nears budget, stale spans are evicted **from the view only** — they remain verbatim in the Event Log under stable addresses. An **eviction index** keeps compact address-anchored landmarks so the agent navigates back to a region instead of re-scanning the whole log. (Contrast with compaction, which mutates the record — see the Compaction Cliff paper.)

## Key Results

With Qwen3.8-Max: **94.8% LongMemEval_S**, **73.1% BEAM_10M (+5.1 over best published memory system)**, **86.7% LOCA_256K**. Because context management runs *as code*, it inherits future gains in model coding ability for free.

## Why It Matters To Us (SmolPaws / OpenHands)

- **Third member of a clear family, and the most "prompt-hygiene" one.** SKILL.state (bounded explicit state), WikiSkill (persistent wiki), Scroll (event-log-as-environment). All say: **the history should not live in the prompt.** Scroll's twist — *only printed projections enter context* — is a clean rule we could adopt for long SmolPaws sessions.
- **Avoids the Compaction Cliff by construction.** Nothing lossy happens to the record; only the *view* shrinks, reversibly. That's the structural answer to "compaction destroys safety rules."
- **Code-as-context-management fits OpenHands' strengths.** We already have a real Python/bash runtime; letting the model program its own retrieval over an event log is very much in the "code-as-harness" spirit (`../harness/`).
- **"Don't commit to a schema before you know future needs"** directly answers the memory-design pain — same instinct as our "index, don't copy," but with lossless ground truth underneath.

## Where It's Thin / Skeptic's Notes

- **Puts more load on the model to write good retrieval code** — weaker models may flail at programmatic context management (the paper leans on Qwen3.8-Max).
- **A persistent kernel per session is real infra** (state, sandboxing, lifecycle) — heavier than a flat transcript; worth it for long-horizon, overkill for short tasks.
- **Benchmarks are memory-recall suites** (LongMemEval/BEAM/LOCA); strong there, but that's not the same as end-to-end task success under adversarial/noisy tools.

## Related

- `../harness/skill-state-scalable-long-horizon-agent-skills.md` — explicit-state runtime; sibling "history-out-of-prompt" idea.
- `wikiskill-compiling-agent-experience-into-persistent-knowledge-for-skill-evolution.md` — immutable raw + consolidated layer.
- `the-compaction-cliff-in-long-running-ai-agent-memory.md` — the failure mode Scroll sidesteps.
