# Long-Context and Prompting Papers

## Benchmarks and Evaluations
- [Analyzing the Performance of Large Language Models on Code Summarization](https://aclanthology.org/2024.lrec-main.89.pdf)
- [Michelangelo: Long Context Evaluations Beyond Haystacks via Latent Structure Queries](https://arxiv.org/abs/2409.12640)
- [NLPerturbator: Studying the Robustness of Code LLMs to Natural Language Variations](https://arxiv.org/abs/2406.19783)
- [Knowing When to Ask: Bridging Large Language Models and Data](https://docs.datacommons.org/papers/DataGemma-FullPaper.pdf)
- [Fact, Fetch, and Reason: A Unified Evaluation of RAG](https://arxiv.org/abs/2409.12941)
- [HELMET: How to Evaluate Long-Context Language Models Effectively and Thoroughly](https://arxiv.org/abs/2410.02694)
- [LLMs Know More Than They Show: On the Intrinsic Representation of LLM Hallucinations](https://arxiv.org/abs/2410.02707)
- [Why Think Step by Step? Reasoning Emerges from the Locality of Experience](https://arxiv.org/abs/2304.03843)
- [Lost in the Middle: How Language Models Use Long Contexts](https://arxiv.org/abs/2307.03172)
- [Promptagator: Few-shot Dense Retrieval From 8 Examples](https://arxiv.org/abs/2209.11755)
- [LLMs Still Can’t Plan; Can LRMs? Preliminary Evaluation of OpenAI’s o1 on PlanBench](https://arxiv.org/abs/2409.13373)
- [MLE-Bench: Evaluating Machine Learning Agents on Machine Learning Engineering](https://arxiv.org/abs/2410.07095)

## Prompting and Reasoning
- [Minstrel: Structural Prompt Generation with Multi-Agents Coordination for Non-AI Experts](https://arxiv.org/abs/2409.13449)
- [Let’s Verify Step by Step](https://arxiv.org/abs/2305.20050)
- [On the Limitations of Compute Thresholds as a Governance Strategy](https://arxiv.org/abs/2407.05694)
- [Implicit Search via Discrete Diffusion: A Study on Chess](https://openreview.net/pdf?id=A9y3LFX4ds) — anonymous, under double-blind review.

## Additional Technical References
- [The Platonic Representation Hypothesis](https://arxiv.org/abs/2405.07987)
- [Playing Atari with Deep Reinforcement Learning](https://paperswithcode.com/paper/playing-atari-with-deep-reinforcement) — origin of the DQN line that inspired o1-style reasoning.
- [Large Language Model as a Policy Teacher for Training Reinforcement Learning Agents](https://arxiv.org/abs/2311.13373)
- [Assisting in Writing Wikipedia-like Articles From Scratch with Large Language Models](https://arxiv.org/abs/2402.14207) — additional discussion in this [tweet thread](https://x.com/lateinteraction/status/1840445257655464318).
- [Sparse Autoencoders Reveal Temporal Difference Learning in Large Language Models](https://arxiv.org/abs/2410.01280)
- [The Difficulties of Executing Simple Algorithms: Why Brains Make Mistakes Computers Don’t](http://sapir.psych.wisc.edu/papers/lupyan_2013.pdf)

## Prompt Engineering Notes
(References from *Embodied LLM Agents Learn to Cooperate in Organized Teams*.)

Language models are sensitive to prompts. Prompt format heavily influences performance, so research has explored:
- heuristic prompt search using the model’s own knowledge,
- first-order methods such as soft prompt tuning,
- prefix tuning for lightweight adaptation.

This work focuses on interpretable natural-language prompts, drawing on insights from Yang et al. (2023), Zhou et al. (2023), and Pryzant et al. (2023).

### Further Reading
- [G-EVAL: NLG Evaluation Using GPT-4 with Better Human Alignment](https://arxiv.org/abs/2303.16634)
- [BERTScore: Evaluating Text Generation with BERT](https://arxiv.org/abs/1904.09675)
- [ROUGE: A Package for Automatic Evaluation of Summaries](https://aclanthology.org/W04-1013/)
- [SummEval: Re-evaluating Summarization Evaluation](https://aclanthology.org/2021.tacl-1.24) 