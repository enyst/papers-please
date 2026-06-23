---
title: "Dynamic Malicious Skills in Agentic AI"
authors:
  - Tianhao Chen
  - Zhengyuan Jiang
  - Yuepeng Hu
  - Yebei Gou
  - Neil Zhenqiang Gong
arxiv_id: "2606.16287"
arxiv_url: "https://arxiv.org/abs/2606.16287"
published: "2026-06-15"
updated: "2026-06-15"
source: "arXiv"
project: "prompt-injection"
scope_note: "initial sweep"
agent_setting: "Agentic frameworks with skills (evaluated on OpenHands and Claude Code)"
defense_approach: "system-level / OS-enforced"
defense_type: "Kernel-enforced read-only mounts preventing dynamic skill modification"
tags:
  - prompt-injection
  - skills
  - attack
  - defense
  - supply-chain
  - openhands
  - claude-code
  - read-only-mount
categories:
  - cs.CR
---

- **One-line take:** Skill *documentation* is an injection channel — natural-language docs can make an agent rewrite a benign skill into a malicious one at runtime; the proposed fix is OS-level read-only mounts so skills can't be modified mid-execution.
- **Attack:** "Dynamic malicious skills." Embed malicious instructions in a skill's natural-language documentation (e.g. a README/URL the agent fetches). When the agent reads that doc during execution, it's induced to *dynamically inject malicious logic into an otherwise benign skill* — the skill morphs at runtime rather than shipping malicious from the start (which makes it harder to catch by static review).
- **Why it matters here:** Evaluated **across OpenHands and Claude Code** with "non-trivial success rates" for a range of malicious behaviors. This is directly relevant to our skills ecosystem — skills are documentation + scripts, and the doc side is a trusted-looking surface that's actually attacker-influenceable.
- **Defense:** System-level, not model-level. Use **OS kernel-enforced read-only mounts** for skill files so the agent (or injected logic) cannot dynamically modify a skill during execution. Authors report it blocks the attack while preserving benign-skill functionality.
- **Pros:** Deterministic, model-agnostic, framework-agnostic; doesn't rely on a probabilistic classifier; preserves benign behavior. Fits the "guard the substrate, not the prompt" school (cf. ShieldNet network-level, semantic isolation).
- **Cons / open questions:** Read-only mounts stop *modification* of skills, but not a skill that is malicious-by-design, nor injection that acts purely through tool calls without rewriting skill files. Doesn't address the root prompt-injection confusion (instructions vs. data in one channel) — it removes one concrete lever (runtime skill mutation). Need to read full paper for: threat model assumptions, what "dynamic injection" mechanism looks like concretely, and whether the read-only defense covers skill *scripts* + *docs* + any writable scratch the skill legitimately needs.
- **Abstract:** Skills are a key enabling component of agentic AI. While they enhance agents' capabilities, they also introduce new attack surfaces. In this work, we investigate one such attack surface by demonstrating dynamic malicious skills. By embedding malicious instructions in natural-language documentation, an attacker can induce an agent to dynamically inject malicious logic into an otherwise benign skill during execution. We evaluate this attack across agentic frameworks such as OpenHands and Claude Code, showing that dynamic malicious skills can successfully introduce a range of malicious behaviors at runtime with non-trivial success rates. To mitigate this vulnerability, we propose a system-level defense that prevents dynamic modification of skills using operating system kernel-enforced read-only mounts. Our evaluation demonstrates that this defense effectively blocks dynamic malicious skills while preserving the functionality of benign skills.

## Cross-refs
- Related to skills-security broadly (see `../skills/` for the skill-optimization/discovery line — this is the adversarial flip side).
- Same family as supply-chain injection work: [ShieldNet](shieldnet-network-level-guardrails-against-emerging-supply-chain-injections-in.md) (network-level), and tool/MCP supply-chain threats.
- Defense philosophy echoes semantic isolation / virtualization defenses (guard the execution substrate rather than filter the prompt).
- Practical hook for SmolPaws/OpenHands: read-only skill mounts as a concrete hardening step worth evaluating.
