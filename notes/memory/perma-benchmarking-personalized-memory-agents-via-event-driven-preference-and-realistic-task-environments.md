---
title: "PERMA: Benchmarking Personalized Memory Agents via Event-Driven Preference and Realistic Task Environments"
authors:
  - Shuochen Liu
  - Junyi Zhu
  - Long Shu
  - Junda Lin
  - Yuhao Chen
  - Haotian Zhang
  - Chao Zhang
  - Derong Xu
  - Jia Li
  - Bo Tang
  - Zhiyu Li
  - Feiyu Xiong
  - Enhong Chen
  - Tong Xu
arxiv_id: "2603.23231"
arxiv_url: "https://arxiv.org/abs/2603.23231"
published: "2026-03-24"
updated: "2026-03-24"
source: "arXiv"
project: "memory"
scope_note: "pass-two meta include: benchmark"
agent_setting: "personalized agents whose memory must track evolving user preferences over time"
memory_mechanism: "Benchmark paper focused on persona consistency and temporally evolving preferences rather than static preference recall."
icl_relevance: "medium"
tags:
  - agent-memory
  - benchmark
  - personalization
  - persona-memory
categories:
  - cs.AI
---

- **One-line take:** Pushes personalized memory evaluation beyond needle-in-a-haystack preference lookup.
- **What it stores:** The benchmark assumes systems store temporally ordered user events, preferences, and cross-domain persona cues.
- **How memory is used at inference time:** Benchmark paper focused on persona consistency and temporally evolving preferences rather than static preference recall.
- **Why it matters for this sub-project:** Helpful because many deployed assistants care about preference coherence over time, which is not well measured by ordinary long-context QA benchmarks.
- **Caveats / limits:** Again, it is a measurement contribution rather than a new memory architecture, and its findings are strongest in personalization-heavy settings.
- **Abstract-level summary:** Empowering large language models with long-term memory is crucial for building agents that adapt to users' evolving needs. However, prior evaluations typically interleave preference-related dialogues with irrelevant conversations, reducing the task to needle-in-a-haystack retrieval while ignoring relationships between events that drive the evolution of user preferences. Such settings overlook a fundamental characteristic of real-world personalization: preferences emerge gradually and accumulate across interactions within noisy contexts. To bridge this gap, we introduce PERMA, a benchmark designed to evaluate persona consistency over time beyond static preference recall. Additionally, we incorporate (1) text variability and (2) linguistic alignment to simulate erratic user inputs and individual idiolects in real-world data. PERMA consists of temporally ordered interaction events spanning multiple sessions and domains, with preference-related queries inserted over time. We design both multiple-choice and interactive tasks to probe the model's understanding of persona along the interaction timeline. Experiments demonstrate that by linking related interactions, advanced memory systems can extract more precise preferences and reduce token consumption, outperforming traditional semantic retrieval of raw dialogues. Nevertheless, they still struggle to maintain a coherent persona across temporal depth and cross-domain interference, highlighting the need for more robust personalized memory management in agents. Our code and data are open-sourced at https://github.com/PolarisLiu1/PERMA.
