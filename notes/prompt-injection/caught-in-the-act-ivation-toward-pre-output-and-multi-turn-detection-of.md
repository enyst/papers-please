---
title: "Caught in the Act(ivation): Toward Pre-Output and Multi-Turn Detection of Credential Exfiltration by LLM Agents"
authors:
  - Kargi Chauhan
  - Pratibha Revankar
arxiv_id: "2606.04141"
arxiv_url: "https://arxiv.org/abs/2606.04141"
published: "2026-06-02"
updated: "2026-06-02"
source: "arXiv"
project: "prompt-injection"
scope_note: "initial sweep"
agent_setting: "LLM agents with tool use and/or persistent state"
defense_approach: "activation-detection"
defense_type: "Pre-output detection via model activations — catch exfiltration before it happens"
tags:
  - prompt-injection
  - detection
  - activation-analysis
  - credential-exfiltration
  - pre-output
categories:
  - cs.CR
  - cs.AI
---

- **One-line take:** Look at what the model is thinking (activations), not just what it says — detect attacks mid-inference.
- **Defense approach:** Pre-output detection via model activations — catch exfiltration before it happens
- **Pros:** Catches attacks before output; works for multi-turn exfiltration; deeper signal than text-level detection
- **Cons:** Requires access to model internals (white-box); may not transfer across models; adds inference latency
- **Abstract-level summary:** LLM agents often place sensitive credentials in the same context window as untrusted retrieved content, creating a direct path for indirect prompt injection to induce credential exfiltration. We study this failure mode through three complementary defenses. First, we ask whether activation probes can detect credential access before output tokens are emitted. Second, we construct honeytokens from format-specific character models and calibrate detection with split conformal prediction. Third, we treat multi-turn exfiltration as a cumulative information-flow problem and track an estimated leakage 
