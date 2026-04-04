---
title: "MemoryBank: Enhancing Large Language Models with Long-Term Memory"
authors:
  - Wanjun Zhong
  - Lianghong Guo
  - Qiqi Gao
  - He Ye
  - Yanlin Wang
arxiv_id: "2305.10250"
arxiv_url: "https://arxiv.org/abs/2305.10250"
published: "2023-05-17"
updated: "2023-05-21"
source: "arXiv"
project: "memory"
scope_note: "core include"
agent_setting: "long-term companion and counseling-style conversational agents"
memory_mechanism: "Stores long-term interaction history, reinforces or forgets memories over time, and synthesizes user personality signals for retrieval."
icl_relevance: "high"
tags:
  - agent-memory
  - long-term-memory
  - dialogue
  - personalization
categories:
  - cs.CL
  - cs.AI
---

- **One-line take:** An early long-term dialogue memory system that treats persistent conversational memory as a first-class runtime component.
- **What it stores:** Conversation-derived memories plus higher-level user traits and preferences.
- **How memory is used at inference time:** Stores long-term interaction history, reinforces or forgets memories over time, and synthesizes user personality signals for retrieval.
- **Why it matters for this sub-project:** Useful as a prototype for personalized agents that need memory across weeks or months without retraining.
- **Caveats / limits:** It is chat-centric and relies on hand-designed forgetting heuristics rather than richer structured memory organization.
- **Abstract-level summary:** Revolutionary advancements in Large Language Models have drastically reshaped our interactions with artificial intelligence systems. Despite this, a notable hindrance remains-the deficiency of a long-term memory mechanism within these models. This shortfall becomes increasingly evident in situations demanding sustained interaction, such as personal companion systems and psychological counseling. Therefore, we propose MemoryBank, a novel memory mechanism tailored for LLMs. MemoryBank enables the models to summon relevant memories, continually evolve through continuous memory updates, comprehend, and adapt to a user personality by synthesizing information from past interactions. To mimic anthropomorphic behaviors and selectively preserve memory, MemoryBank incorporates a memory updating mechanism, inspired by the Ebbinghaus Forgetting Curve theory, which permits the AI to forget and reinforce memory based on time elapsed and the relative significance of the memory, thereby offering a human-like memory mechanism. MemoryBank is versatile in accommodating both closed-source models like ChatGPT and open-source models like ChatGLM. We exemplify application of MemoryBank through the creation of an LLM-based chatbot named SiliconFriend in a long-term AI Companion scenario. Further tuned with psychological dialogs, SiliconFriend displays heightened empathy in its interactions. Experiment involves both qualitative analysis with real-world user dialogs and quantitative analysis with simulated dialogs. In the latter, ChatGPT acts as users with diverse characteristics and generates long-term dialog contexts covering a wide array of topics. The results of our analysis reveal that SiliconFriend, equipped with MemoryBank, exhibits a strong capability for long-term companionship as it can provide emphatic response, recall relevant memories and understand user personality.
