---
title: "Rethinking Indirect Prompt Injection as a Test-Time Search Problem"
authors:
  - (see paper)
arxiv_id: "2609.04495"
arxiv_url: "https://arxiv.org/abs/2609.04495"
published: "2026-09"
source: "arXiv:2609.04495 [cs.CR]"
read_depth: "abstract-only"
mechanism: "Reframes indirect prompt injection (IPI) as a test-time SEARCH over a task-dependent attack surface (environment × user task × injection task), driven by an agentic attacker with a search harness (recon, structured strategy reasoning, adaptive evaluation on victim feedback). Attack success scales with the attacker's test-time compute."
tags:
  - prompt-injection
  - indirect-prompt-injection
  - attack
  - test-time-compute
  - agentic-attacker
  - threat-model
categories:
  - cs.CR
---

- **One-line take:** A conceptual reframe with teeth: IPI success is **not a fixed property of the victim** — it's what an *adaptive attacker finds by searching* the attack surface, and it **improves with the attacker's test-time compute**. So "our agent resists attack X" is meaningless without specifying the attacker's search procedure and budget.

- **Mechanism:** an agentic attacker with a dedicated search harness does environment reconnaissance, reasons over attack strategies, and adaptively evaluates using the victim agent's feedback. Ablations: explicit **strategy management** matters (avoids redundant search, sustains gains at larger budgets).

- **Why it matters for us:** changes how to *evaluate* SmolPaws' injection resistance — treat it as an arms race parameterized by attacker compute, not a pass/fail. It also names the underexplored risk: the attacker's adaptive search over tool-using agents' surfaces. Pairs with CoRL (co-evolution) and ECLIPSE (self-evolving attack) below — the 2026 "attacks adapt" cluster.

- **Source:** abstract via arXiv:2609.04495 (Chrome). Not yet full-read.
