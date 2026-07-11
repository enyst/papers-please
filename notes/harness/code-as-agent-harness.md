# Code as Agent Harness

**Paper:** [arXiv:2605.18747](https://arxiv.org/abs/2605.18747)
**Authors:** Xuying Ning, Katherine Tieu, Dongqi Fu, Tianxin Wei, Zihao Li, Yuanchen Bei, Jiaru Zou, ... Hanghang Tong, Jingrui He (large collaboration; UIUC-led)
**Date:** May 2026
**Type:** Survey

## One-Line Summary

Reframes the agent *harness* around code: code is no longer just an output but the operational substrate for an agent's reasoning, acting, environment modeling, and execution-based verification.

## Core Idea

In agentic systems, code stops being only a target artifact and becomes the **infrastructure** an agent runs on. The survey unifies this under "code as agent harness" and organizes the field into three connected layers:

| Layer | What it covers |
|---|---|
| **Harness interface** | How code connects the agent to *reasoning*, *action*, and *environment modeling*. |
| **Harness mechanisms** | Planning, memory, and tool use for long-horizon execution; plus feedback-driven control and optimization that make the harness reliable and adaptive. |
| **Scaling the harness** | Single-agent → multi-agent: shared code artifacts support coordination, review, and verification across agents. |

Across these layers it catalogs representative methods and applications: coding assistants, GUI/OS automation, embodied agents, scientific discovery, personalization/recommendation, DevOps, and enterprise workflows.

## Open Challenges (their "harness engineering" agenda)

- Evaluation **beyond final task success**.
- Verification under **incomplete feedback**.
- **Regression-free** harness improvement (don't break behavior while improving it).
- **Consistent shared state** across multiple agents.
- **Human oversight** for safety-critical actions.
- Extension to **multimodal** environments.

## Why It Matters To Us

- Names the thing we build (SmolPaws / OpenHands SDK) as a first-class object of study: the harness, with code as its substrate. "Best harness, best model" stated as a research program.
- The three-layer decomposition (interface / mechanisms / scaling) is a useful skeleton for documenting *any* harness, including the OpenHands SDK.
- The open challenges map onto our own work: evaluation beyond task success, regression-free changes (cf. the `iterate` skill + generated-artifact freshness), shared state across delegated subagents, human-in-the-loop confirmation.

## Related

- [Harness Handbook](harness-handbook.md) — a concrete method/tool for making a specific harness's behavior navigable and auditable (behavior→code map). This survey is the map of the territory; the Handbook is one instrument for walking it.
