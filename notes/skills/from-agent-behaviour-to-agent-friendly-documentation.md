# From Agent Behaviour to Agent-Friendly Documentation: An Empirical Study of How Coding Agents Discover, Read, and Write Technical Documentation

**Paper:** [arXiv:2608.20195](https://arxiv.org/abs/2608.20195)
**Authors:** Zhijun Gao, Jing Chen
**Date:** August 2026

## One-Line Summary

Coding agents mostly read and write *agent-facing* docs (instruction files, working notes — 60.5% of all doc interactions), rarely consult classical technical docs or API references, don't validate against docs, and touch code *before* documentation — so the two assumed pillars of "agent-friendly" docs (actionability and verifiability) have no consistent behavioural support.

## Core Idea

Technical documentation is written for humans, but a growing share of code changes is now authored by autonomous agents. Nobody had measured *which* documents agents actually consult, *when*, and *what follows*. This is a behaviour-grounded study of real agent traces — not a benchmark of doc quality, but an empirical map of how agents actually interact with docs.

## Method

Two public datasets of real agentic activity:

- **SWE-chat** — 557 agentic coding sessions → 94,813 development events, including **3,033 documentation interactions**.
- **AIDev** — 33,097 agentic pull requests → 690,260 classified file-level change records.

They build a coding scheme classifying documentation into agent-facing artefacts (instruction files like AGENTS.md/CLAUDE.md, working notes), classical technical documentation, and API references, then measure transition probabilities and lifts between doc events and code/test events (with a stage-adjusted model to control for session phase).

## Four Findings

1. **Agent docs dominate.** Instruction files + working notes = **60.5%** of all documentation interactions, vs **10.6%** for classical technical documentation and **1.3%** for API references. Agents mostly read/write docs written *for agents*, not the human docs.
2. **Consultation → editing link is weak/unresolved.** Adjacent transition probability 0.002; unadjusted three-event lift 1.05; only a stage-adjusted model puts it above unity (OR 1.33 [1.09, 1.62]). Doc *creation* is elevated unadjusted (lift 1.67) but its adjusted interval includes unity. So "read the docs, then edit" is not a clean behavioural pattern.
3. **No doc-based validation.** No explicit documentation-based validation sequence was observed, and consultation is associated with *less* immediate testing (lift 0.23; adjusted OR 0.39 [0.25, 0.60]). Agents don't check their work against docs.
4. **Docs trail code.** Consultation is **self-initiated (70.2%)** far more than failure-driven (7.5%). In multi-commit PRs that change both, **code is touched first 4.7× more often** than docs. Documentation follows the code, it doesn't lead it.

## The Model

From these traces they derive a **descriptive two-lobed cycle** of agent-documentation interaction, *not* a linear "discover → read → apply → verify" journey. Two widely assumed properties of "agent-friendly" documentation — **actionability** (docs drive the next edit) and **verifiability** (docs used to validate) — **lack consistent behavioural support** in the data.

## Why It Matters for SmolPaws

- **Direct pairing with [`evaluating-agents-md-repository-level-context-files.md`](./evaluating-agents-md-repository-level-context-files.md).** That paper showed AGENTS.md/CLAUDE.md often *hurt* task success and cost more. This one shows *why* the picture is murky: instruction files are by far the most-touched doc type, but their link to actual editing and validation is weak and phase-dependent. Together: agents lean heavily on agent-facing context files, yet those files don't reliably drive better behaviour.
- **Validates the "writing-for-agents" instinct but tempers it.** SmolPaws' own AGENTS.md / skills / MEMORY.md are exactly the "agent-facing artefacts" that dominate (60.5%). Worth writing well — but this paper is a caution that *actionability* and *verifiability* claims about such docs are behaviourally unproven; don't assume a skill file reliably steers the next action.
- **Memory/working-notes angle.** "Working notes" being a top doc category maps onto our daily-memory + dreaming loop; agents genuinely create and re-read their own notes.
- **Consultation is self-initiated, not failure-driven** (70.2% vs 7.5%) — agents reach for docs proactively, so front-loading good context (not just error-recovery hints) is the higher-leverage place to invest.

## Caveats

- Descriptive, behaviour-grounded — it maps what agents *do*, not what *works*. It does not show that better docs would change outcomes (that's the AGENTS.md eval paper's lane).
- Two datasets (SWE-chat, AIDev) of a particular era of agents; behaviour will shift as harnesses change.
- Authors release the pipeline, coding scheme, and event-level data — reproducible.
