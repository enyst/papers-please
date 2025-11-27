# Obsidian Paper Digests

## Attention and Transformer Foundations
- Bahdanau et al. 2014 — [*Neural Machine Translation by Jointly Learning to Align and Translate*](https://arxiv.org/abs/1409.0473) kicked off the attention wave cited in the notes.
- Devlin et al. 2018 — [*BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding*](https://arxiv.org/abs/1810.04805) marked the tipping point where self-supervised learning plus transformers went mainstream.
- Self-attention enforces permutation equivariance by comparing every token pair, enabling order-agnostic reasoning inside a transformer block.

## Evaluation, Long Context, and Reasoning
- *Analyzing the Performance of Large Language Models on Code Summarization* (ACL 2024) — benchmark coverage for code summarization quality.
- [*Michelangelo: Long Context Evaluations Beyond Haystacks via Latent Structure Queries*](https://arxiv.org/abs/2409.12640).
- [*NLPerturbator: Studying the Robustness of Code LLMs to Natural Language Variations*](https://arxiv.org/abs/2406.19783).
- *Knowing When to Ask – Bridging Large Language Models and Data* (DataCommons technical report) on routing questions between free-form reasoning and structured knowledge.
- [*Fact, Fetch, and Reason: A Unified Evaluation of RAG*](https://arxiv.org/abs/2409.12941).
- [*HELMET: How to Evaluate Long-Context Language Models Effectively and Thoroughly*](https://arxiv.org/abs/2410.02694).
- [*LLMs Know More Than They Show: On the Intrinsic Representation of LLM Hallucinations*](https://arxiv.org/abs/2410.02707).
- [*Why think step by step? Reasoning emerges from the locality of experience*](https://arxiv.org/abs/2304.03843).
- [*Lost in the Middle: How Language Models Use Long Contexts*](https://arxiv.org/abs/2307.03172).
- [*Promptagator: Few-shot Dense Retrieval From 8 Examples*](https://arxiv.org/abs/2209.11755).
- *LLMs STILL CAN'T PLAN; CAN LRMS?* — PlanBench commentary evaluating OpenAI o1 on structured planning tasks.

## Memory and Retrieval-Augmented Generation
- [*MemoRAG: Moving towards Next-Gen RAG Via Memory-Inspired Knowledge Discovery*](https://arxiv.org/abs/2409.05591).
- [*Retrieval Augmented Generation or Long-Context LLMs? A Comprehensive Study and Hybrid Approach*](https://arxiv.org/abs/2407.16833) introduces Self-Route to decide between RAG and long-context inference.
- [*Memory 3: Language Modeling with Explicit Memory*](https://arxiv.org/abs/2407.01178).
- [*Astute RAG: Overcoming Imperfect Retrieval Augmentation and Knowledge Conflicts for Large Language Models*](https://arxiv.org/abs/2410.07176).
- [*Contextual Document Embeddings*](https://arxiv.org/abs/2410.02525).
- [*Agent Workflow Memory*](https://arxiv.org/abs/2409.07429).
- [*ScienceAgentBench: Toward Rigorous Assessment of Language Agents for Data-Driven Scientific Discovery*](https://arxiv.org/abs/2410.05080) — includes OpenHands in the benchmark discussion.

## Prompting Techniques Mentioned
- [*Chain-of-Thought Prompting Elicits Reasoning in Large Language Models*](https://arxiv.org/abs/2201.11903).
- [*Tree of Thoughts: Deliberate Problem Solving with Large Language Models*](https://arxiv.org/abs/2305.10601).
- [*Self-Reflection: Refining Tool-Augmented Reasoning in Language Models*](https://arxiv.org/abs/2405.06682).
- [*Self-Contrast: Aligning Reasoning in Large Language Models via Internal Contrastive Explanations*](https://arxiv.org/abs/2401.02009).
- [*Think Before You Speak: Training Language Models With Pause Tokens*](https://arxiv.org/abs/2311.07445) — highlights the CSIM prompting template (empathy, topic transitions, proactive questions, concept guidance, frequent summaries).
