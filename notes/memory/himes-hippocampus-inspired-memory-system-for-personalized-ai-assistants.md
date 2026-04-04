---
title: "HiMeS: Hippocampus-inspired Memory System for Personalized AI Assistants"
authors:
  - Hailong Li
  - Feifei Li
  - Wenhui Que
  - Xingyu Fan
arxiv_id: "2601.06152"
arxiv_url: "https://arxiv.org/abs/2601.06152"
published: "2026-01-06"
updated: "2026-01-06"
source: "arXiv"
project: "memory"
scope_note: "pass-three borderline include: RL-trained short-term memory extractor"
agent_setting: "personalized AI assistants and customer-service-style assistants with user-specific knowledge needs"
memory_mechanism: "Fuses short-term dialogue compression and proactive retrieval with a partitioned long-term memory network for user-specific re-ranking."
icl_relevance: "medium"
tags:
  - agent-memory
  - personalization
  - hippocampus-inspired
  - borderline-trained
categories:
  - cs.AI
---

- **One-line take:** A personalized-assistant memory stack that explicitly splits short-term and long-term roles in a hippocampus-inspired design.
- **What it stores:** Compressed recent dialogue state plus partitioned long-term user-specific memory and retrieved knowledge signals.
- **How memory is used at inference time:** Fuses short-term dialogue compression and proactive retrieval with a partitioned long-term memory network for user-specific re-ranking.
- **Why it matters for this sub-project:** Useful for breadth because it adds an industrial personalization angle and a cognitively motivated split between immediate and durable memory.
- **Caveats / limits:** The short-term memory extractor is trained end-to-end, so it sits partly outside a strict inference-only memory corpus.
- **Abstract-level summary:** Large language models (LLMs) power many interactive systems such as chatbots, customer-service agents, and personal assistants. In knowledge-intensive scenarios requiring user-specific personalization, conventional retrieval-augmented generation (RAG) pipelines exhibit limited memory capacity and insufficient coordination between retrieval mechanisms and user-specific conversational history, leading to redundant clarification, irrelevant documents, and degraded user experience. Inspired by the hippocampus-neocortex memory mechanism, we propose HiMeS, an AI-assistant architecture that fuses short-term and long-term memory. Our contributions are fourfold: (1) A short-term memory extractor is trained end-to-end with reinforcement learning to compress recent dialogue and proactively pre-retrieve documents from the knowledge base, emulating the cooperative interaction between the hippocampus and prefrontal cortex. (2) A partitioned long-term memory network stores user-specific information and re-ranks retrieved documents, simulating distributed cortical storage and memory reactivation. (3) On a real-world industrial dataset, HiMeS significantly outperforms a cascaded RAG baseline on question-answering quality. (4) Ablation studies confirm the necessity of both memory modules and suggest a practical path toward more reliable, context-aware, user-customized LLM-based assistants.
