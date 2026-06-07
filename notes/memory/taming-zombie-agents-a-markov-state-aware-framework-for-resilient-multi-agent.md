---
title: "Taming "Zombie'' Agents: A Markov State-Aware Framework for Resilient Multi-Agent Evolution"
authors:
  - Taolin Zhang
  - Pukun Zhao
  - Qizhou Chen
  - Jiuheng Wan
  - Chen Chen
  - Xiaofeng He
  - Chengyu Wang
  - Richang Hong
arxiv_id: "2605.17348"
arxiv_url: "https://arxiv.org/abs/2605.17348"
published: "2026-05-17"
updated: "2026-05-17"
source: "arXiv"
project: "memory"
scope_note: "pass-four include (Q2 2026 sweep)"
agent_setting: "LLM-based multi-agent systems with evolving collaboration graphs"
memory_mechanism: "Uses Markov state transitions (Active/Standby/Terminated) to manage agent memory propagation, preventing premature pruning of temporarily underperforming agents."
icl_relevance: "medium"
tags:
  - agent-memory
  - multi-agent
  - state-management
  - resilience
categories:
  - cs.CL
---

- **One-line take:** Not every struggling agent is dead — state-aware transitions let agents recover from transient failures.
- **What it stores:** See memory_mechanism above.
- **How memory is used at inference time:** Uses Markov state transitions (Active/Standby/Terminated) to manage agent memory propagation, preventing premature pruning of temporarily underperforming agents.
- **Why it matters for this sub-project:** Addresses the zombie agent problem from the defense side — managing rather than just detecting compromised state.
- **Caveats / limits:** Newly published (Q2 2026); peer validation pending.
- **Abstract-level summary:** Recent advancements in LLM-based multi-agent systems have demonstrated remarkable collaborative capabilities across complex tasks. To improve overall efficiency, existing methods often rely on aggressive graph evolution among agents (e.g., node or edge pruning), which risks prematurely discarding valuable agents due to transient issues such as hallucinations or temporary knowledge gaps. However, such hard pruning overlooks the potential for ``zombie'' agents to recover and contribute in subsequent discussion rounds. In this paper, we propose AgentRevive, a Markov state-aware framework for resilient multi-agent evolution. Our approach dynamically manages agent collaboration through soft state transitions, implemented via two key components: (1) State-Aware Policy Learning: Agent states are divided into ``Active'', ``Standby'', and ``Terminated'' states, selectively propagating messages based on agent memory. The policy employs a risk estimator to optimize agent state transitions by assessing hallucination risk, minimizing the influence of unreliable nodes while safeguarding valuable ones. (2) State-Aware Edge Optimization: Subgraph edges are pruned according to states learned from the policy, permanently removing ``Terminated'' nodes and retaining ``Standby'' nodes for subsequent rounds to assess their potential future contributions. Extensive experiments on general reasoning, domain-specific, and hallucination challenge tasks show that our method consistently outperforms strong baselines and significantly reduces token consumption through state-aware agent scheduling.
