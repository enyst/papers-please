# Mixture-of-Models: Unifying Heterogeneous Agents via N-Way Self-Evaluating Deliberation

**Paper:** [arXiv:2601.16863](https://arxiv.org/abs/2601.16863)
**Authors:** Tims Pecerskis, Aivars Smirnovs (Peeramid Labs)
**Date:** January 2026

## One-Line Summary

Ensemble small (<20B) models via iterative deliberation rounds with peer-review voting, claim to match 100B+ frontier models on AIME and LiveCodeBench.

## Core Idea

Instead of using one big model, run multiple small models in rounds. Each round: all models generate answers, all models critique each other's answers (N-to-N peer review), a "broker" selects the best via quadratic voting, and the consensus feeds back as context for the next round. Iterate until convergence or degradation.

The paper frames this as a "Macro-Scale Semantic RNN" where the consensus state is the hidden state, looping back through a "semantic forget gate." Also frames model selection as a Knapsack Problem.

**Benchmark results:**
- AIME 2025: 84% (mid-tier ensemble) / 90% (high-perf ensemble) at peak round 6
- LiveCodeBench v5 Hard: 51.5% → 60.2% peak (vs 33% majority voting baseline)
- DarkBench safety: peer-mediated correction reduces sycophancy below individual agent scores

## What's Actually Novel

1. **Iterative recurrence over rounds** instead of single-pass ensemble. Models critique each other and refine. This is "debate" applied to inference.
2. **Empirical finding: performance peaks then degrades.** There's an optimal stopping point (~round 5-6). More rounds → sycophancy creeps in and consensus degrades. They model this with a "fatigue coefficient."
3. **Quadratic voting for consensus** — prevents a majority of mediocre models from drowning out a strong minority expert. Borrowed from mechanism design (Glen Weyl).

## Skepticism — ⚠️ Read With Caution

**This is a company paper.** Both authors are from Peeramid Labs, whose product IS this protocol. The incentive to oversell is structural.

**The terminology is grandiose.** "Cognitive Thermodynamics", "Macro-Scale Semantic RNN", "Dynamic Expertise Broker", "trustless orchestration fabric" — strip away the language and the mechanism is: run multiple models, have them critique each other, vote, repeat. That's model debate/ensemble, which is well-known. The terminological density makes it hard to separate what's actually new from what's rebranding.

**Compute cost is conspicuously absent.** Running 4 models × 7 rounds = ~28 forward passes of <20B models. That's roughly equivalent compute to several runs of a single 100B+ model. The "small models matching frontier" claim only holds if you ignore total compute budget. A fair comparison would be: given the same total FLOPS, does this beat a single large model? That comparison isn't made.

**R² ≈ 0.99 on 7 data points.** Fitting a parametric curve to 7 points and reporting high R² is not evidence of a deep theoretical framework. It's overfitting.

**Baseline selection.** They compare against individual model baselines and "naive majority voting" (33% on LiveCodeBench). But majority voting with how many samples? If you gave a single model 28 attempts and took the best, how would it compare? Best-of-N sampling is the natural baseline for inference-time compute scaling, and it's not compared.

**No public code.** For a paper about a "protocol," the absence of a public implementation is telling. They want you to use their platform.

## What's Probably Real

- Iterative deliberation between heterogeneous models does improve over single-pass. This is consistent with the broader debate/ensemble literature.
- There IS an optimal number of rounds. Sycophancy and "context noise" accumulate. This finding is useful regardless of the framing.
- Peer-mediated safety correction (models catching each other's harmful outputs) is a real effect documented elsewhere too.

## Verdict

The underlying mechanism (iterative multi-model debate) works. The paper wraps it in enough terminology and theoretical apparatus to fill a PhD thesis, which makes the actual contribution hard to evaluate. The missing compute-cost comparison is the biggest red flag — if the method costs 20x more inference compute to match a frontier model, that's not "hardware arbitrage," it's just an expensive ensemble.

Worth knowing about as a design pattern. Not worth treating as a breakthrough until independently reproduced with fair baselines.
