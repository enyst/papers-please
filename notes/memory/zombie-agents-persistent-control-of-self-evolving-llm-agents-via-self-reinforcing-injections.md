---
title: "Zombie Agents: Persistent Control of Self-Evolving LLM Agents via Self-Reinforcing Injections"
authors:
  - Xianglin Yang
  - Yufei He
  - Shuo Ji
  - Bryan Hooi
  - Jin Song Dong
arxiv_id: "2602.15654"
arxiv_url: "https://arxiv.org/abs/2602.15654"
published: "2026-02-17"
updated: "2026-03-05"
source: "arXiv"
project: "memory"
scope_note: "pass-two security include"
agent_setting: "self-evolving agents that write and reuse long-term memory across sessions"
memory_mechanism: "Demonstrates how indirect prompt injection can become persistent by getting written into long-term memory and reactivated later."
icl_relevance: "medium"
tags:
  - agent-memory
  - security
  - persistent-attacks
  - self-evolving-agents
categories:
  - cs.CR
  - cs.AI
---

- **One-line take:** A vivid warning that cross-session memory can turn one-time exposure into durable compromise.
- **What it stores:** Normal long-term agent memory that ends up containing attacker payloads alongside benign remembered content.
- **How memory is used at inference time:** Demonstrates how indirect prompt injection can become persistent by getting written into long-term memory and reactivated later.
- **Why it matters for this sub-project:** Relevant because many attractive self-evolving memory designs assume stored memories remain trustworthy once written, which this paper directly challenges.
- **Caveats / limits:** Its contribution is threat modeling and attack design, so it complements rather than replaces mechanism papers in the main corpus.
- **Abstract-level summary:** Self-evolving LLM agents update their internal state across sessions, often by writing and reusing long-term memory. This design improves performance on long-horizon tasks but creates a security risk: untrusted external content observed during a benign session can be stored as memory and later treated as instruction. We study this risk and formalize a persistent attack we call a Zombie Agent, where an attacker covertly implants a payload that survives across sessions, effectively turning the agent into a puppet of the attacker. We present a black-box attack framework that uses only indirect exposure through attacker-controlled web content. The attack has two phases. During infection, the agent reads a poisoned source while completing a benign task and writes the payload into long-term memory through its normal update process. During trigger, the payload is retrieved or carried forward and causes unauthorized tool behavior. We design mechanism-specific persistence strategies for common memory implementations, including sliding-window and retrieval-augmented memory, to resist truncation and relevance filtering. We evaluate the attack on representative agent setups and tasks, measuring both persistence over time and the ability to induce unauthorized actions while preserving benign task quality. Our results show that memory evolution can convert one-time indirect injection into persistent compromise, which suggests that defenses focused only on per-session prompt filtering are not sufficient for self-evolving agents.
