---
title: "WikiSkill: Compiling Agent Experience into Persistent Knowledge for Skill Evolution"
authors:
  - Liyan Tang
  - Cyrus Rashtchian
  - Chun-Sung Ferng
  - Andrew Tomkins
  - Da-Cheng Juan
  - Tu Vu
arxiv_id: "2608.27454"
arxiv_url: "https://arxiv.org/abs/2608.27454"
published: "2026-08-27"
updated: "2026-08-27"
source: "arXiv"
project: "memory"
scope_note: "post-cutoff targeted addition (requested 2026-08-29 via @dair_ai)"
affiliation: "Google"
agent_setting: "skill-evolving LLM agents that iteratively refine a reusable skill library from training rollouts"
memory_mechanism: "Three-layer workspace (immutable raw traces / persistent structured wiki / evolving executable skills). A Wiki Maintainer consolidates traces into the wiki; a Skill Proposer edits skills using the wiki; validation gating rolls back skills but never the wiki, so knowledge compounds across iterations."
icl_relevance: "high"
tags:
  - agent-memory
  - memory-consolidation
  - skill-evolution
  - self-improvement
  - persistent-knowledge
  - skill-transfer
  - agent-skills
categories:
  - cs.CL
  - cs.AI
---

# WikiSkill: Compiling Agent Experience into Persistent Knowledge for Skill Evolution

