# Two Camps of Agentic Engineering — Vítor Balocco (synthesis)

**Author:** Vítor Balocco ([@vitorbal](https://x.com/vitorbal))
**Source:** [x.com/vitorbal/status/2093363623376589046](https://x.com/vitorbal/status/2093363623376589046)
**Date:** 2026-08-28
**Type:** Synthesis tweet (names the poles this whole directory circles)

## One-Line Summary

Opinions on agentic engineering are converging into **two camps** — *plan hard up front, then let agents cook* (HumanLayer/Dex Horthy) vs. *invest hard in guardrails + automatic verification up front, let agents rip, garbage-collect periodically* (poteto/Lauren Tan). Balocco lands **in between**, and adds the practical middle-path mechanics.

## The Two Camps (his framing)

| | **The HumanLayer way** (plan-first) | **The poteto way** (guardrail-first) |
|---|---|---|
| Bet | "Put a lot of planning up front, all the way down to **program design**, then let the agents cook." | "Do a shit ton of investment in **architecture/linters/LLM checks/automatic verification** upfront, then let agents rip. **Garbage collect periodically.**" |
| Where the human effort goes | Before generation: specs, plans, design. | Before *and after*: build the rails, then sweep for what slipped through. |
| Trust model | Trust the plan. | Trust the guardrails (and re-verify constantly). |

This is exactly the tension the rest of the directory embodies: Horthy×Gupta (`software-factory-design-patterns…`) push planning/program-design; poteto (`verification-and-trust-lauren-tan-poteto`) pushes rigor+verification-as-rails. Balocco just names it cleanly.

## His middle path (the actual content worth keeping)

- **Research + planning up front, but skip program design** *unless* he spots a net-new abstraction is needed, or it's high-stakes/core code. (Plan-first, selectively.)
- **For everyday work, lean heavily on guardrails.** (poteto-side by default.)
- **Frequent sampling of PRs landing on main** to spot bad code a guardrail *should* have caught → add the missing guardrail, burn down the offenders. (A feedback loop that *grows the rails from observed escapes*.)
- **Frequent sampling of codebase hot spots** to detect when *human intervention* is needed — e.g. an abstraction grown out of control. Muses about building a **heatmap visualization** for this.
- Endorses poteto's **tier of guardrails**, in strength order:
  **opinionated architecture > static analysis > tests > LLM checks.**

## The Guardrail Tiering (the sharpest reusable idea)

poteto's ordering, amplified by Balocco: prefer the *strongest, most deterministic* guardrail available.
1. **Opinionated architecture** — make the wrong thing impossible to express. (Strongest: structural.)
2. **Static analysis / linters** — deterministic, fast, catches classes of error.
3. **Tests** — verify behavior, but only what you thought to test.
4. **LLM checks** — flexible, catch the un-lintable, but probabilistic/weakest.

This is a *hard-boundary-first* hierarchy — deterministic rails beat probabilistic ones — which quietly agrees with the security camp (Bargury/Schneier in `blogs/`) against Yegge's "polite fence" optimism. Reach for the LLM check last, not first.

## Why It Matters To Us

- **This is the directory's synthesis note.** It collapses six sources into one axis (plan-first ↔ guardrail-first) and a defensible middle. Good top-of-mind map.
- **"Grow guardrails from observed escapes"** is a concrete self-improvement loop we don't have explicitly: sample merged PRs → find what slipped → add the rail that would've caught it. That's skills-from-traces (Uber/poteto/our dreaming) pointed at *guardrails* instead of skills. Directly adoptable.
- **The guardrail tier ranks our own tools.** For SmolPaws/OpenHands: opinionated architecture + typed boundaries (strongest) > linters/CI > tests > the LLM-as-reviewer skills like `codereview-axes`/`no-ai-slop` (weakest, use last). Good discipline against reaching for an LLM check when a linter would do.
- **Hot-spot heatmap** is a nice, small idea: surface where abstractions are decaying so a human steps in. Aligns with `improve-codebase-architecture`.

## Where It's Thin / Skeptic's Notes

- **It's a map, not evidence.** A tidy 2-camps framing is satisfying and probably too tidy — Yegge (govern with law), Rosen (receipts), Ng (human keeps the tradeoffs) don't fit neatly on this one axis. Treat it as a useful lens, not the whole territory.
- **"Somewhere in between" is the safe answer.** The value is in the *specific* mechanics (sample-PRs-grow-guardrails, hot-spot sampling, the tier), not the centrist conclusion.
- **No numbers.** One practitioner's workflow; the heatmap is still a "maybe I oughta build."

## Related

- `software-factory-design-patterns-ai-that-works.md` — the plan-first (HumanLayer) pole.
- `verification-and-trust-lauren-tan-poteto.md` — the guardrail/verification-first (poteto) pole; source of the guardrail tiering.
- `ai-engineering-skills-map-andrew-ng.md` — the human-judgment layer that sits above both camps.
- `blogs/interesting-posts.md` — deterministic-over-probabilistic (hard vs soft boundaries) echoes the guardrail tier.
- SmolPaws local: `codereview-axes`, `no-ai-slop`, `improve-codebase-architecture` (LLM-check tier); linters/CI (static tier).
