# SKILL.state: Scalable Long-Horizon Agent Skills

**Paper:** [arXiv:2608.26263](https://arxiv.org/abs/2608.26263)
**Authors:** Sanket Badhe, Priyanka Tiwari, Jonghyun Chung
**Date:** 2026-08-26
**Subjects:** cs.AI; cs.MA
**Type:** Runtime architecture + benchmark

## One-Line Summary

Replace the agent's **append-only conversation history** with an **explicit, mutable execution state**. At each step the model sees only three things — the immutable skill spec, the current structured state, and the latest observation — and its intermediate reasoning is **discarded immediately** after producing a validated state update. Prompt size stays flat; token cost drops enormously; long-horizon reliability goes up.

## The Problem

Modern agent runtimes are conversational: every step re-sends the original skill spec plus an ever-growing transcript of past reasoning, actions, observations, tool outputs. Two failure modes over long horizons:
1. **Prompt grows with execution length** → rising latency and token cost (quadratic cumulative cost, O(n²) over horizon n).
2. **Context poisoning** → obsolete observations and stale reasoning stay embedded in context long after they're irrelevant; the model must continually reconstruct "current facts" from historical text, and old facts can overpower new contradictory observations.

Memory systems (summarization/retrieval) reduce growth but **preserve the same execution semantics** — decisions still condition on textual reconstructions of the past rather than an explicit current state.

## The Method

Reformulate procedural skill execution as **explicit state transitions**. At step *t*, the model receives only:
- **σ** — immutable procedural skill specification
- **Sₜ** — structured execution state (a domain schema, JSON-like)
- **oₜ** — latest environment observation

It never sees previous observations, actions, or reasoning. Each step:
1. Model generates a full multi-step **Chain-of-Thought** (intact *during* generation for real deductive planning), a **structured state update** (JSON dict of key mutations/deletions), and the **action**.
2. Runtime **deterministically validates** the proposed state transition, applies it, executes the action.
3. **The reasoning trace is discarded permanently** — never appears in later prompts.

Key design points:
- **Schema authored once per domain, not per task.** E.g. all 100 InterCode CTF instances reuse one static 5-field schema (`discovered_flags`, `tested_hypotheses`, `active_files`, `working_dir`, `cmd_summary`).
- **Schema ownership + validation live in the deterministic runtime, not the model.** A malformed patch can't corrupt persistent state — it triggers rollback-retry. (For small open-weight models, grammar-constrained decoding can eliminate syntactic errors.)
- **Complexity:** conversational runtimes are O(n²) cumulative tokens over horizon n; SKILL.state keeps per-step prompt bounded/constant, so cumulative cost grows **strictly linearly** with the horizon.

## Key Results

Models: Gemini-3-Flash, Gemma-4-31B, Qwen-3-8B (temp 0 for reproducibility). Benchmarks: **SkillExecBench** (their controlled testbed), **InterCode CTF**, **Sierra τ-Bench** (Retail + Airline).

- **Long-horizon scaling (SkillExecBench Warehouse, 500 shelves):** SKILL.state holds flat prompt size (~1.7k–1.9k tokens) and matches/exceeds accuracy across horizons. At one horizon the **Stateful baseline uses 1,062,387 tokens vs SKILL.state's 65,408** (~16× reduction); at a longer horizon it keeps **0.94 accuracy at 122k tokens while the Memory baseline balloons to 6.1M**.
- **Noise robustness (Exp 2):** with 5–50 distractor events/turn injected, the standard Prompt runtime degrades 0.68 → 0.53; SKILL.state stays robust (~unchanged) because distractors are filtered during state-patch generation and never enter later prompts.
- **State recovery (Exp 3):** history-based baselines hallucinate for **5–8 consecutive turns** after a corrective alert (obsolete prompt facts overpower new observations); SKILL.state needs **zero recovery steps** — state updates immediately.
- **Public benchmarks (Exp 4):** InterCode CTF pass@1 **54.2% (+7.8 over strongest baseline, +12.4 over Stateful), −60.4% tokens vs ReAct, −65.9% vs Stateful**; τ-Bench Retail 58.3% at lowest token cost.
- **Budget-matched controls (Exp 5):** compression baselines pinned to SKILL.state's ~1,800-token budget collapse — sliding-window 0.18 (evicts early inventory), LLMLingua 0.22 (entropy filtering removes semantically vital slot IDs) — vs SKILL.state's **0.94**. The gain is from *structured state*, not merely shorter prompts.
- **Error taxonomy (open-weight):** e.g. **premature state overwrite/deletion (68%)** — model omits existing keys during update instead of merging in-place. Motivates in-place-merge patch semantics + constrained decoding.

## Why It Matters To Us (SmolPaws / OpenHands)

- **A concrete answer to context-window discipline.** This is the strongest form of "don't re-send history": maintain an explicit world-state, feed only spec + state + latest observation. Directly relevant to OpenHands' long agent loops and to SmolPaws' context budgeting.
- **The runtime, not the model, owns state validity.** Deterministic validation + rollback-retry is a hard-boundary pattern — malformed model output cannot corrupt persistent state. Echoes the guardrail-tiering thread (`notes/agentic-engineering/two-camps-synthesis-vitor-balocco.md`): put the strong deterministic rail in the runtime.
- **Complements WikiSkill, doesn't compete.** WikiSkill (`notes/memory/wikiskill-…`) is about *evolving* the skill spec across runs (persistent knowledge). SKILL.state is about *executing* a fixed skill spec within a run (bounded state). One improves the spec offline; the other runs it cheaply online — they compose.
- **"Discard reasoning after it's used" is a sharp memory principle.** Within-step CoT is kept for planning, then thrown away — reasoning is computation, not memory. A cleaner rule than summarize-everything.
- **Schema-once-per-domain** maps onto the skill/outer-harness idea: a small stable structured state definition beats per-task prompt engineering.

## Where It's Thin / Skeptic's Notes

- **Works best for well-structured procedural skills** with a definable state schema (warehouse slots, CTF flags, DB workflows). Open-ended or exploratory tasks where the relevant state is unknown up front are a poorer fit — you must anticipate the schema.
- **Pushes burden onto the model to emit valid patches**, and open-weight models fail here (68% premature-overwrite). Needs constrained decoding / careful patch semantics to be reliable off-frontier.
- **"Discard all intermediate reasoning" risks losing genuinely reusable insight** across steps if the schema under-captures it — the schema *is* the memory, so a bad schema silently drops signal. (Contrast WikiSkill, which keeps immutable raw traces precisely so nothing is lost.)
- **Benchmarks include a self-authored one (SkillExecBench).** Public results (CTF, τ-Bench) are the load-bearing evidence; weight those.

## Related

- `code-as-agent-harness.md`, `harness-handbook.md` — same "harness = what makes an agent operational" lens; this is a concrete harness-runtime design.
- `../memory/wikiskill-compiling-agent-experience-into-persistent-knowledge-for-skill-evolution.md` — offline skill *evolution* vs. this online skill *execution*; the immutable-raw vs discard-reasoning contrast is instructive.
- `../memory/` — context-management / long-horizon memory architectures (the paper's own §2.2, §2.4).
- `../agentic-engineering/` — deterministic-rail-in-the-runtime echoes the guardrail-tier thread.
