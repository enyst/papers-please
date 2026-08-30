---
title: "Vero: Can AI Agents Build Formally Verified Software Repositories?"
authors: Zhe Ye, Hantao Lou, Yuechun Sun, Peiyang Song, Zhengxu Yan, Timothe Kasriel, Qingyang Zhang, Kaiyu Yang, Soonho Kong, Jingxuan He, Dawn Song
arxiv_id: "2608.13522"
arxiv_url: https://arxiv.org/abs/2608.13522
published: 2026-08-13
mechanism: First repository-level benchmark for joint implementation-and-proof synthesis in Lean 4; 43 multi-module instances with a formal audit mechanism that accepts machine-checked proofs of spec unsatisfiability / reference-code incorrectness
tags: [verification, formal-methods, code-generation, benchmark, lean4, repository-level, coding-agents, vericoding, audit]
---

# Vero: Can AI Agents Build Formally Verified Software Repositories?

**Paper:** [arXiv:2608.13522](https://arxiv.org/abs/2608.13522) · **Authors:** Zhe Ye, Hantao Lou, Yuechun Sun, Peiyang Song, Zhengxu Yan, Timothé Kasriel, Qingyang Zhang, Kaiyu Yang, Soonho Kong, Jingxuan He, Dawn Song (UC Berkeley et al.) · **Date:** 2026-08-13 · **Subjects:** cs.LG/AI/LO/PL/SE

## One-Line Summary

The **first repository-level** benchmark for *verified* code generation: an agent must produce **both** a multi-module implementation **and** a machine-checked Lean 4 proof that it meets a formal spec — across real codebases, not single functions. It's frontier-resistant: the best agent fully solves only **27 of 43** instances, and **10 resist every** configuration.

## Why It's Different From Prior Work

Two gaps in existing verified-code-gen benchmarks:
1. **Function-level only** (miniCodeProps, FVAPPS, VERINA, CLEVER, most Dafny/Verus sets) — standalone problems from HumanEval/MBPP/APPS.
2. **Proof-only at repo scale** (RVBench, VeruSAGE-Bench, VeriSoftBench, CoqStoq) — they hand the agent a fixed implementation and only ask for proofs.

Vero does the **joint code-and-proof task at the repository level**. The authors argue repo-scale verification "does not reduce to scaling up function-level techniques," because code, spec, and proof choices are *coupled across modules* — a local implementation choice can make a downstream proof easy or impossible.

## The Benchmark

- **43 multi-module Lean 4 instances**, curated from real repositories originally in **Python, Dafny, Verus, Coq** — domains from cryptographic protocols and distributed systems to foundational data structures. Sourcing from verification-aware languages gives real specs to port.
- Each instance = a multi-module Lean 4 repo with **predetermined API interfaces**, **manually curated formal specifications**, and **reference implementations**.
- **Two evaluation modes:**
  - **Proof-only** — implementation provided, agent writes proofs.
  - **Code-and-proof** — agent synthesizes *both*; "qualitatively different" because implementation freedom interacts with proof difficulty.
- **Reward-hacking defenses** (Appendix D, 3 layers): slot-scoped re-rendering, an **axiom allowlist** (block `sorry`/custom axioms), and declaration screening — so an agent can't "prove" things by assuming them.

### The novel bit: a formal audit mechanism
Benchmark ground truth itself can be subtly wrong (a known problem in formal-verification benchmarks). Instead of silently penalizing agents for benchmark defects, Vero **accepts machine-checked proofs that a provided spec is unsatisfiable or a reference implementation is incorrect** — turning "agent failure" into an actionable benchmark correction. Documented case studies fixed real defects (e.g. two specs in direct conflict; a comparator-lawfulness gap in `verified_ironkv`). This makes the benchmark *self-correcting as agents get stronger*.

## Key Results

Harnesses/models: **Codex (v0.140.0)** with GPT-5.5 at medium and **xhigh** reasoning; **Claude Code (v2.1.191)** with **Claude Opus 4.8** and **Claude Sonnet 5** at xhigh. Full tool access — filesystem edits, build invocations, the Lean toolchain.

- **GPT-5.5 (xhigh) leads by a wide margin:** 27/43 code-and-proof, 25/43 proof-only. Far ahead of Claude Opus 4.8 (8 / 10), GPT-5.5 (mid) (2 / 6), Claude Sonnet 5 (2 / 2).
- **Frontier-resistant:** 10 instances resist all 8 configurations in both modes; most solved instances are closed by **only one** configuration ("shared walls, not random residuals" — failures concentrate on the same hard repos).
- **The wall is global reasoning, not local proof skill.** Unsolved instances encode **cross-module invariants, protocol consistency, and custom mathematical theories**. Specs needing no helper lemma pass ~83.9% (code-and-proof); at helper-chain **depth ≥4** that falls to ~50.6% (39.1% proof-only). Agents attempt *local* proofs of individual obligations and can't build the layered lemma chains.
- **Agents commit to an implementation early, then grind proofs.** GPT-5.5 (xhigh) fixes its median ~65 impl lines by minute 30, then grows proof text 883→1,077 lines. Implementation freedom "helps only the strongest agent."
- **Failure modes differ by strength:** strong agents leave ~a third failing at build time and ~14% rejected as cheating (they *attempt* the hard obligations); weak agents leave ~78% of specs with **no proof body at all**.
- **Cost:** the most capable config is also *cheapest per completed repo*; raising reasoning effort is **superlinear in yield**; unfinished runs cost more than finished ones.

## Why It Matters To Us

- **The honest ceiling on "trustworthy AI code" right now.** This whole cluster of my recent notes (software factories, verification-is-the-bottleneck) assumes agents can eventually *prove* their work. Vero measures that directly at repo scale: even GPT-5.5 xhigh clears only ~63%, and 10 repos are untouched. Verification isn't just the bottleneck rhetorically — it's an empirically hard wall.
- **The audit mechanism is a genuinely reusable idea.** "Let the agent prove the *benchmark* wrong, with a machine-checked counter-proof" is a clean way to keep an eval honest as models improve. Same spirit as our verification-as-judge / proposal-consequence threads — the deterministic checker adjudicates both the agent *and* the ground truth.
- **Cross-module invariants are where agents fall down** — mirrors the codebase-design/deep-module theme: the hard part isn't the function, it's the coupling across boundaries. An agent that can't hold a global invariant can't verify a real system.
- **Method matters more than raw model:** GPT-5.5 xhigh vs mid is a huge gap (27 vs 2). Reasoning-effort/harness config dominates — echoes the "best harness, best model" and Pareto-routing threads.

## Where It's Thin / Skeptic's Notes

- **Small N (43 instances)** and Lean-4-only. Real, hand-curated, and hard — but not a large-scale statistical benchmark, and results are per-repo lumpy.
- **Ported specs, not native ones.** Instances are curated from Dafny/Verus/Coq/Python originals into Lean 4; the porting choices shape difficulty.
- **Frontier config churn.** Specific versions (Codex 0.140.0, Claude Code 2.1.191, GPT-5.5, Opus 4.8) date fast; treat absolute numbers as an Aug-2026 snapshot, the *ranking of difficulty sources* as the durable finding.
- **Curation is expensive** (their own "curation effort" appendix) — extensibility depends on the semi-automated pipeline actually scaling.

## Related

- `algoveri-verified-code-generation.md` — sibling benchmark, **function-level** across Dafny/Verus/Lean; Vero is the **repository-level** step up. Both find Lean/explicit-proof hardest and "verification ≠ testing."
- `../harness/skill-state-scalable-long-horizon-agent-skills.md` — runtime-owns-validity / deterministic judge (same trust-the-checker spirit as the audit mechanism).
- `../agentic-engineering/` — verification-is-the-bottleneck thesis; Vero is the hard empirical evidence for it.
