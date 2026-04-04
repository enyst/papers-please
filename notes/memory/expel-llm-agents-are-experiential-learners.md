---
title: "ExpeL: LLM Agents Are Experiential Learners"
authors:
  - Andrew Zhao
  - Daniel Huang
  - Quentin Xu
  - Matthieu Lin
  - Yong-Jin Liu
  - Gao Huang
arxiv_id: "2308.10144"
arxiv_url: "https://arxiv.org/abs/2308.10144"
published: "2023-08-20"
updated: "2024-12-20"
source: "arXiv"
project: "memory"
scope_note: "core include"
agent_setting: "general decision-making agents that can improve across task episodes"
memory_mechanism: "Extracts natural-language insights from accumulated experiences and recalls those insights plus prior episodes at inference time."
icl_relevance: "high"
tags:
  - agent-memory
  - experience-memory
  - icl-heavy
  - cross-trial-learning
categories:
  - cs.LG
  - cs.AI
  - cs.CL
---

- **One-line take:** Makes the case that agents can learn from prior episodes through retrieved language insights, not parameter updates.
- **What it stores:** Experience summaries, lessons, and recalled examples from previous tasks.
- **How memory is used at inference time:** Extracts natural-language insights from accumulated experiences and recalls those insights plus prior episodes at inference time.
- **Why it matters for this sub-project:** This is a direct bridge from trial history to ICL-style guidance and is especially relevant if the goal is memory as reusable task knowledge.
- **Caveats / limits:** It depends on the transferability of extracted insights and on retrieval finding the right prior experiences for the new task.
- **Abstract-level summary:** The recent surge in research interest in applying large language models (LLMs) to decision-making tasks has flourished by leveraging the extensive world knowledge embedded in LLMs. While there is a growing demand to tailor LLMs for custom decision-making tasks, finetuning them for specific tasks is resource-intensive and may diminish the model's generalization capabilities. Moreover, state-of-the-art language models like GPT-4 and Claude are primarily accessible through API calls, with their parametric weights remaining proprietary and unavailable to the public. This scenario emphasizes the growing need for new methodologies that allow learning from agent experiences without requiring parametric updates. To address these problems, we introduce the Experiential Learning (ExpeL) agent. Our agent autonomously gathers experiences and extracts knowledge using natural language from a collection of training tasks. At inference, the agent recalls its extracted insights and past experiences to make informed decisions. Our empirical results highlight the robust learning efficacy of the ExpeL agent, indicating a consistent enhancement in its performance as it accumulates experiences. We further explore the emerging capabilities and transfer learning potential of the ExpeL agent through qualitative observations and additional experiments.
