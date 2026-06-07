---
title: "VeriGuard: Enhancing LLM Agent Safety via Verified Code Generation"
authors:
  - Wenyue Hua
  - Xianjun Yang
  - Mingyu Jin
  - Zelong Li
  - Yongfeng Zhang
arxiv_id: "2510.05156"
arxiv_url: "https://arxiv.org/abs/2510.05156"
published: "2025-10-03"
updated: "2025-10-03"
source: "arXiv"
project: "prompt-enforcement"
scope_note: "initial sweep"
agent_setting: "autonomous AI agents in sensitive domains such as healthcare"
mechanism: "Generates formally verified code wrappers around agent actions that guarantee adherence to predefined safety constraints."
tags:
  - agent-safety
  - formal-verification
  - code-generation
  - safety-constraints
  - deterministic-enforcement
categories:
  - cs.AI
  - cs.CL
---

- **One-line take:** Instead of hoping the LLM follows rules, generate verified code that makes rule-breaking impossible.
- **How it enforces safety:** Generates formally verified code wrappers around agent actions that guarantee adherence to predefined safety constraints.
- **Why it matters:** Strongest version of the compile-to-enforcement idea — uses formal verification to guarantee compliance.
- **Caveats / limits:** Newly collected; needs deeper reading.
- **Abstract-level summary:** The deployment of autonomous AI agents in sensitive domains, such as healthcare, introduces critical risks to safety, security, and privacy. These agents may deviate from user objectives, violate data handling policies, or be compromised by adversarial attacks. Mitigating these dangers necessitates a mechanism to formally guarantee that an agent's actions adhere to predefined safety constraints. We propose VeriGuard, a framework that enhances LLM agent safety via verified code generation.
