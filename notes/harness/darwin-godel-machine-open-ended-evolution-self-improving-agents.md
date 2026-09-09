# Darwin Gödel Machine: Open-Ended Evolution of Self-Improving Agents

**Paper:** [arXiv:2505.22954](https://arxiv.org/abs/2505.22954)
**Authors:** Jenny Zhang, Shengran Hu, Cong Lu, Robert Lange, Jeff Clune
**Date:** 2025-05-29 (v3, 2026-03-12)
**Subjects:** cs.AI
**Type:** Self-modifying agent architecture + empirical study

## One-Line Summary

A coding agent that **edits its own source code** and keeps every version in an **archive of ancestors**, growing an open-ended tree of agents. Each proposed self-modification is kept or discarded by **empirical validation on coding benchmarks** — not by proof. It's the point in the harness genealogy where the *harness code itself* becomes the thing being optimized.

## The Problem

The original **Gödel machine** (Schmidhuber) is a self-improving AI that rewrites itself only when it can *prove* the change is net-beneficial. Proving that for most real changes is impossible in practice, so the idea never ran. Meta-learning automates algorithm discovery but is stuck at first-order improvements inside a human-designed search space.

## The Method

Replace the proof requirement with **Darwinian empirical validation**:
1. Maintain an **archive** of generated coding agents (starts from one).
2. **Sample** an agent from the archive and hand its own code to a foundation model, asking for a new, *interesting* variant (open-ended exploration, not just greedy hill-climbing).
3. **Score** the variant on coding benchmarks; add it back to the archive.
4. Because a better agent is also better *at modifying agents*, improvements compound. The archive becomes a growing tree of diverse, high-quality agents, allowing parallel exploration of many paths (open-endedness / stepping-stone collection rather than a single optimum).

The self-discovered improvements are concrete harness pieces: better code-editing tools, long-context window management, peer-review mechanisms.

## Key Results

- **SWE-bench: 20.0% → 50.0%**; **Polyglot: 14.2% → 30.7%**, holding the underlying foundation model fixed — the gains come from the harness the DGM wrote for itself.
- Significantly beats ablations without self-improvement and without open-ended (archive) exploration — both ingredients matter.
- All runs under safety precautions: sandboxing + human oversight.

## Why It Matters (for us)

This is the "let the harness learn" apex in the DAIR.AI [Harness Engineering](../../blogs/interesting-posts.md) genealogy: not optimizing the prompt (DSPy/GEPA) or the scaffolding around a fixed loop, but rewriting the agent's *own code*. Same self-improving-SDLC cluster as our `../agentic-engineering/harness-of-harness-multi-day-autonomous-development.md` (HoH wraps a harness; DGM mutates one) and a natural pair with Meta-Harness (`meta-harness-end-to-end-optimization-of-model-harnesses.md`, an outer loop that searches harness code with an explicit scorer instead of an evolutionary archive). The archive-of-ancestors idea rhymes with our skills/experience-compilation notes (Voyager's skill library, Trace2Skill) — keep stepping stones, don't collapse to one line.

## Caveats / Limits

- Empirical validation inherits benchmark bias: the DGM optimizes whatever the benchmark rewards, including possible reward-hacking of the eval harness (the paper flags safety/sandboxing precisely because a self-editing agent scored by an eval is a gameable loop).
- Cost: maintaining and scoring a growing archive is expensive; open-endedness trades compute for diversity.
- "Interesting-ness" of proposed variants is foundation-model-dependent — the search is only as good as the proposer.

## Beyond the paper

Reference implementation (self-modifying agent archive) is open-sourced; linked from the collection's "Beyond the papers" section.
