---
title: "Reflexion: Language Agents with Verbal Reinforcement Learning"
authors:
  - Noah Shinn
  - Federico Cassano
  - Edward Berman
  - Ashwin Gopinath
  - Karthik Narasimhan
  - Shunyu Yao
arxiv_id: "2303.11366"
arxiv_url: "https://arxiv.org/abs/2303.11366"
published: "2023-03-20"
updated: "2023-10-10"
source: "arXiv"
project: "memory"
scope_note: "core include"
agent_setting: "general language agents for coding, reasoning, and sequential decision making"
memory_mechanism: "Stores natural-language self-reflections derived from task feedback in an episodic buffer and reuses them in later prompts."
icl_relevance: "high"
tags:
  - agent-memory
  - episodic-memory
  - reflective-memory
  - icl-heavy
categories:
  - cs.AI
  - cs.CL
  - cs.LG
---

- **One-line take:** A foundational paper for experience-as-text memory: the agent improves across trials by remembering verbal critiques instead of updating weights.
- **What it stores:** Short textual reflections distilled from success/failure signals and prior trajectories.
- **How memory is used at inference time:** Stores natural-language self-reflections derived from task feedback in an episodic buffer and reuses them in later prompts.
- **Why it matters for this sub-project:** This is one of the clearest demonstrations that agent memory can live entirely in prompt-time language, making it a key ancestor of later ICL-style memory systems.
- **Caveats / limits:** The memory is shallow and unstructured; usefulness depends on the quality of reflections and can degrade as the buffer grows noisier.
- **Abstract-level summary:** Large language models (LLMs) have been increasingly used to interact with external environments (e.g., games, compilers, APIs) as goal-driven agents. However, it remains challenging for these language agents to quickly and efficiently learn from trial-and-error as traditional reinforcement learning methods require extensive training samples and expensive model fine-tuning. We propose Reflexion, a novel framework to reinforce language agents not by updating weights, but instead through linguistic feedback. Concretely, Reflexion agents verbally reflect on task feedback signals, then maintain their own reflective text in an episodic memory buffer to induce better decision-making in subsequent trials. Reflexion is flexible enough to incorporate various types (scalar values or free-form language) and sources (external or internally simulated) of feedback signals, and obtains significant improvements over a baseline agent across diverse tasks (sequential decision-making, coding, language reasoning). For example, Reflexion achieves a 91% pass@1 accuracy on the HumanEval coding benchmark, surpassing the previous state-of-the-art GPT-4 that achieves 80%. We also conduct ablation and analysis studies using different feedback signals, feedback incorporation methods, and agent types, and provide insights into how they affect performance.
