---
title: "Agent Workflow Memory"
authors:
  - Zora Zhiruo Wang
  - Jiayuan Mao
  - Daniel Fried
  - Graham Neubig
arxiv_id: "2409.07429"
arxiv_url: "https://arxiv.org/abs/2409.07429"
published: "2024-09-11"
updated: "2024-09-11"
source: "arXiv"
project: "memory"
scope_note: "core include"
agent_setting: "long-horizon web navigation agents"
memory_mechanism: "Induces reusable workflows from prior trajectories and selectively injects them to guide future agent generations in offline or online mode."
icl_relevance: "high"
tags:
  - agent-memory
  - workflow-memory
  - web-agents
  - icl-heavy
categories:
  - cs.CL
---

- **One-line take:** Treats memory as reusable routines rather than isolated facts, which is especially compelling for web and tool-using agents.
- **What it stores:** Workflow templates abstracted from successful action trajectories.
- **How memory is used at inference time:** Induces reusable workflows from prior trajectories and selectively injects them to guide future agent generations in offline or online mode.
- **Why it matters for this sub-project:** This is one of the cleanest papers on memory as action structure, not just memory as factual recall.
- **Caveats / limits:** It shines when tasks share recurring procedural skeletons; its benefits may drop when tasks are highly novel or idiosyncratic.
- **Abstract-level summary:** Despite the potential of language model-based agents to solve real-world tasks such as web navigation, current methods still struggle with long-horizon tasks with complex action trajectories. In contrast, humans can flexibly solve complex tasks by learning reusable task workflows from past experiences and using them to guide future actions. To build agents that can similarly benefit from this process, we introduce Agent Workflow Memory (AWM), a method for inducing commonly reused routines, i.e., workflows, and selectively providing workflows to the agent to guide subsequent generations. AWM flexibly applies to both offline and online scenarios, where agents induce workflows from training examples beforehand or from test queries on the fly. We experiment on two major web navigation benchmarks -- Mind2Web and WebArena -- that collectively cover 1000+ tasks from 200+ domains across travel, shopping, and social media, among others. AWM substantially improves the baseline results by 24.6% and 51.1% relative success rate on Mind2Web and WebArena while reducing the number of steps taken to solve WebArena tasks successfully. Furthermore, online AWM robustly generalizes in cross-task, website, and domain evaluations, surpassing baselines from 8.9 to 14.0 absolute points as train-test task distribution gaps widen.
