# Running a Software Factory Efficiently at Uber Scale

**Author:** Uber Engineering ([@UberEng](https://x.com/ubereng)), post author @udaykiran
**Source:** [x.com/ubereng/status/2093444169037762840](https://x.com/ubereng/status/2093444169037762840) (blog, promoted at AI Engineer 2026)
**Date:** 2026-08-28
**Type:** Engineering blog / production field report

## One-Line Summary

The most concrete "software factory" data point: at Uber, **>70% of PRs are attributed to agents**, 3,600+ agent skills, 30K+ skill executions/day. They treat rising AI cost as a tractable engineering problem — decompose spend into a **six-term cost equation**, benchmark real work, and route each workload to its **Pareto-optimal model**. Result Feb→Jul (model held constant): cost/1K requests **−34%**, cost/session **−52%**, while usage grew **7x** and quality held.

## Hard Numbers (the reason to keep this)

- >70% of PRs from local/cloud agents. 3,600+ skills. 30K+ skill runs/day.
- Feb→mid-Aug 2026: weekly active users **7x**, weekly agentic requests **9.4x**; total AI spend **stabilized since April** via optimization.
- Isolating *their own* gains (hold one model fixed, since every upgrade shifts behavior): cost/1K model requests **−34%** from peak; cost/session **−52%** from June peak.
- A growing share of sessions are **not human-initiated** — managed agents do code review, self-healing CI, E2E PRs with visual validation, on-call triage, bug debugging, maintenance.

## The Framework

### Four layers of agent usage
Specialized → general. The *higher* (more specialized/managed) the layer, the *more control* over cost, quality, and model selection. Strategic push: move work **from interactive developer sessions → fully managed agents**, because managed environments give complete control over routing, harness, and spend.

### The six-term cost equation
Total spend decomposed into six multiplicative terms:
- **First two = adoption & engagement** — want these growing (interactive or agent-on-your-behalf).
- **Three middle terms = optimization surface** — "the work the agent does on its own behalf, on top of the request an engineer actually made." Most effort goes here: plan faster, cut unwanted turns/errors, shrink input tokens.

### Optimization levers
- **Price/token — benchmark-driven model selection.** For each managed agent: (1) build a benchmark from the agent's *real work*; (2) run on a harness that serves any model (frontier or open-weight) behind one interface; (3) move to whatever is Pareto-optimal, *and keep moving* — "the frontier shifts every few weeks." Example: **uReview** (AI code review for all PRs) benchmarked on real PRs with known bugs graded easy/med/hard; scored on precision/recall/F1 + cost/latency/timeouts/noise. Switching models raised F1 *and* cut cost/PR. They also run an internal **Uber SWE Benchmark** over thousands of real monorepo PRs.
- **Default model selection.** Biggest lever: the **subagent default**. Subagents do well-defined tasks that often don't need frontier reasoning → default them to a weaker/cheaper model (manual override allowed); primary model does decomposition + evaluation.
- **Tokens/request.** Every turn re-sends full history + context + tool results, so per-request savings compound. **Auto-compaction at 400K tokens even for 1M-context models** (balances performance vs. cache bursts and repeated input cost). Unified harness wrapper for install/config/auth/cost visibility.

### Session-level waste detection
A dashboard flags **16 distinct anti-patterns** across local/cloud sessions, each paired with financial impact + targeted remediation. Named ones:
- Suboptimal routing (running simple multi-turn on Opus when Sonnet suffices).
- Context bloat (40KB MCP payloads persisting in context, re-billed every turn).
- Cache-expiration inefficiency (resuming after a break → expired prompt cache → full-price prefix rebuild).
- Prompt-init overhead (pre-loading 100K tokens of system instructions + tool defs before any user input).

### What's next
Grow the managed-agent fleet (each with target metrics + eval benchmark + Pareto model); dynamic model routing; deeper **context-graph** integration; real-time in-editor efficiency guidance (batch anti-pattern detection → continuous trace monitoring); **auto-generate skill updates from collected traces** ("record papercuts from skill executions").

## Why It Matters To Us

- **The empirical backbone of this directory.** Lloyd theorized the factory; Yegge is n=1 hobby-scale; Uber is n=production, with numbers. "70% of PRs are agent-attributed" is the headline stat for the whole agentic-engineering thesis.
- **Benchmark-real-work → Pareto model, and keep moving** is the concrete, honest version of Lloyd's "multi-model, built-in evals." It answers *how* you pick a model without hand-waving. Reusable methodology for any harness (incl. SmolPaws/OpenHands SDK model routing).
- **"Optimize the agent's self-directed work" (middle three terms)** names exactly the overhead SmolPaws' context budgeting / dreaming targets: input-token shrinkage, fewer wasted turns, cache-friendly ordering. Their 400K compaction threshold and cache-expiration lever are directly relevant to our context-window discipline.
- **Skills-from-traces again.** Uber's "auto-generate skill updates from traces" = poteto's `/automate-me` = SmolPaws' dreaming. **Three independent production/practitioner parties converged on it** — the strongest cross-source signal in this dir.
- **Subagent-defaults-to-cheaper-model** is a clean, adoptable pattern for any orchestrator with delegation.

## Where It's Thin / Skeptic's Notes

- **"70% of PRs attributed to agents" needs unpacking.** Attribution ≠ authorship ≠ merged-and-shipped. A human-triggered agent that writes a one-line fix counts; so does a bot rebasing. Impressive, but the metric is doing PR work.
- **Cost down, but against *their own* baseline.** The −34%/−52% are self-referential (model held constant, from a *peak*). Real question — total cost vs. the human-only counterfactual — isn't answered; total spend merely "stabilized."
- **All measurement, little on quality drift.** "Improving/maintaining output quality" is asserted; the eval detail is on cost/F1 for review, not on whether the 70% agent PRs are as good as human ones over time.
- **Vendor-neutral-ish but selective.** Explicit trademark nods to Anthropic/OpenAI; "publicly available pricing." The routing wins are real but framed to flatter their own infra.

## Related

- `software-factories-zach-lloyd.md` — the theory Uber operationalizes at scale.
- `verification-and-trust-lauren-tan-poteto.md` — the trust/verification layer; both do skills-from-traces.
- `fences-not-sandboxes-steve-yegge.md` — the other live factory (hobby-scale, governance-first) vs. this (enterprise-scale, cost-first).
- `notes/skills/` — 3,600 skills + auto-skill-generation from traces.
