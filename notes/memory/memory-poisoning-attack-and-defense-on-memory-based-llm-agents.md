---
title: "Memory Poisoning Attack and Defense on Memory Based LLM-Agents"
authors:
  - Balachandra Devarangadi Sunil
  - Isheeta Sinha
  - Piyush Maheshwari
  - Shantanu Todmal
  - Shreyan Mallik
  - Shuchi Mishra
arxiv_id: "2601.05504"
arxiv_url: "https://arxiv.org/abs/2601.05504"
published: "2026-01-09"
updated: "2026-01-12"
source: "arXiv"
project: "memory"
scope_note: "pass-two security include"
agent_setting: "memory-based LLM agents in realistic EHR-style deployments"
memory_mechanism: "Studies how malicious content can be written into persistent memory and later retrieved, and evaluates moderation plus sanitization defenses."
icl_relevance: "medium"
tags:
  - agent-memory
  - security
  - memory-poisoning
  - defense
categories:
  - cs.CR
  - cs.MA
---

- **One-line take:** Shows that persistent memory is not just a capability boost but also a durable attack surface.
- **What it stores:** Long-term task memories that may contain both legitimate clinical context and attacker-injected instructions.
- **How memory is used at inference time:** Studies how malicious content can be written into persistent memory and later retrieved, and evaluates moderation plus sanitization defenses.
- **Why it matters for this sub-project:** Important for the corpus because any serious deployed-memory design has to account for poisoning, trust calibration, and retrieval-time filtering.
- **Caveats / limits:** The experiments are domain-specific and defense-centric, so this is more about securing memory systems than inventing new memory representations.
- **Abstract-level summary:** Large language model agents equipped with persistent memory are vulnerable to memory poisoning attacks, where adversaries inject malicious instructions through query only interactions that corrupt the agents long term memory and influence future responses. Recent work demonstrated that the MINJA (Memory Injection Attack) achieves over 95 % injection success rate and 70 % attack success rate under idealized conditions. However, the robustness of these attacks in realistic deployments and effective defensive mechanisms remain understudied. This work addresses these gaps through systematic empirical evaluation of memory poisoning attacks and defenses in Electronic Health Record (EHR) agents. We investigate attack robustness by varying three critical dimensions: initial memory state, number of indication prompts, and retrieval parameters. Our experiments on GPT-4o-mini, Gemini-2.0-Flash and Llama-3.1-8B-Instruct models using MIMIC-III clinical data reveal that realistic conditions with pre-existing legitimate memories dramatically reduce attack effectiveness. We then propose and evaluate two novel defense mechanisms: (1) Input/Output Moderation using composite trust scoring across multiple orthogonal signals, and (2) Memory Sanitization with trust-aware retrieval employing temporal decay and pattern-based filtering. Our defense evaluation reveals that effective memory sanitization requires careful trust threshold calibration to prevent both overly conservative rejection (blocking all entries) and insufficient filtering (missing subtle attacks), establishing important baselines for future adaptive defense mechanisms. These findings provide crucial insights for securing memory-augmented LLM agents in production environments.
