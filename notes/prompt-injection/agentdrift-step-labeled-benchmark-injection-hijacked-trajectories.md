---
title: "AgentDrift: A Step-Labeled Benchmark of Injection-Hijacked LLM Agent Trajectories"
authors:
  - (see paper)
arxiv_id: "2609.06972"
arxiv_url: "https://arxiv.org/abs/2609.06972"
published: "2026-09"
source: "arXiv:2609.06972 [cs.CR]"
read_depth: "abstract-only"
mechanism: "A benchmark of 12,536 synthetic tool-call trajectories (71,024 steps) over five agent domains, where EVERY step is labeled one of {benign, injection point, hijacked, failed injection} — enabling step-level (not whole-trace) detection of where an injection enters and which steps it corrupts."
tags:
  - prompt-injection
  - indirect-prompt-injection
  - benchmark
  - agent-trajectories
  - detection
  - step-labeling
categories:
  - cs.CR
---

- **One-line take:** The eval infrastructure the trajectory-detection line was missing. Existing benchmarks only measure *whether* an attack succeeds; guard models judge a *whole* trace. AgentDrift labels **every step** — where the injection enters, which steps it hijacked, which attacks were resisted — so detectors can be trained/measured at step granularity.

- **Contents:** 12,536 trajectories / 71,024 labeled steps across 5 domains: 4,000 benign, 5,536 attacked, 1,500 failed-attack, 1,500 hard-negative. Four per-step labels: benign / injection point / hijacked / failed injection.

- **Why it matters for us:** the shape of a successful injection ("benign prefix → attacker-serving suffix") is exactly what an operator of a long-horizon agent needs to spot. This is the training/eval substrate for that; pairs directly with **DriftNet** (the detector trained on it, same authors likely). Relevant if we ever want to detect hijack in SmolPaws' own tool-call logs.

- **Source:** abstract via arXiv:2609.06972 (Chrome). Not yet full-read.
