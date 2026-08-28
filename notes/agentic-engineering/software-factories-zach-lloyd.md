# Cloud Software Factories — An Engineering Mindset for Coding Agents

**Author:** Zach Lloyd ([@zachlloydtweets](https://x.com/zachlloydtweets), CEO of Warp)
**Source:** [x.com/zachlloydtweets/status/2093379309566308664](https://x.com/zachlloydtweets/status/2093379309566308664)
**Date:** 2026-08-28
**Type:** Manifesto tweet (ties to warp.dev/factories)

## One-Line Summary

Stop hand-waving about which agent/model is best; set up a cloud "software factory" — SDLC automation loops defined as code — that measures agents against *your* data and workflows, and improves itself over time. Call it meta-engineering.

## Core Idea

A **software factory** is an automation loop around the SDLC, made of agents that triage, spec, implement, verify, review, monitor. The point isn't the agents — it's the *loop* being measurable and improvable, so you optimize ROI on "actual data and not vibes."

Design principles he lists:

| Principle | What it forces |
|---|---|
| **Defined as code** | Version-controlled, and the definition is itself editable by agents. |
| **Lives in the cloud** | Team access, central data storage, automations. |
| **API-driven runtime** | Not UI-first. |
| **Built-in evals/benchmarks** | Prove improvement over time, not assert it. |
| **Multi-model, multi-agent** | Ride model/harness improvements without rewrites. |

## The Self-Improvement Loop (the load-bearing claim)

Three roles, closing the loop:

1. **Factory agents** — triage, implement, verify: they build the product.
2. **Scorer agents** — periodically grade that work along human-defined dimensions (cost, quality, verbosity, …).
3. **Self-improvement agents** — read scores, propose improvements as **diffs against the factory definition**. Humans review those as PRs and merge.

Because the factory is code, agents can propose edits to it the same way they edit any repo. That's the "closed-loop" goal: data, observability, and improvement baked in so both agents and humans raise the factory's quality over time.

## Why It Matters To Us

- This is the "best harness, best model" thesis scaled to a *team-level SDLC*: the factory definition is a harness-of-harnesses. Maps directly onto SmolPaws' own skills + heartbeat + dreaming loop, just industrialized.
- **Scorer → self-improvement agents ≈ our dreaming step.** SmolPaws already promotes/prunes its own context nightly; Lloyd's version grades work products and proposes definition diffs. Same shape, different substrate (memory vs. workflow-as-code).
- "Defined as code, editable by agents" is exactly why we keep skills and AGENTS.md as plain files an agent can rewrite. Validates the local design.

## Where It's Thin / Skeptic's Notes

- **The scoring dimensions are the whole game, and they're hand-waved.** "Cost, quality, verbosity" — *quality* is doing enormous work. Whoever defines the eval defines the optimum; a factory that self-improves toward a bad metric just gets worse faster. This is the Goodhart risk, unaddressed.
- **Humans-review-PRs is the real throughput cap.** If every improvement needs human PR review, the "closed loop" is only as fast as the reviewer. The claim of automation-over-time understates that bottleneck.
- **Vendor pitch attached.** It's an argument for buying Warp's factory platform. The *idea* (measure the loop, define it as code) is separable and correct; the "you can't build this yourself, it's a big endeavor" framing is the sales part.
- **No mention of provenance/verifiability of the work itself** — which is exactly the gap Josh Rosen's "receipts" fills. Read the two together.

## Related

- `immutable-artifacts-josh-rosen.md` — the missing verifiability layer for a factory's outputs.
- `notes/harness/` — code-as-harness and Harness Handbook: the factory definition, at the subsystem level.
- `notes/skills/` — self-improvement-as-diffs ≈ skill optimization at the workflow scale.
