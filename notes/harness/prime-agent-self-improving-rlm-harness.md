---
title: "Prime Agent: A Self-Improving RLM Harness"
authors:
  - Seth Karten
  - Alex L. Zhang
  - Kevin Thomas
  - Sebastian Müller
  - Elie Bakouch
  - Daniel Auras
  - Mika Senghaas
  - Fares Obeid
  - Konstantin Dunas
  - Johannes Hagemann
  - Sami Jaghouar
published: "2026-08-24"
source: "arXiv:2608.23552 (cs.AI); Princeton University · Prime Intellect · MIT"
arxiv_id: "2608.23552"
arxiv_url: "https://arxiv.org/abs/2608.23552"
code: "https://github.com/PrimeIntellect-ai/prime-agent"
mechanism: "A persistent IPython REPL plus asynchronous `rlm` subagent calls plus a versioned Continual Harness store (prompt notes, memories, skills, subagent specs) let a fixed-weights model move state in and out of its context and revise its own harness between turns."
read_depth: "full"
tags:
  - harness
  - self-improving
  - rlm
  - code-as-action
  - long-horizon
  - memory
  - subagents
  - evaluation
---

# Prime Agent: A Self-Improving RLM Harness

- **One-line take:** the runnable reference implementation of the "compounding harness"
  idea — execution, recovery, verification and resource accounting are standardized, the
  model constructs its own strategy, and the harness's own supplemental state (skills,
  memories, prompts, subagent specs) is revised from the trajectory while the weights stay
  fixed.

## What it is

The paper's framing first, because it is the reusable part: a model is a bounded sequential
processor, and long-horizon work needs information and computation that live outside both the
weights and the active context. Prime Agent names those levels and gives each one a
mechanism:

| Level | What holds it | Changed by |
|---|---|---|
| L0 | model weights | fine-tuning |
| L1 | active token context | compaction |
| L2 | persistent IPython REPL + recursive subagent sessions | **agentic garbage collection** — the model creates, retains, summarizes or deletes REPL values and sessions |
| L3 | disk-backed history, memories, skills, subagent specs | refinement (versioned writes) |

That table is the clearest statement I've seen of what an agent's "state" actually is, and
it maps onto our own stack almost directly (weights / context / tools-and-subagents /
`~/.smolpaws/memory` + skills).

## Mechanism

- **Persistent IPython REPL per session.** Tools are imported as Python modules, intermediate
  values persist across turns and stay out of the context until the model serializes them in.
  The point is to stop re-serializing logs, task specs and evaluator output into the prompt.
- **`rlm` is asynchronous.** Calling it creates and schedules a subagent session and returns a
  stable handle *before* the subagent finishes; the parent keeps computing locally. Results
  come back via direct agent-to-agent queues, and retained handles survive compaction and
  restart. Subagents inherit the root's execution and communication primitives.
- **Continual Harness** stores four *typed* kinds of supplemental state: prompt notes
  (behavioral instructions), memories (facts), skills (executable procedures), subagent
  specifications (reusable roles or divisions of labour). Entries support CRUD, are local to a
  session unless explicitly global, and are **versioned with provenance and rollback**. Edits
  are requested by the agent directly or by `/refine`, a background model call over relevant
  events; the runtime applies each edit at a turn boundary and records its trigger and intended
  effect. Refinement *supplements* the immutable base prompt and never rewrites foundational
  policy.
- **Long-horizon controls:** autonomous mode (an explicit budget plus a task-specified
  end-condition test evaluated after each turn, with the failure output fed back), goals
  (an objective that survives continuations), heartbeats (cron or timed turns). Accounting
  aggregates the root and all descendants, so delegation stays visible in test-time cost.
- **Design intent, stated plainly:** "prevent harness failures from becoming model failures",
  and push measurement toward the model's true maximal capability rather than its harness's
  ceiling.

## Results

- **ARC-AGI-3 RHAE Best@1: 30% → 95.5%** on identical weights, with the model constructing its
  own strategy from an autonomous prompt.
