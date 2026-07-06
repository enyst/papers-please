---
title: "How can we assess human-agent interactions? Case studies in software agent design (PULSE)"
authors:
  - Valerie Chen
  - Rohit Malhotra
  - Xingyao Wang
  - Juan Michelini
  - Xuhui Zhou
  - Aditya Bharat Soni
  - Hoang H. Tran
  - Calvin Smith
  - Ameet Talwalkar
  - Graham Neubig
venue: arXiv
date: 2025-10-10
arxiv: "2510.09801"
url: https://arxiv.org/abs/2510.09801
tags: [evaluation, human-agent-interaction, openhands, ab-testing, memory, condenser, satisfaction]
---

# How can we assess human-agent interactions? Case studies in software agent design (PULSE)

**Paper:** [arXiv:2510.09801](https://arxiv.org/abs/2510.09801) (v3)
**Authors:** Valerie Chen (lead), Rohit Malhotra, Xingyao Wang, Juan Michelini, Xuhui Zhou, Aditya Bharat Soni, Hoang H. Tran, Calvin Smith, Ameet Talwalkar, Graham Neubig
**Date:** October 2025

## One-Line Summary

Benchmarks assume full automation and miss how agents actually get used. PULSE evaluates agent *design decisions* on real users of the OpenHands cloud platform (15k users, 36k+ sessions) by blending sparse human satisfaction ratings with an ML model's pseudo-labels — cutting confidence intervals ~40% vs a plain A/B test — and finds in-the-wild results that contradict benchmarks (notably an **anti-correlation between claude-sonnet-4 and gpt-5**).

## Why It's Here / Relevance

This is the paper behind the "A/B testing on OpenHands cloud" experiments that resurfaced in **OpenHands/extensions PR #378** (documenting automation A/B config), where Engel requested **full transparency** (LLM profile/config + conversation trajectories) for automation runs on OpenHands repos. This is the *earlier iteration* of that experiment. One of the three case studies is the **Condenser** (memory management), which is why it kept coming up.

## Core Idea: PULSE

Rigorous human-centric evaluation of agent designs without needing everyone to leave feedback:

1. **Collect user feedback** (sparse explicit satisfaction signals from real usage).
2. **Train an ML model** to predict user satisfaction from session features.
3. **Combine** real human ratings with **model-generated pseudo-labels** on the unlabeled majority to compute results.

Result: ~**40% narrower confidence intervals** than a standard A/B test on the same data — more robust conclusions from the same traffic.

Deployed in software engineering via a large web platform built on the open-source **OpenHands** agent.

## The Three Case Studies (agent design decisions varied in the wild)

- **Case Study 1 — LLM Model backbone.** Compared 3 SOTA models on agentic coding: `claude-3.7-sonnet`, `claude-4-sonnet`, and `gpt-5` (reasoning effort high). This is where the **benchmark-vs-reality gap** shows: the in-the-wild satisfaction ordering does not match benchmark ordering (anti-correlation between claude-sonnet-4 and gpt-5).
- **Case Study 2 — Planning.** Varied the planning strategy for handling complex user messages.
- **Case Study 3 — Memory Management (Condenser).** Once work segments exceed context limits (and long contexts get costly), the agent needs a memory mechanism. They A/B'd condenser settings (e.g. **Condenser 120 vs. 80** thresholds in the full results, Appendix B / Table 8).

## Key Findings

1. **PULSE ≫ vanilla A/B** for the same traffic: ~40% tighter confidence intervals by adding model pseudo-labels to sparse human ratings.
2. **Benchmarks mislead.** In-the-wild developer satisfaction is substantially discrepant from static benchmark performance — the flagship example being the **anti-correlation between claude-sonnet-4 and gpt-5**. A model that looks better on benchmarks can be worse for real users.
3. **PULSE surfaces impactful design choices** across model, planning, and memory that a benchmark-driven process would miss.

## Why It Matters

- **Evaluation of deployed agents is the real frontier.** Static benchmarks with full automation don't capture collaborative, human-in-the-loop use — where most real value (and dissatisfaction) lives.
- **Design decisions, not just model picks.** Planning strategy and memory/condenser configuration measurably move user satisfaction — harness design matters as much as model choice.
- **Directly relevant to the transparency ask.** These experiments run on OpenHands repos with real users; publishing the LLM profile/config + trajectories (as Engel requested on extensions#378, ref OpenHands/automation#221) is the open-source-consistent way to run them.

## Related

- Follow-up / sibling controlled study: [Code with Me or for Me? How Increasing AI Automation Transforms Developer Workflows](https://arxiv.org/abs/2507.08149) (Chen, Talwalkar, Brennan, Neubig).
- Context: OpenHands/extensions PR #378 (automation A/B config docs) and OpenHands/automation#221 (transparency request: LLM + trajectories).
