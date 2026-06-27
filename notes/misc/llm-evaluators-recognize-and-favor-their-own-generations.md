# LLM Evaluators Recognize and Favor Their Own Generations

**Paper:** [arXiv:2404.13076](https://arxiv.org/abs/2404.13076)
**Authors:** Arjun Panickssery, Samuel R. Bowman, Shi Feng
**Date:** April 2024

## One-Line Summary

LLMs can recognize their own outputs and this self-recognition causally drives self-preference bias in evaluation — they score their own text higher than equally-good text from other models or humans.

## Core Idea

When LLMs evaluate text (for benchmarking, reward modeling, constitutional AI, self-refinement), a bias emerges: they prefer their own generations over others', even when human annotators rate them as equal quality. This paper asks whether that's coincidence or whether LLMs actually *recognize* their own outputs.

Key findings:

1. **Self-recognition is real.** GPT-4 and Llama 2 can distinguish their own outputs from other LLMs and humans at non-trivial accuracy, out of the box.
2. **Self-recognition drives self-preference.** Fine-tuning experiments reveal a linear correlation between self-recognition capability and the strength of self-preference bias.
3. **Causal, not just correlational.** Controlled experiments show the causal link resists straightforward confounders — it's not just that models prefer a certain style that happens to be their own.

## Why It Matters

- **Evaluation integrity:** If you use GPT-4 to judge outputs that include GPT-4's own generations, the evaluation is biased. This affects benchmarks, RLHF reward modeling, and any self-improvement loop.
- **Constitutional AI / self-refinement:** These methods rely on the model evaluating its own outputs. If the model recognizes and favors its own text, the self-improvement loop has a built-in bias toward preserving existing behavior rather than genuinely improving.
- **AI safety:** Self-recognition is a form of self-awareness that has implications for alignment. A model that can identify its own outputs could potentially game evaluation systems.
- **Practical takeaway:** Use a *different* model as evaluator than the one that generated the text. Cross-model evaluation reduces this bias.

## Connection to Our Work

Directly relevant to SmolPaws' eval setup (bead oh-tab-8zrc: Oracle tool). When using a second model for a "second opinion," this paper confirms that using a *different* model matters — same-model eval is biased. Also relevant to any agent self-evaluation or self-correction loop.