**Paper:** [arXiv:2608.27454](https://arxiv.org/abs/2608.27454) · **Authors:** Liyan Tang, Cyrus Rashtchian, Chun-Sung Ferng, Andrew Tomkins, Da-Cheng Juan, Tu Vu (**Google**) · **Date:** 2026-08-27
**Flagged by:** [@dair_ai](https://x.com/dair_ai/status/2093324233158045788) ("banger paper... if you maintain a skill library for your agents").

## One-Line Summary

Skill-evolution systems usually collapse three things into one blob; WikiSkill **separates them** — raw execution traces, a persistent **wiki** of accumulated knowledge, and the executable **skills** — and consolidates experience into the wiki so every later skill update builds on structured knowledge instead of a scattered optimization history. Ablations show **the wiki carries most of the gain.**

## The Core Idea: a Three-Layer Workspace

Prior skill-evolution work (EvoSkill, Trace2Skill, SkillOpt) keeps "what was learned" scattered across optimization history — cumulative proposal logs, per-trajectory lessons, rejected-edit feedback — but never as a **separate, evolving knowledge representation**. WikiSkill makes that representation first-class, organizing the agent workspace into three layers:

| Layer | Path | What | Mutability |
|---|---|---|---|
| **Raw** | `raw/` | Full step-by-step execution traces (reasoning, tool calls, outputs, answers) from each iteration's rollouts. | **Immutable** |
| **Wiki** | `wiki/` | Structured, compounding knowledge — a `patterns/` directory of markdown pages documenting specific failure modes / effective strategies, plus evolution logs. | Persistent, continuously updated |
| **Skills** | `skills/` | Evolving executable procedural knowledge (`SKILL.md` files) injected into the agent. | Versioned; rolled back on regression |

## The Loop (four components per iteration)

State is the tuple **(active skills, wiki)**. Each iteration:

1. **Inference Agent** — runs rollouts on training tasks using current `skills/`, producing immutable traces in `raw/`. **Crucially, it is *denied* wiki access during rollouts** (ablation shows wiki access here *hurts* — the agent solves from the wiki instead of the skills, making traces less informative for skill development).
2. **Wiki Maintainer** — analyzes sampled traces (stratified: up to 5 failing for root-cause + 3 passing to protect working behavior; each log capped ~15k chars) against the existing wiki, and updates the persistent pattern catalog + evolution logs. One LLM call per batch.
3. **Skill Proposer** — an autonomous multi-turn **ReAct** agent that reads the wiki + traces and proposes skill edits.
4. **Gating & Rollback** — a candidate skill set is kept only if it improves the **validation** score; otherwise reverted to the last good config. **The wiki is *never* rolled back** — accumulated patterns/logs persist and compound regardless of whether a skill edit is accepted. (Early-stops if validation hits max.)

The asymmetry is the whole trick: **skills are gated and reversible; knowledge is permanent and compounding.**

## Key Results

Evaluated across **5 benchmarks** — LiveMathBench (math), SealQA (web search), SpreadsheetBench (spreadsheets), OfficeQA (long-context doc QA), ALFWorld (embodied) — and **5 models** across **Qwen / Gemma / Gemini** families. Scores averaged over 3 full pipeline runs with paired bootstrap significance testing.

- **Beats SOTA skill-evolution methods** and improves over no-skill baselines in most model-benchmark settings.
- **Skill evolution complements model scaling** — larger models generally gain *more* from evolved skills (e.g. one setting: +6.5 / +9.3 / +40.9 pts as model scale grows). But **smaller models with skills can beat substantially larger models without them** (Qwen-3.5-9B + WikiSkill 47.4% avg > larger Qwen-3.6-27B no-skill).
- **Skills transfer across models and families**, and **transferred skills sometimes beat self-evolved ones.** E.g. Qwen-3.6-27B SpreadSheet skills lift Qwen-3.5-9B to 50.5% vs 24.3% (no skill) / 33.6% (self-evolved). Transfer works **small→large** too (Qwen-3.5-4B skills lift Gemma-4-31B to 73.1% on LiveMath). One striking case: Qwen-3.5-4B's OfficeQA skills *hurt itself* (30.2%→28.5%) but *help* Qwen-3.6-27B (42.1%→52.9%).
- **Negative transfer exists too** — SpreadSheet skills show strong source-target interactions (Qwen-3.5-4B skills *drop* Gemini-3.5-Flash 50.5%→18.1%, while Qwen-3.6-27B skills lift it to 63.4%). So WikiSkill produces a mix of *general* procedural knowledge (transfers) and *model-specific* strategies (can backfire).

### The load-bearing ablation
With the Inference Agent's wiki access off, giving the **Skill Proposer** access to the persistent wiki raises avg performance **48.7% → 63.7% (+15.0)** — huge jumps on LiveMath (51.3→72.6) and SpreadsheetBench (49.9→76.6). Removing persistent accumulation cripples the proposer's ability to resolve intricate failure modes. Conversely, giving the *Inference Agent* wiki access during rollouts *drops* 63.7→60.9. **Persistent knowledge accumulation is confirmed as the critical ingredient — not the skill edits themselves.**

## Why It Matters To Us (SmolPaws / OpenHands)

- **This is our dreaming architecture, formalized and benchmarked.** SmolPaws already separates daily memory (≈ raw traces) → durable `MEMORY.md` (≈ wiki) and has skills on top. WikiSkill's result — *the persistent consolidated layer carries most of the gain, not the skill diffs* — is direct empirical support for prioritizing the dreaming/consolidation step over just editing skills.
- **"Never roll back the wiki" is a design rule we can adopt.** Even when a change to behavior/skills is reverted, the *learning about why it failed* should persist. Our dreaming should keep a compounding pattern log, not just promote/prune skill text.
- **Index, don't copy — with a twist.** The immutable `raw/` + structured `wiki/` split mirrors our context-index principle (pointer to source vs. consolidated fact). WikiSkill adds: consolidate into a *queryable pattern catalog*, and keep the raw immutable for re-analysis.
- **Skill transfer across model families is a big deal for a multi-model project.** Skills evolved on one model help others — sometimes more than self-evolved. Argues for treating a skill library as a portable asset, but the **negative-transfer** finding warns that some skills encode model-specific quirks; tag general vs. model-specific.
- **Deny the executor the knowledge base during data collection.** Non-obvious and counterintuitive: letting the working agent read the wiki *during* task execution degrades the traces used to improve skills. Relevant if we ever auto-generate skills from SmolPaws' own transcripts.

## Cross-source connection

Same mechanism the "agentic-engineering" dir keeps finding independently: **skills-from-your-own-traces** (Uber's auto-skill-generation, poteto's `/automate-me`+`/reflect`, our dreaming). WikiSkill is the *rigorous, ablated* version and adds the sharpest claim: it's the **persistent consolidated knowledge**, not the skill edits, that does the work. See `notes/agentic-engineering/README.md`.

## Where It's Thin / Skeptic's Notes

- **Retrieval is deliberately out of scope.** Skills are injected directly into the prompt to isolate skill *quality*; they don't evaluate retrieval/triggering, which the authors flag becomes critical as a library grows. Real deployments hit exactly that.
- **Strict gating drops "neutral" edits** — proposals that don't immediately help but could enable later gains are excluded. May under-explore.
- **Small validation splits** add gating noise (mitigated with 3 runs + bootstrap, but still).
- **Negative transfer is unsolved**, only diagnosed — no method yet to predict which skills are general vs. model-specific before they backfire.

## Related

- `notes/memory/auto-dreamer-learning-offline-memory-consolidation-for-language-agents.md` — offline consolidation policy; same "sleep-time compute" family.
- `notes/memory/agent-workflow-memory.md` — workflow-as-memory, a precursor idea.
- `notes/skills/` — skill discovery/optimization; WikiSkill's baselines (EvoSkill, Trace2Skill, SkillOpt) likely live/belong there.
- `notes/agentic-engineering/` — skills-from-traces convergence (Uber, poteto) and SmolPaws' dreaming.
