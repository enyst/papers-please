---
title: "Poster: ClawdGo: Endogenous Security Awareness Training for Autonomous AI Agents"
authors:
  - Jiaqi Li
  - Yang Zhao
  - Bin Sun
  - Yang Yu
  - Jian Chang
  - Lidong Zhai
arxiv_id: "2604.24020"
arxiv_url: "https://arxiv.org/abs/2604.24020"
published: "2026-04-27"
updated: "2026-04-27"
source: "arXiv"
project: "prompt-injection"
scope_note: "initial sweep"
agent_setting: "LLM agents with tool use and/or persistent state"
defense_approach: "endogenous-awareness"
defense_type: "Train the agent itself to recognize and resist injection attempts"
tags:
  - prompt-injection
  - defense
  - security-awareness
  - endogenous
  - agent-training
categories:
  - cs.CR
  - cs.AI
---

- **One-line take:** Instead of external guardrails, teach the agent to smell danger — endogenous security awareness.
- **Defense approach:** Train the agent itself to recognize and resist injection attempts
- **Pros:** No external infrastructure needed; agent-native; can adapt to novel attacks
- **Cons:** Still probabilistic; can be overridden by strong enough injections; hard to validate exhaustively
- **Abstract-level summary:** Autonomous AI agents deployed on platforms such as OpenClaw face prompt injection, memory poisoning, supply-chain attacks, and social engineering, yet existing defences address only the platform perimeter, leaving the agent's own threat judgement entirely untrained. We present ClawdGo, a framework for endogenous security awareness training: we teach the agent to recognise and reason about threats from the inside, at inference time, with no model modification. Four contributions are introduced: TLDT (Three-Layer Domain Taxonomy) organises 12 trainable dimensions across Self-Defence, Owner-Prote
