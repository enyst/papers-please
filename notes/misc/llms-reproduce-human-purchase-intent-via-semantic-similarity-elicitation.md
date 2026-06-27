# LLMs Reproduce Human Purchase Intent via Semantic Similarity Elicitation of Likert Ratings

**Paper:** [arXiv:2510.08338](https://arxiv.org/abs/2510.08338)
**Authors:** Benjamin F. Maier, Ulf Aslak, Luca Fiaschi, Nina Rismal, Kemble Fletcher, Christian C. Luhmann, Robbie Dow, Kli Pappas, Thomas V. Wiecki
**Date:** October 2025 (v3)

## One-Line Summary

A method to get realistic Likert-scale survey distributions from LLMs by eliciting text responses and mapping them to ratings via embedding similarity — hitting 90% of human test-retest reliability on real consumer surveys.

## Core Idea

Asking LLMs directly for numerical ratings produces unrealistic distributions (they cluster around specific values, don't match human variance). The insight: don't ask for numbers. Ask for text, then convert.

**Semantic Similarity Rating (SSR):**
1. Give the LLM a product and survey question
2. Elicit a free-text response (natural language opinion)
3. Embed that response + embed reference statements for each Likert point (e.g., "I would definitely buy this" = 5, "I would never buy this" = 1)
4. Map to the Likert scale via cosine similarity between response embedding and reference embeddings
5. Aggregate across multiple synthetic respondents to get a distribution

**Results on 57 real consumer surveys (9,300 human responses):**
- Achieves 90% of human test-retest reliability
- Realistic response distributions (KS similarity > 0.85 vs human data)
- Bonus: synthetic respondents provide qualitative feedback explaining their ratings

## Why It Matters

- **Synthetic data that actually works.** Most LLM-as-survey-respondent approaches fail because the distributions are wrong. SSR fixes this by decoupling generation (text) from measurement (embedding similarity).
- **The trick is indirect elicitation.** Don't ask the model for the thing you want directly — ask for something adjacent and derive the answer. This pattern generalizes beyond surveys.
- **Scale economics.** Consumer research is a billion-dollar industry built on panels of ~1000 people. If synthetic respondents can approximate real ones at 90% reliability, that's a massive cost reduction for screening/early-stage research.
- **Qualitative + quantitative.** Human surveys give you a number. SSR gives you a number *and* an explanation. That's strictly more useful for product teams.

## Interesting Details

- The embedding-based mapping is the key innovation. Direct numerical elicitation from LLMs has been tried and fails. The semantic detour works because LLMs are better at expressing opinions in natural language than in calibrated numbers.
- KS similarity > 0.85 means the synthetic distribution shape closely matches the real one — not just the mean, but the spread and skew.
- 90% of test-retest reliability is a meaningful bar. Human surveys themselves aren't perfectly reproducible; hitting 90% of that ceiling means the synthetic noise is comparable to human noise.

## Connection to Our Work

Indirect elicitation pattern is relevant to agent evaluation. Instead of asking an agent "rate your confidence 1-5," have it explain its reasoning and derive confidence from the text. Connects to the self-preference bias paper (2404.13076) — indirect measurement may also reduce self-recognition artifacts.

Also relevant to Liberty Labs product thinking: if agents can simulate realistic user personas, that's useful for UX testing and product validation before building.
