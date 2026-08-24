# Adversarial Review: Structured Disagreement for Grounded Agentic Code Review

**Paper:** [arXiv:2608.18167](https://arxiv.org/abs/2608.18167)
**Authors:** Eric S. Qiu, Joyce Gill
**Date:** August 2026
**Subjects:** cs.AI, cs.SE

## One-Line Summary

A minimal 3-agent code-review protocol (coder + reviewer + critic) where a critic audits the reviewer through *structured disagreement* before edits; beats a 5-agent baseline on LiveCodeBench and tops F1 on SWE-PRBench — showing cooperative review needs disagreement that is minimal, structured, and evidence-grounded, not many agents.

## Core Idea

Two failure modes bracket multi-agent coding today: role-separated teams don't scale (diminishing returns as agent count grows), and pure subagents-as-tools throw away the benefit of agent interaction entirely. Adversarial Review (AR) aims for the middle: the least cooperation that still helps.

The loop uses three agents:
- **Main coding agent** — does the work / edits.
- **Reviewer** — evaluates the code.
- **Critic** — audits the *review* (not the code) via structured disagreement, before the main agent edits.

The critic's job is to prevent the reviewer and coder from rubber-stamping each other. Disagreement is the mechanism.

## Results

- **LiveCodeBench:** highest pass rate among tested methods; beats a five-agent baseline using only three agents.
- **SWE-PRBench:** naive AR hits a *false-consensus* failure — agents converge on agreement without enough evidence. A single prompt iteration that makes disagreement explicit fixes it and achieves the highest F1 among tested methods.
- **SWE-bench Verified:** improvements over baselines on repo-level tasks.

## What's Actually Novel / Useful

1. **Critic audits the review, not the code.** The adversarial layer sits one level up — it checks the reviewer's judgment. That's the structural trick that makes 3 agents beat 5.
2. **False-consensus is a named, reproduced failure mode.** Agents "agree" cheaply. The fix is not more agents or richer comms — it's *forcing* disagreement to be explicit and evidence-grounded. Directly relevant to any review/critique loop that risks sycophantic convergence.
3. **Minimal beats elaborate.** The claim is that cooperative code review does not require many agents or complex communication structures.

## Relevance to SmolPaws / OpenHands

- Directly informs agentic code-review loops (PR review, codereview skills). The "critic audits the reviewer" pattern is a cheap upgrade over a single reviewer pass, and the false-consensus warning is a concrete thing to guard against in any self-review or peer-review setup.
- Pairs with `misc/mixture-of-models-nsed-deliberation.md` (peer-review deliberation) and `misc/llm-evaluators-recognize-and-favor-their-own-generations.md` (self-favoring evaluators — another argument for an adversarial critic).
