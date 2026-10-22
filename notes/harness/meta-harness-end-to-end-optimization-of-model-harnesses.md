# Meta-Harness: End-to-End Optimization of Model Harnesses

**Paper:** [arXiv:2603.28052](https://arxiv.org/abs/2603.28052)
**Authors:** Yoonho Lee, Roshen Nair, Qizheng Zhang, Kangwook Lee, Omar Khattab, Chelsea Finn
**Date:** 2026-03-30
**Subjects:** cs.AI
**Type:** Outer-loop optimization system

## One-Line Summary

An **outer loop that searches over harness *code*** — the logic deciding what to store, retrieve, and present to the model — using an **agentic proposer** that reads the full source, scores, and execution traces of every prior candidate. A harness that writes harnesses, around a fixed model.

## The Problem

LLM system performance depends on the harness (store/retrieve/present code), but harnesses are still hand-written. Existing **text/prompt optimizers** are a poor fit here because they **compress feedback too aggressively** — they distill traces into short textual lessons and throw away the detail an engineer would actually use to improve retrieval or context-assembly code.

## The Method

Meta-Harness gives its proposer **rich, uncompressed access to prior experience** through a filesystem: the source code, the scores, and the full execution traces of all previous candidate harnesses. The agentic proposer reads that history and writes a new harness (retrieval / memory / prompt-assembly code) around a **fixed** model, which is then scored — and its own code, score, and traces feed the next proposal. The thesis: *richer access to prior experience enables automated harness engineering*, where over-compressing optimizers fail.

## Key Results (all holding the model fixed)

- **Online text classification:** +7.7 points over a state-of-the-art context-management system while using **4× fewer context tokens**.
- **Retrieval-augmented math reasoning:** a single discovered harness adds **+4.7 points** on average across five held-out models on 200 IMO-level problems (generalizes across models).
- **Agentic coding:** discovered harnesses **beat the best hand-engineered baselines on TerminalBench-2**.

## Why It Matters (for us)

Directly the "meta harness: a harness whose job is producing harnesses" node in the DAIR.AI [Harness Engineering](../../blogs/interesting-posts.md) genealogy. Two things worth stealing for OpenHands harness work:
1. **Don't over-compress feedback.** This is the sharp, actionable finding — the reason to prefer full traces over distilled "lessons" when the optimization target is *code*, not a prompt. It's a direct counterpoint/complement to GEPA (`../skills/gepa-reflective-prompt-evolution-can-outperform-reinforcement-learning.md`), which optimizes *prompts* from natural-language reflection; Meta-Harness argues that for harness *code* you need the raw traces, not the reflection.
2. **Filesystem-as-memory for the optimizer.** The proposer reads prior source+scores+traces off disk — the same substrate our own [notes+retrieval condensation proposal](../../blogs/interesting-posts.md) leans on (OpenHands already persists the full event stream). Pairs with Darwin Gödel Machine (`darwin-godel-machine-open-ended-evolution-self-improving-agents.md`): DGM uses an evolutionary archive + benchmark scoring; Meta-Harness uses an agentic proposer + explicit scorer with uncompressed trace access. Same "optimize the harness, freeze the weights" thesis, two search strategies. Khattab (DSPy/GEPA) is an author, so this is the same lineage arguing its own next step.

## Caveats / Limits

- Reported on classification / math-RAG / TerminalBench-2; agentic-coding gains are the least quantified in the abstract.
- Cost of the outer loop (running an agent that repeatedly proposes + scores full harnesses) is not the headline and matters for practical adoption.
- "Fixed model" is the point, but also the ceiling: it optimizes context/retrieval, not reasoning.

## Beyond the paper

Reference code (the harness that searches over harnesses) is open-sourced; linked from the collection's "Beyond the papers" section.

## Follow-up: learning the revision procedure

- [Harness Learning Enables Generalizable Test-Time Adaptation](harness-learning-generalizable-test-time-adaptation.md) (2026-09-28; full read) trains a small proposer with execution-based RL, then repeatedly revises a frozen solver’s harness on unseen task families. This adds transfer of a **learned editing procedure**, alongside Meta-Harness’s agentic code-search approach. Its supplied reports are externally generated; it does not test replacing an agentic optimizer’s trace filesystem with compressed reports. Strong fixed-tool-loop baselines and unmatched feedback/compute budgets limit claims about general superiority.

## Follow-up: specialize while keeping the base

- [Object-Oriented Harness](object-oriented-harness-specialization-routing.md) (2610.28380v1; full read) compares a global Meta-Harness adaptation with inherited specialists and frozen trajectory-informed routing on disjoint discovery/test splits. Its strongest OOD result is **all-base reuse**, not transfer of learned specialist code. The follow-up notes that Meta-Harness’s TerminalBench-2 discovery experiment uses the same tasks for search and evaluation; do not generalize the original coding score into held-out transfer evidence. OO’s cluster-local evaluations, router/base execution and single-search inheritance ablation require separate compute and causal caveats.
