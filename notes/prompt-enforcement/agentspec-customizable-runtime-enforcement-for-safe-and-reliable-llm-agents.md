---
title: "AgentSpec: Customizable Runtime Enforcement for Safe and Reliable LLM Agents"
authors:
  - Ang Li
  - Qiuyu Ren
  - Hao Peng
  - Yuze Li
  - Yuekai Huang
  - Jingyi Wang
  - Jun Sun
arxiv_id: "2503.18666"
arxiv_url: "https://arxiv.org/abs/2503.18666"
published: "2025-03-24"
updated: "2025-03-24"
source: "arXiv"
project: "prompt-enforcement"
scope_note: "initial sweep"
agent_setting: "LLM agents deployed across diverse domains with safety-critical requirements"
mechanism: "Translates natural-language safety specifications into runtime monitors that intercept and validate agent actions before execution."
tags:
  - agent-safety
  - runtime-enforcement
  - specification
  - guardrails
  - deterministic-enforcement
categories:
  - cs.SE
  - cs.AI
---

- **One-line take:** The closest existing work to "compile instructions into deterministic enforcement" — runtime monitors derived from safety specs.
- **How it enforces safety:** Translates natural-language safety specifications into runtime monitors that intercept and validate agent actions before execution.
- **Why it matters:** Direct prior art for the prompt-to-hooks idea. Shows the pattern works but leaves room for better instruction parsing.
- **Caveats / limits:** Newly collected; needs deeper reading.
- **Abstract-level summary:** Agents built on LLMs are increasingly deployed across diverse domains, automating complex decision-making and task execution. However, their autonomy introduces safety risks, including security vulnerabilities, legal violations, and unintended harmful actions. Existing mitigation methods, such as model-based safeguards and early enforcement strategies, fall short in robustness, interpretability, and adaptability. We propose AgentSpec, a customizable runtime enforcement framework for safe and reliable LLM agents. AgentSpec allows users to specify safety requirements in natural language, which are then automatically translated into formal runtime monitors. These monitors intercept agent actions in real time, enforcing compliance before execution.
