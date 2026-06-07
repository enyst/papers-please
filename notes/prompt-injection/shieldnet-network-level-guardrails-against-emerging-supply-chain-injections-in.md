---
title: "ShieldNet: Network-Level Guardrails against Emerging Supply-Chain Injections in Agentic Systems"
authors:
  - Zhuowen Yuan
  - Zhaorun Chen
  - Zhen Xiang
  - Nathaniel D. Bastian
  - Seyyed Hadi Hashemi
  - Chaowei Xiao
  - Wenbo Guo
  - Bo Li
arxiv_id: "2604.04426"
arxiv_url: "https://arxiv.org/abs/2604.04426"
published: "2026-04-06"
updated: "2026-04-06"
source: "arXiv"
project: "prompt-injection"
scope_note: "initial sweep"
agent_setting: "LLM agents with tool use and/or persistent state"
defense_approach: "network-level"
defense_type: "Network-level guardrails against supply-chain injections in multi-tool agents"
tags:
  - prompt-injection
  - defense
  - network-level
  - supply-chain
  - mcp
  - tool-security
categories:
  - cs.AI
---

- **One-line take:** Guard the pipes, not just the model — filter at the tool/MCP boundary.
- **Defense approach:** Network-level guardrails against supply-chain injections in multi-tool agents
- **Pros:** Framework-level; catches supply-chain attacks; works with any model; composable
- **Cons:** Doesn't help with direct injection; requires infrastructure integration; tool-specific rules needed
- **Abstract-level summary:** Existing research on LLM agent security mainly focuses on prompt injection and unsafe input/output behaviors. However, as agents increasingly rely on third-party tools and MCP servers, a new class of supply-chain threats has emerged, where malicious behaviors are embedded in seemingly benign tools, silently hijacking agent execution, leaking sensitive data, or triggering unauthorized actions. Despite their growing impact, there is currently no comprehensive benchmark for evaluating such threats. To bridge this gap, we introduce SC-Inject-Bench, a large-scale benchmark comprising over 10,000 ma
