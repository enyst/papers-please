---
title: "ECLIPSE: Self-Evolving Stealthy Prompt Injection Attack against Long-Horizon Agentic Systems"
authors:
  - (see paper)
arxiv_id: "2608.30441"
arxiv_url: "https://arxiv.org/abs/2608.30441"
published: "2026-08"
source: "arXiv:2608.30441 [cs.CR]"
read_depth: "abstract-only"
mechanism: "A self-evolving attack for long-horizon agents (Codex/Claude Code/OpenClaw-style). Combines direct user-prompt injection with indirect tool-side injection: sandbox-verifies candidate tool chains, renders a verified chain as a natural one-shot prompt, then steers the target via Static Workflow Encoding embedded in tool outputs."
tags:
  - prompt-injection
  - indirect-prompt-injection
  - attack
  - long-horizon-agents
  - stealth
  - self-evolving
categories:
  - cs.CR
---

- **One-line take:** Attacks tuned for **long-horizon agents** (many tool calls). Existing injections trade off detectability vs reliability — one explicit malicious instruction is easy to catch; intent spread across stages is hard to complete. ECLIPSE gets both stealth *and* reliability by sandbox-verifying a working tool chain first, then delivering it as a natural one-shot prompt + tool-side steering.

- **Mechanism:** (1) *Stealthy Attack Trajectory Synthesis* — a sandbox generates and iteratively verifies candidate tool chains, then renders a verified chain as a natural one-shot direct instruction. (2) *Tool-Chain Steering* — transfers that plan to the target via **Static Workflow Encoding** embedded in tool outputs (indirect channel).

- **Why it matters for us:** SmolPaws *is* a long-horizon, many-tool agent with automations reading untrusted inbound (Slack/AgentMail/GitHub) — exactly ECLIPSE's target profile. The "verify in sandbox, then deliver as one clean prompt" trick defeats naive single-instruction detectors. Part of the 2026 "attacks adapt / self-evolve" cluster (with CoRL, test-time-search).

- **Source:** abstract via arXiv:2608.30441 (Chrome; abstract partially truncated on capture). Not yet full-read.
