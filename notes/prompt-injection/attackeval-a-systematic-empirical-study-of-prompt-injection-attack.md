---
title: "AttackEval: A Systematic Empirical Study of Prompt Injection Attack Effectiveness Against Large Language Models"
authors:
  - Jackson Wang
arxiv_id: "2604.03598"
arxiv_url: "https://arxiv.org/abs/2604.03598"
published: "2026-04-04"
updated: "2026-04-04"
source: "arXiv"
project: "prompt-injection"
scope_note: "initial sweep"
agent_setting: "LLM agents with tool use and/or persistent state"
defense_approach: "attack-evaluation"
defense_type: "Systematic evaluation of which injection strategies work and why"
tags:
  - prompt-injection
  - attack-evaluation
  - empirical-study
  - benchmark
categories:
  - cs.CR
---

- **One-line take:** Finally studies the attack side systematically — which injections work, which fail, and why.
- **Defense approach:** Systematic evaluation of which injection strategies work and why
- **Pros:** Attack-side focus fills a gap; empirical grounding; helps understand what defenses need to handle
- **Cons:** Attack-focused, not a defense; may lag behind latest attack innovations
- **Abstract-level summary:** Prompt injection has emerged as a critical vulnerability in large language model (LLM) deployments, yet existing research is heavily weighted toward defenses. The attack side -- specifically, which injection strategies are most effective and why -- remains insufficiently studied.We address this gap with AttackEval, a systematic empirical study of prompt injection attack effectiveness. We construct a taxonomy of ten attack categories organized into three parent groups (Syntactic, Contextual, and Semantic/Social), populate each category with 25 carefully crafted prompts (250 total), and evaluate
