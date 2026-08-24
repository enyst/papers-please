# Sleep-time Compute: Beyond Inference Scaling at Test-time

**Paper:** [arXiv:2504.13171](https://arxiv.org/abs/2504.13171)
**Authors:** Kevin Lin, Charlie Snell, Yu Wang, Charles Packer, Sarah Wooders, Ion Stoica, Joseph E. Gonzalez (Letta / UC Berkeley)
**Date:** April 2025
**Subjects:** cs.AI, cs.CL

## One-Line Summary

Let the model "think" offline about a context *before* queries arrive — anticipate likely questions and pre-compute useful quantities — to cut test-time compute for the same accuracy by ~5x, and raise accuracy by 13–18% when you scale the offline pass.

## Core Idea

Standard test-time compute reasons hard *at query time* — high latency and cost, and it re-derives the same context facts on every query. **Sleep-time compute** splits the work: while the model is idle, it processes the raw context into a richer, pre-reasoned representation (anticipated questions, derived intermediate results). When a real query lands, it answers from that pre-computed state with far less on-the-spot reasoning.

Two regimes benefit most:
- **Predictable queries.** Efficacy correlates with how predictable the user query is given the context. If you can guess what will be asked, pre-computing pays off.
- **Many queries per context.** Offline work amortizes across related queries about the same context.

## Results

- **~5x less test-time compute** for equal accuracy on Stateful GSM-Symbolic and Stateful AIME (variants they built where context is separated from the query).
- **+13% (GSM-Symbolic) / +18% (AIME)** accuracy by scaling the sleep-time pass.
- **Multi-Query GSM-Symbolic:** amortizing the offline pass across related queries on one context cuts average cost per query by **2.5x**.
- Case study applying sleep-time compute to a realistic agentic SWE task.

## Why This Matters to SmolPaws

This is the **foundational paper behind SmolPaws' dreaming / heartbeat design.** The heartbeat's daily "dream" — reading daily memory, promoting durable facts to `MEMORY.md`, pruning, restructuring, and pre-computing "current state" notes for future conversations — *is* sleep-time compute applied to agent memory: do the expensive consolidation while idle so future conversations start with useful pre-reasoned context instead of rediscovering it.

Connections:
- Directly upstream of Letta's Context Constitution work that shapes our dreaming rules (see HEARTBEAT.md and `docs/context-constitution.md` in smolpaws).
- The "predictability of the query" finding is a useful lens: promote/pre-compute the things future-me is *likely* to need, not everything.
- Pairs with `memory/auto-dreamer-learning-offline-memory-consolidation-for-language-agents.md` — offline consolidation as a learned/deliberate step.