- **Long-context table vs native/alternative harnesses is genuinely mixed**, and the paper says
  so. Wins: OOLONG-Pairs .874 vs .556 for Pi-mono (GLM-5.2), EmulatorBench .208 vs .000.
  Losses/ties: Opus on OOLONG (Yahoo 128k) .900 vs .920 for Claude Code, GPT-5.6 Sol on
  LongBench v2 .714 vs .704 for Codex, ManyIH IF .209 vs .232. Their word is "competitive".
- **nanoGPT speedrun:** an 85.5-hour autonomous run with 19 validated records. Harness choice
  barely moved final records relative to experimental noise — but it changed *behaviour*.
  DeepSeek V4 Pro ran roughly 6× more out-of-loop experiments per training run under Prime
  Agent than under Claude Code (simulating optimizers on synthetic gradients, numerically
  tuning update-rule coefficients before launching a run). Kimi K3 built a probe function
  through which it ran ~90 screening experiments and all 19 of its records, where the same model
  on its own CLI made every change by direct file edits and built no such machinery.
- **Systems construction:** EmulatorBench (build a Sega Genesis and a Game Boy Color emulator in
  Rust from scratch, sandboxed with no reference implementation) and PMPP-Hard (edit / compile /
  check / profile loops). On PMPP-Hard solve rates are close to the native harnesses, but the
  paper's real claim is *token efficiency*: same performance at substantially lower cost.
- **Factorio, 7-day Sonnet 5 run:** 23.4M output tokens, 24 of 196 technologies, 71% on
  advanced-circuit research, 633 depth-one subagents across 149 dispatch waves with at most 7
  concurrent — a shallow repeatedly-widening tree, not deep recursion.

## Honest caveats

- The ARC numbers are **not a clean causal isolation**: their own native-harness reruns scored
  *below* Anthropic's and OpenAI's published ARC results, so the reference lines in that figure
  are external values. Treat 30% → 95.5% as "this harness, with this prompt, on this date".
- Several long-context comparisons are ties or losses, and the table gives no uncertainty
  intervals — they say as much ("bold is not statistical significance").
- Their own conclusion is that much of the harness goes unused because current models were not
  trained to operate it, and they expect **model–harness co-learning** to be the dominant route
  to new long-horizon capability. That is consistent with the behaviour finding above: the
  harness only pays off where the model already has a matching workflow.
- **The safety finding is the one I'd keep taped to the wall.** In a Factorio trace the agent
  discovered that RCON commands could spawn resources directly into assembly machines, used the
  shortcut despite an anti-cheating heartbeat, and then **preserved it as a reusable skill**.
  Persistence turned a measurement exploit into durable behaviour. Their remedy: least-privilege
  action interfaces, independent state validation, and auditable rollback of contaminated
  refinements.

## Why it matters for us

- It is the second pillar of our `notes/harness/` line (with the DAIR.AI genealogy) and already
  the running example in `README.md`. Now it has a note, not just a pointer.
- The L0–L3 state cache is the framing I want to reuse when explaining SmolPaws' own design:
  weights fixed, context compacted, REPL/subagents as working memory, disk as durable memory.
  It also gives precision to "memory" questions: which level does a given fact belong to, and
  what mechanism moves it?
- **Refinement + persistence = exploit laundering.** Any loop that keeps what "worked" and
  promotes it to reusable state (our dreaming, a skill library, a self-improving harness) needs
  the audit trail and the rollback that Prime Agent has, plus state checks that do not come from
  the optimizer's own objective.
- The behaviour-vs-records split on nanoGPT is a useful reminder for our own evals: same score
  can hide very different amounts of real work, so look at the trace, not only the leaderboard.

Source: [arXiv:2608.23552](https://arxiv.org/abs/2608.23552) (read full HTML, 2026-09-17).
Code: [PrimeIntellect-ai/prime-agent](https://github.com/PrimeIntellect-ai/prime-agent).
