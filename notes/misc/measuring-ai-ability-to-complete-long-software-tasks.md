# Measuring AI Ability to Complete Long Software Tasks

**Paper:** [arXiv:2503.14499](https://arxiv.org/abs/2503.14499)
**Authors:** Thomas Kwa, Ben West, Joel Becker, Amy Deng, Megan Kinniment, Nate Rush, Nikola Jurkovic, et al. (METR)
**Date:** 2025-03-18 (v4, 2026-07-10)
**Subjects:** cs.AI; cs.LG
**Type:** Capability measurement / metric proposal

## One-Line Summary

Stop scoring agents on single-turn pass rates; measure the **length of task** they can finish. METR's metric: the **50%-task-completion time horizon** — the time a skilled human takes on tasks the model completes with 50% success. It converts benchmark numbers into a human-time scale and reveals a trend line.

## The Metric

- Time humans with domain expertise on a task set (RE-Bench + HCAST + 66 novel shorter tasks), then find the human-time length at which a model hits **50% success**. That length is the model's time horizon.
- **Frontier models (e.g. Claude 3.7 Sonnet) sit at ~50 minutes.** The point isn't the absolute number; it's that a single scalar now maps model capability onto *how long a human would take*.

## The Trend Line

- **AI time horizon has roughly doubled every ~7 months since 2019**, possibly accelerating in 2024.
- Improvement is driven mainly by **greater reliability and ability to recover from mistakes**, plus better reasoning and tool use — not raw single-step accuracy.
- Naive extrapolation: within ~5 years, AI could automate many software tasks that currently take humans a month. (The paper is explicit about external-validity caveats.)

## Why It Matters (for us)

This is the **yardstick behind the whole harness argument.** In the DAIR.AI [Harness Engineering](../../blogs/interesting-posts.md) genealogy it's the closing paper: harness progress (static-harness era → self-improving era) only *counts* if the horizon a system can work over is actually getting longer — the two eras are "two slopes on this chart." It reframes what our harness/condensation/memory work is *for*: the goal isn't higher single-turn scores, it's extending the reliable time horizon. Concretely useful framing for OpenHands long-horizon work (cf. `../harness/skill-state-scalable-long-horizon-agent-skills.md`, `../harness/continual-harness-online-adaptation-self-improving-foundation-agents.md`, and our notes+retrieval condensation proposal): reliability and mistake-recovery over long runs are what move the horizon, which is exactly what context management is supposed to protect.

## Caveats / Limits

- **Time horizon depends on the task distribution** — RE-Bench/HCAST + short tasks are not "all software work"; external validity is the paper's own biggest caveat.
- 50% success is a low bar for a *reliable* horizon; the useful-in-production horizon (e.g. 80–95%) is shorter.
- Human baseline timing is itself noisy (expertise, familiarity), so the absolute minutes should be read as order-of-magnitude, not precise.

## Beyond the paper

METR keeps an updated public tracker of the time-horizon trend across newer frontier models; the collection cites this paper as the chart "everyone cites."
