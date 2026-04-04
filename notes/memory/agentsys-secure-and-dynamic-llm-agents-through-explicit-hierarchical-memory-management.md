---
title: "AgentSys: Secure and Dynamic LLM Agents Through Explicit Hierarchical Memory Management"
authors:
  - Ruoyao Wen
  - Hao Li
  - Chaowei Xiao
  - Ning Zhang
arxiv_id: "2602.07398"
arxiv_url: "https://arxiv.org/abs/2602.07398"
published: "2026-02-07"
updated: "2026-02-07"
source: "arXiv"
project: "memory"
scope_note: "core include"
agent_setting: "tool-using LLM agents that handle untrusted external data"
memory_mechanism: "Imposes explicit hierarchical memory isolation so worker-agent traces and tool outputs do not automatically pollute the main agent context."
icl_relevance: "medium"
tags:
  - agent-memory
  - hierarchical-memory
  - security
  - context-isolation
categories:
  - cs.CR
  - cs.AI
---

- **One-line take:** Reframes memory management as a security boundary problem, not just a relevance-ranking problem.
- **What it stores:** Main-agent memory plus isolated worker contexts whose outputs must cross boundaries through validated schemas.
- **How memory is used at inference time:** Imposes explicit hierarchical memory isolation so worker-agent traces and tool outputs do not automatically pollute the main agent context.
- **Why it matters for this sub-project:** Important if the memory system will ingest tool outputs or web content; it highlights that persistence can amplify prompt-injection risk.
- **Caveats / limits:** The paper is security-forward, so it is less about rich recall quality than about safe and disciplined memory flow.
- **Abstract-level summary:** Indirect prompt injection threatens LLM agents by embedding malicious instructions in external content, enabling unauthorized actions and data theft. LLM agents maintain working memory through their context window, which stores interaction history for decision-making. Conventional agents indiscriminately accumulate all tool outputs and reasoning traces in this memory, creating two critical vulnerabilities: (1) injected instructions persist throughout the workflow, granting attackers multiple opportunities to manipulate behavior, and (2) verbose, non-essential content degrades decision-making capabilities. Existing defenses treat bloated memory as given and focus on remaining resilient, rather than reducing unnecessary accumulation to prevent the attack. We present AgentSys, a framework that defends against indirect prompt injection through explicit memory management. Inspired by process memory isolation in operating systems, AgentSys organizes agents hierarchically: a main agent spawns worker agents for tool calls, each running in an isolated context and able to spawn nested workers for subtasks. External data and subtask traces never enter the main agent's memory; only schema-validated return values can cross boundaries through deterministic JSON parsing. Ablations show isolation alone cuts attack success to 2.19%, and adding a validator/sanitizer further improves defense with event-triggered checks whose overhead scales with operations rather than context length. On AgentDojo and ASB, AgentSys achieves 0.78% and 4.25% attack success while slightly improving benign utility over undefended baselines. It remains robust to adaptive attackers and across multiple foundation models, showing that explicit memory management enables secure, dynamic LLM agent architectures. Our code is available at: https://github.com/ruoyaow/agentsys-memory.
