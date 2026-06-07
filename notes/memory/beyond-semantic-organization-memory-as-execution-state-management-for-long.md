---
title: "Beyond Semantic Organization: Memory as Execution State Management for Long-Horizon Agents"
authors:
  - Yaoqi Chen
  - Haibin Lai
  - Yuru Feng
  - Chuyu Han
  - Qianxi Zhang
  - Baotong Lu
  - Menghao Li
  - Xinjiang Wang
  - Zhirui Wang
  - Shusen Xu
  - Zengzhong Li
  - Zewen Jin
  - Hao Wu
  - Cheng Li
  - Qi Chen
arxiv_id: "2606.06090"
arxiv_url: "https://arxiv.org/abs/2606.06090"
published: "2026-06-04"
updated: "2026-06-04"
source: "arXiv"
project: "memory"
scope_note: "pass-four include (Q2 2026 sweep)"
agent_setting: "long-horizon agents managing complex execution state"
memory_mechanism: "Reframes memory not as semantic retrieval but as execution state management — tracking goals, progress, dependencies, and context."
icl_relevance: "medium"
tags:
  - agent-memory
  - execution-state
  - long-horizon-agents
  - state-management
categories:
  - cs.AI
---

- **One-line take:** A philosophical shift: memory is not a knowledge base to search but an execution state to manage.
- **What it stores:** See memory_mechanism above.
- **How memory is used at inference time:** Reframes memory not as semantic retrieval but as execution state management — tracking goals, progress, dependencies, and context.
- **Why it matters for this sub-project:** Challenges the retrieval-centric view of memory that dominates the literature.
- **Caveats / limits:** Newly published (Q2 2026); peer validation pending.
- **Abstract-level summary:** LLM-based agents increasingly tackle long-horizon tasks with interdependent decisions, where each action reshapes future constraints and intermediate errors can cascade. Existing RAG and agent memory systems organize histories by semantic similarity, retrieving content-relevant entries at decision time. We argue that this design mismatches execution-state dependencies: it fragments decision trajectories and mixes valid and erroneous traces, hindering coherent state reconstruction and error isolation. We propose MAGE (Memory as Agent-Guided Exploration), an active execution-state manager that stores interactions in a hierarchical state tree. The agent derives its state from the active root-to-current path, combining subgoal summaries, recent traces, and hints from prior branches. Four coupled operations maintain the tree: Grow records new traces, Compress summarizes completed subgoals, Maintain validates summaries, and Revise restores a target boundary and resumes on a new branch. This design bounds context growth while preserving state integrity and isolating flawed segments from the active path. Experiments on MemoryArena show that MAGE improves the average task success rate by 7.8--20.4 pp over baselines, while reducing token consumption by 55.1%.
