# Harness Handbook — Making Agent Harnesses Understandable, Auditable & Editable

**Project page:** [ruhan-wang.github.io/Harness-Handbook](https://ruhan-wang.github.io/Harness-Handbook/)
**Authors:** Ruhan Wang, Yucheng Shi, Zongxia Li, Zhongzhi Li, Yue Yu, Junyao Yang, Kishan Panaganti, Haitao Mi, Dongruo Zhou, et al.
**Affiliations:** Tencent HY LLM Frontier; Indiana University; University of Maryland; University of Georgia; National University of Singapore
**Date:** June 2026
**Type:** Project page + tool (paper "coming soon"; no arXiv entry under this title as of 2026-07-11)

## One-Line Summary

A **behavior-level manual** for an agent harness: a navigable map that starts from a system behavior and links every step to verifiable code evidence, so the harness can be understood, audited, and edited without reading the whole tree.

## The Problem

A harness — "the subsystem that makes an agent operational" (prepares context, provides tools, preserves state, checks permissions/sandbox rules, turns model output into real actions) — is what actually decides agent behavior, not the model alone. But that behavior is implicit and buried in code. Ask a concrete question — *"will the agent confirm before deleting a file?"* — and you must find the confirmation logic, trace every bypass path, and locate every implementation site a change would touch. Grepping `delete` / `permission` / `confirm` returns scattered fragments.

> The problem is not missing code, but a missing path **from behavior to implementation**.

Scale example: Codex is ~2,267 files, >34,000 functions, ~160,000 code connections. A file tree shows *where* code lives, not *how* pieces combine into a behavior.

## The Method

The Handbook reorganizes scattered implementation into **navigable behavior paths**, each step linked to verifiable code evidence, generated *from* the code. One behavior request typically spans many implementation sites; the map connects behavior ↔ code so understanding, auditing, and modification share one artifact. Three use-cases, all starting from a behavior and returning to code for evidence:

| Goal | What you do with the map |
|---|---|
| **Understand** | Follow one request end-to-end: what the model receives, when tools are called, how state moves, how failures are handled. |
| **Audit** | Trace the actual execution path to check permissions, confirmation logic, sandboxing, and data flow — *including* unusual routes that bypass those protections. |
| **Adapt** | See which capabilities the harness provides and the code behind them, then extend/adjust to build your own agent. |

Additional claim: it makes a **coding agent's edits more reliable** — mapping a natural-language change request to the relevant behavior units + implementation sites, so the agent skips irrelevant searches, misses fewer dependencies, and produces a tighter edit plan (evaluation promised).

Ships **Handbook Studio**, an operational entry point over the behavior map, with demos for **Terminus** and **Codex**. GitHub "coming soon".

## Why It Matters To Us

- It's a concrete method for the thing we keep hand-rolling for OpenHands: behavior→code maps (cf. our `show-me` / `teach-me` study pages). Worth watching for the released method to generate the map automatically.
- Reinforces the thesis "the harness, not the model, decides behavior" — shared with [Code as Agent Harness](code-as-agent-harness.md) and with Raschka's harness-token-overhead finding (`blogs/interesting-posts.md`).
- The audit use-case (find bypass paths for confirmation/sandboxing/permissions) is directly relevant to reviewing the OpenHands SDK's security surface.

## To Revisit

The landing page is JS-rendered; this note is built from the intro + takeaways. Revisit the deep sections once the paper/repo drop: (1) how the behavior map is generated from code, (2) the behavior-question → code-evidence retrieval, (3) the "does it help a coding agent find code more accurately" evaluation.

## Related

- [Code as Agent Harness](code-as-agent-harness.md) — the survey that frames the whole "code as harness" territory; the Handbook is one instrument for navigating a specific harness within it.
