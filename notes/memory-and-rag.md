# Memory and RAG Papers

## Recommended by N
- Hayati et al. 2018 — Retrieval-Based Neural Code Generation
- Zhou et al. 2022 — RAG for LLMs

## Memory and Retrieval Research
- [MemoRAG: Moving Towards Next-Gen RAG Via Memory-Inspired Knowledge Discovery](https://arxiv.org/abs/2409.05591)
- [Retrieval Augmented Generation or Long-Context LLMs? A Comprehensive Study and Hybrid Approach](https://arxiv.org/abs/2407.16833) — proposes Self-Route to decide between RAG and long-context inference.
- [Memory 3: Language Modeling with Explicit Memory](https://arxiv.org/abs/2407.01178) — additional context in this [tweet thread](https://x.com/rohanpaul_ai/status/1825729380544377009?s=61).
- [Astute RAG: Overcoming Imperfect Retrieval Augmentation and Knowledge Conflicts for Large Language Models](https://arxiv.org/abs/2410.07176)
- [Contextual Document Embeddings](https://arxiv.org/abs/2410.02525) — NotebookLM notes [here](https://notebooklm.google.com/notebook/be5ded78-7fc3-4df4-b88e-3488cf50d994?authuser=1).
- [Agent Workflow Memory](https://arxiv.org/abs/2409.07429)
- [ScienceAgentBench: Toward Rigorous Assessment of Language Agents for Data-Driven Scientific Discovery](https://arxiv.org/abs/2410.05080) — mentions OpenHands as part of the evaluation suite.
- [MLE-Bench: Evaluating Machine Learning Agents on Machine Learning Engineering](https://arxiv.org/abs/2410.07095)


Language models convert prompts into tokens, process them via transformer layers, and use attention to weigh contextual relevance before decoding outputs. Randomness is governed by temperature and top-k sampling [[38](https://arxiv.org/html/2310.14735v3#bib.bib38), [39](https://arxiv.org/html/2310.14735v3#bib.bib39), [40](https://arxiv.org/html/2310.14735v3#bib.bib40), [41](https://arxiv.org/html/2310.14735v3#bib.bib41)].

### o1-Style Prompting References
1. [Chain of Thought](https://arxiv.org/abs/2201.11903) — elicits intermediate reasoning; self-consistency samples multiple traces and votes.
2. [Tree of Thoughts](https://arxiv.org/abs/2305.10601) — expands CoT into an m-ary search tree of partial solutions.
3. [Self-Reflection](https://arxiv.org/abs/2405.06682) — feeds back correctness signals before re-answering, without leaking solutions.
4. [Self-Contrast](https://arxiv.org/abs/2401.02009) — contrasts diverse prompts to build a to-do checklist for revisions.
5. [Think Before You Speak](https://arxiv.org/abs/2311.07445) — introduces CSIM prompts (empathy, topic transitions, proactive questions, concept guidance, frequent summaries) and separates inner monologue from user-facing responses.
