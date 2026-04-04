---
title: "Omni-SimpleMem: Autoresearch-Guided Discovery of Lifelong Multimodal Agent Memory"
authors:
  - Jiaqi Liu
  - Zipeng Ling
  - Shi Qiu
  - Yanqing Liu
  - Siwei Han
  - Peng Xia
  - Haoqin Tu
  - Zeyu Zheng
  - Cihang Xie
  - Charles Fleming
  - Mingyu Ding
  - Huaxiu Yao
arxiv_id: "2604.01007"
arxiv_url: "https://arxiv.org/abs/2604.01007"
published: "2026-04-01"
updated: "2026-04-02"
source: "arXiv"
project: "memory"
scope_note: "core include"
agent_setting: "lifelong multimodal agents evaluated on long-horizon memory benchmarks"
memory_mechanism: "A unified multimodal memory framework discovered and iteratively improved by an autonomous research pipeline."
icl_relevance: "medium"
tags:
  - agent-memory
  - multimodal-memory
  - autoresearch
  - lifelong-memory
categories:
  - cs.AI
---

- **One-line take:** Interesting less for one neat memory primitive than for showing that autonomous research can discover strong lifelong-memory systems.
- **What it stores:** Multimodal experiences organized by the discovered memory framework.
- **How memory is used at inference time:** A unified multimodal memory framework discovered and iteratively improved by an autonomous research pipeline.
- **Why it matters for this sub-project:** Helpful as a meta-paper on how agent-memory systems may increasingly be designed and tuned by agents themselves.
- **Caveats / limits:** The contribution is partly about the discovery process, so the memory design lessons are less tidy than in more focused mechanism papers.
- **Abstract-level summary:** AI agents increasingly operate over extended time horizons, yet their ability to retain, organize, and recall multimodal experiences remains a critical bottleneck. Building effective lifelong memory requires navigating a vast design space spanning architecture, retrieval strategies, prompt engineering, and data pipelines; this space is too large and interconnected for manual exploration or traditional AutoML to explore effectively. We deploy an autonomous research pipeline to discover Omni-SimpleMem, a unified multimodal memory framework for lifelong AI agents. Starting from a naïve baseline (F1=0.117 on LoCoMo), the pipeline autonomously executes ${\sim}50$ experiments across two benchmarks, diagnosing failure modes, proposing architectural modifications, and repairing data pipeline bugs, all without human intervention in the inner loop. The resulting system achieves state-of-the-art on both benchmarks, improving F1 by +411% on LoCoMo (0.117$\to$0.598) and +214% on Mem-Gallery (0.254$\to$0.797) relative to the initial configurations. Critically, the most impactful discoveries are not hyperparameter adjustments: bug fixes (+175%), architectural changes (+44%), and prompt engineering (+188% on specific categories) each individually exceed the cumulative contribution of all hyperparameter tuning, demonstrating capabilities fundamentally beyond the reach of traditional AutoML. We provide a taxonomy of six discovery types and identify four properties that make multimodal memory particularly suited for autoresearch, offering guidance for applying autonomous research pipelines to other AI system domains. Code is available at this https://github.com/aiming-lab/SimpleMem.
