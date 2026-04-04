---
title: "Voyager: An Open-Ended Embodied Agent with Large Language Models"
authors:
  - Guanzhi Wang
  - Yuqi Xie
  - Yunfan Jiang
  - Ajay Mandlekar
  - Chaowei Xiao
  - Yuke Zhu
  - Linxi Fan
  - Anima Anandkumar
arxiv_id: "2305.16291"
arxiv_url: "https://arxiv.org/abs/2305.16291"
published: "2023-05-25"
updated: "2023-10-19"
source: "arXiv"
project: "memory"
scope_note: "core include"
agent_setting: "open-ended embodied Minecraft agent"
memory_mechanism: "Builds an ever-growing skill library of executable code and retrieves those skills as reusable action abstractions during future tasks."
icl_relevance: "high"
tags:
  - agent-memory
  - embodied-agent
  - skill-library
  - icl-heavy
categories:
  - cs.AI
  - cs.LG
---

- **One-line take:** A canonical example of memory as reusable executable skill rather than raw text or retrieved facts.
- **What it stores:** Executable code skills and supporting trajectory information from prior exploration.
- **How memory is used at inference time:** Builds an ever-growing skill library of executable code and retrieves those skills as reusable action abstractions during future tasks.
- **Why it matters for this sub-project:** Shows a strong ICL-adjacent pattern: instead of updating weights, the agent accumulates reusable procedures and conditions future prompting on them.
- **Caveats / limits:** The memory is highly domain-shaped and optimized for embodied Minecraft tasks, so transfer to general assistants is indirect.
- **Abstract-level summary:** We introduce Voyager, the first LLM-powered embodied lifelong learning agent in Minecraft that continuously explores the world, acquires diverse skills, and makes novel discoveries without human intervention. Voyager consists of three key components: 1) an automatic curriculum that maximizes exploration, 2) an ever-growing skill library of executable code for storing and retrieving complex behaviors, and 3) a new iterative prompting mechanism that incorporates environment feedback, execution errors, and self-verification for program improvement. Voyager interacts with GPT-4 via blackbox queries, which bypasses the need for model parameter fine-tuning. The skills developed by Voyager are temporally extended, interpretable, and compositional, which compounds the agent's abilities rapidly and alleviates catastrophic forgetting. Empirically, Voyager shows strong in-context lifelong learning capability and exhibits exceptional proficiency in playing Minecraft. It obtains 3.3x more unique items, travels 2.3x longer distances, and unlocks key tech tree milestones up to 15.3x faster than prior SOTA. Voyager is able to utilize the learned skill library in a new Minecraft world to solve novel tasks from scratch, while other techniques struggle to generalize. We open-source our full codebase and prompts at https://voyager.minedojo.org/.
