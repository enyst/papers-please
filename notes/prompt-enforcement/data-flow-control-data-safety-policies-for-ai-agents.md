---
title: "Data Flow Control: Data Safety Policies for AI Agents"
authors:
  - Various
arxiv_id: "2606.05679"
arxiv_url: "https://arxiv.org/abs/2606.05679"
published: "2026-06-04"
updated: "2026-06-04"
source: "arXiv"
project: "prompt-enforcement"
scope_note: "initial sweep"
agent_setting: "agents that generate SQL, orchestrate pipelines, and automate data analysis"
mechanism: "Enforces data safety constraints as infrastructure-level policies — the agent cannot violate privacy/regulatory rules even with correct queries."
tags:
  - agent-safety
  - data-safety
  - policy-enforcement
  - privacy
  - infrastructure
categories:
  - cs.AI
  - cs.DB
---

- **One-line take:** A correct query is not a safe query — enforce data policies at the infrastructure level.
- **How it enforces safety:** Enforces data safety constraints as infrastructure-level policies — the agent cannot violate privacy/regulatory rules even with correct queries.
- **Why it matters:** Shows how the deterministic enforcement idea applies specifically to data access and SQL generation.
- **Caveats / limits:** Newly collected; needs deeper reading.
- **Abstract-level summary:** Agents increasingly generate SQL, orchestrate pipelines, and automate data analysis on behalf of users. While recent work improves query correctness, correctness is not safety. A query may be semantically valid yet violate regulatory, privacy, or business constraints that govern how data may be combined and released.
