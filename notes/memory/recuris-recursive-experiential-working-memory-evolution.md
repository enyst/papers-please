---
title: "Recuris: Recursive Experiential-Working Memory Evolution for Long-Horizon Agent Harnesses"
authors:
  - Zhaochen Yu
  - Yingcheng Wu
  - Zhenfei Yin
  - Kaiyuan Chen
  - Zhe Zhao
  - Mengdi Wang
  - Shuicheng Yan
  - Ling Yang
arxiv_id: "2608.24876"
arxiv_url: "https://arxiv.org/abs/2608.24876"
published: "2026-08-27"
source: "arXiv"
project: "memory"
scope_note: "post-cutoff targeted addition (requested 2026-08-30 via @dair_ai top-papers list)"
agent_setting: "long-horizon agent harnesses doing recursive self-improvement (RSI)"
memory_mechanism: "Two-part memory: Working Memory tracks task progress and grounds skill selection from Experiential (Skill) Memory in current state, not full history. Execution becomes structured evidence that localizes failures to a specific memory component; a fixed Meta-Agent turns that into validation-gated updates to Skill Memory — a bounded recursive memory-evolution loop."
icl_relevance: "high"
tags:
  - agent-memory
  - working-memory
  - experiential-memory
  - skill-evolution
  - recursive-self-improvement
  - long-horizon
  - validation-gated
categories:
  - cs.AI
  - cs.CL
---

# Recuris: Recursive Experiential-Working Memory Evolution

**Paper:** [arXiv:2608.24876](https://arxiv.org/abs/2608.24876) · **Authors:** Zhaochen Yu, Yingcheng Wu, Zhenfei Yin, Kaiyuan Chen, Zhe Zhao, Mengdi Wang, Shuicheng Yan, Ling Yang · **Date:** 2026-08-27
**Flagged by:** @dair_ai top-papers-of-the-week (#8).

## One-Line Summary

Split agent memory in two: a **Working Memory** that tracks *current task progress* and a **Experiential (Skill) Memory** that holds skills — so skill selection is grounded in the current task state, **not the full growing history**. Because skill use is anchored to explicit state, a failed run points at a *specific* memory component, and a fixed **Meta-Agent** turns that evidence into **validation-gated** updates to Skill Memory. A bounded recursive self-improvement loop.

## The Mechanism

Recursive self-improvement (RSI) is hard on long-horizon tasks because growing histories obscure the task state and misalign skill invocation. Recuris addresses both:
1. **Working Memory** tracks task progress and **guides skill selection** from Experiential Memory based on *current needs* — decoupling "what skill do I need now" from "everything that has happened."
2. **Execution → structured evidence.** Because skill use is anchored to an explicit state, when a run fails the failure **localizes to a specific memory component** (bad skill vs. bad state-tracking vs. bad selection) instead of a vague "the agent messed up."
3. **Meta-Agent (fixed) closes the loop.** It converts that localized evidence into **validation-gated** updates to Skill Memory, which reshape execution and yield new evidence → bounded recursive memory-evolution loop.

## Key Results

Four long-horizon benchmarks × ten models. Improves task success in **35 of 37** completed model-benchmark pairs. Carries frontier models to SOTA-level:
- **τ-bench:** +17.8 to GPT-5.6 Sol, +15.6 to Claude Opus 5 (→ **87.9%**).
- **SkillFlow:** +16.6 / +13.5 to Qwen3.6-27B / 35B.
- **Advantage widens with horizon** — up to **+32.2 points** on the longest tasks; common long-horizon failures fall by **up to 80%**. Code released.

## Why It Matters To Us (SmolPaws)

- **Yes, it's memory — and squarely in our family.** It's the *architecture* complement to WikiSkill: WikiSkill separates raw/wiki/skills for offline *evolution*; Recuris separates working/experiential memory for *online selection + failure localization*, then still does validation-gated skill updates. Together they cover "evolve the skills" and "pick the right skill now, and know which one broke."
- **"Ground skill selection in current state, not full history"** is a direct answer to a real SmolPaws problem: as skills grow, retrieval/triggering degrades (the exact gap WikiSkill flagged as out-of-scope). Recuris tackles it via an explicit working-memory state.
- **Failure localization to a memory component** is the sharpest idea for us: when a heartbeat/skill run goes wrong, being able to say *which* memory piece caused it (stale fact vs. wrong skill vs. bad progress-tracking) is exactly what our dreaming/debugging lacks.
- **Validation-gated updates** — same discipline as WikiSkill's gating and SKILL.state's runtime validation: never accept a self-edit that doesn't pass a check. Reinforces the pattern across the whole batch.

## Where It's Thin / Skeptic's Notes

- **Working/Experiential split adds moving parts** — two memory stores + a Meta-Agent to maintain; more to get wrong than a flat memory.
- **"Fixed Meta-Agent" is load-bearing** — the quality of self-improvement depends on that fixed component's judgment; the paper doesn't (from the abstract) stress-test a bad Meta-Agent.
- **Benchmark-driven** (τ-bench, SkillFlow) — strong, but these are structured long-horizon suites; open-ended real work may localize failures less cleanly.

## Related

- `wikiskill-compiling-agent-experience-into-persistent-knowledge-for-skill-evolution.md` — offline skill evolution; Recuris is the online-selection + failure-localization complement.
- `context-as-an-environment-scroll-programmatic-context-management.md`, `../harness/skill-state-scalable-long-horizon-agent-skills.md` — "explicit state, not full history" family.
- `../agentic-engineering/` — skills-from-traces + validation-gated self-improvement convergence.
