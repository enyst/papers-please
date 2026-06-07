---
title: "GuardNet: Ensemble Strategies of Shallow Neural Networks for Robust Prompt Injection and Jailbreak Detection"
authors:
  - Paulo Ricardo Ferreira Neves
  - Edson Rodrigues da Cruz Filho
  - Paulo Henrique Eleuterio Falsetti
  - João Vitor Pavan
  - Ian Degaspari
  - Henrique Vieira Laturrague
  - Patrick Vieira Laturrague
  - Guilherme Nielsen Dias
  - Marccello Wilson Perez Berto
  - Gustavo Voltani Von Atzingen
arxiv_id: "2606.05566"
arxiv_url: "https://arxiv.org/abs/2606.05566"
published: "2026-06-04"
updated: "2026-06-04"
source: "arXiv"
project: "prompt-injection"
scope_note: "initial sweep"
agent_setting: "LLM agents with tool use and/or persistent state"
defense_approach: "detection-classifier"
defense_type: "Shallow neural network ensemble for detecting injection/jailbreak attempts"
tags:
  - prompt-injection
  - detection
  - classifier
  - ensemble
  - guardrail
categories:
  - cs.AI
  - cs.CR
---

- **One-line take:** Lightweight neural classifiers that flag injections before they reach the model — fast and cheap.
- **Defense approach:** Shallow neural network ensemble for detecting injection/jailbreak attempts
- **Pros:** Low latency; works as a pre-filter; ensemble reduces false negatives; model-agnostic
- **Cons:** Probabilistic (can be evaded); needs training data; false positives block legitimate queries; arms race with attackers
- **Abstract-level summary:** Large Language Models (LLMs) have transformed natural language processing, but they remain vulnerable to Prompt Injection (PI) and Jailbreak (JB) attacks. In addition, benchmark evaluations may be affected by contamination and partial information leakage, compromising performance estimates. This work presents GuardNet, a guardrail system based on an ensemble of shallow neural networks (BiLSTMs) with approximately 47 million parameters. We investigate the hypothesis that robustness in adversarial scenarios depends more on the diversity of example coverage and threshold calibration than on model
