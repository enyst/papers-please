---
title: "Auto-Dreamer: Learning Offline Memory Consolidation for Language Agents"
authors:
  - Chongrui Ye
  - Yuxiang Liu
  - Yu Wang
  - Haofei Yu
  - Yining Zhao
  - Ge Liu
  - Julian McAuley
  - Jiaxuan You
arxiv_id: "2605.20616"
arxiv_url: "https://arxiv.org/abs/2605.20616"
published: "2026-05-20"
updated: "2026-05-20"
source: "arXiv"
project: "memory"
scope_note: "pass-four include (Q2 2026 sweep)"
agent_setting: "language agents that accumulate experience across sessions"
memory_mechanism: "Learns an offline memory consolidation policy that decides what to keep, compress, and discard during between-session sleep-time compute."
icl_relevance: "medium"
tags:
  - agent-memory
  - memory-consolidation
  - offline-compute
  - lifelong-memory
categories:
  - cs.CL
---

- **One-line take:** The first paper to explicitly learn a consolidation policy for offline memory processing — directly validates the sleep-time compute pattern.
- **What it stores:** See memory_mechanism above.
- **How memory is used at inference time:** Learns an offline memory consolidation policy that decides what to keep, compress, and discard during between-session sleep-time compute.
- **Why it matters for this sub-project:** Directly validates our SmolPaws dreaming approach with empirical evidence that learned consolidation outperforms hand-crafted rules.
- **Caveats / limits:** Newly published (Q2 2026); peer validation pending.
- **Abstract-level summary:** Language agents increasingly operate over streams of related tasks, yet existing memory systems struggle to convert accumulated experience into reusable knowledge. Retrieval-augmented and structured memory methods record per-session observations effectively, but often couple acquisition and consolidation into a single online process, leaving the agent without a global view across sessions to discover recurring patterns, abstract shared procedures, or prune redundant entries. Inspired by complementary learning systems theory, we propose Auto-Dreamer, a learned offline consolidator for language-agent memory. Auto-Dreamer decouples fast per-session memory acquisition from slow cross-session consolidation. Given a selected working region of a typed memory bank, the consolidator treats the region as read-only evidence, performs bounded tool-use to inspect entries and provenance-linked source trajectories, and synthesizes a fresh compact replacement set that abstracts across sessions and supersedes the original region. We train Auto-Dreamer via GRPO, using end-to-end agent performance as the reward signal to learn how to consolidate memories acquired through fast online experience. Trained on ScienceWorld trajectories alone, Auto-Dreamer outperforms fixed, RL-trained, and prompted memory baselines on ScienceWorld by 7 points while using an active memory bank 12$\times$ smaller than the strongest baseline, and continues to lead on held-out ALFWorld and WebArena without retraining -- using 6$\times$ less memory than the strongest baseline on ALFWorld.
