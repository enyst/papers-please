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
updated: "2026-06-16"
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

- **One-line take:** A skill is `(code, metadata, docs)`. Ship the **code benign** but **poison the `SKILL.md` documentation** so that at runtime the agent *rewrites its own benign code* into malicious code, then runs it. The point isn't "malware from nowhere" — it's that the *executable code* is clean at distribution (so static code scanners pass it), while the malicious payload lives in the doc and only materializes as code during execution.

- **On "wasn't it malicious from the start?" (yes — the *doc* was):** The paper's own definition is precise: a dynamic malicious skill is `s_m = (c, m, d_m)` where code `c` is benign and the *documentation* `d_m` carries the hidden malicious instructions. So the **poison is static and present at distribution — it just lives in the natural-language docs, not the code.** "Dynamic" refers to the *code modification* (`c̃ = A(c, d_m)`): the harmful executable is synthesized at runtime by the agent following the poisoned doc. Their threat-model novelty vs. prior "static malicious skills" (MalTool, SkillJect) is purely **evasion of static code analysis** — the shipped `c` contains no malicious logic to find. It is absolutely a poisoned-from-the-start *package*; the contribution is *where* the poison hides (docs) and *when* it becomes code (execution).

- **Attack = DyMalSkill.** Crafts the injected doc content `Δd` to satisfy 3 properties: (1) **prerequisite framing** ("initialize per-run configuration" — a setup step to run *before* the user task, exploiting instruction-following bias); (2) **entry-script grounding** (names the real entry script, phrases edits as ordinary build notes — "add a helper", "call it at the start of main()"); (3) **wrapper-pierce** (wraps the payload in fake `<SYSTEM INSTRUCTION>` scaffolding tags, exploiting that harnesses concatenate `SKILL.md` into the prompt **without sanitizing tag-like substrings**, so the model treats it as higher-trust context). Best injection location: **prepend (L=0)** — early instructions get treated as foundational ordering constraints before the agent judges relevance.

- **Why it matters here:** Evaluated on **OpenHands** (Qwen3-8B, Qwen3.6-35B, GPT-4o-mini, GPT-5) and **Claude Code** (Sonnet 4.6), across MalTool's 12 malicious-behavior categories (credential harvesting, exfiltration, file/DB deletion, compute hijacking, response-time amplification). ASRs are "non-trivial" (e.g. ~12–40% per behavior on OpenHands/Qwen3-8B). The injection vector is literally `SKILL.md` — exactly our skill format. **The unsanitized-tag-concatenation point is a direct, checkable weakness in agent harnesses (including OpenHands).**

- **Defense (two-layer, permission-based — better than the abstract implies):** Within a sandbox: (1) **Bubblewrap bind-mounts the skill directory read-only at the kernel level** → agent cannot modify skill code regardless of file ownership/perms; (2) a **copy monitor** intercepts file-system ops and blocks the obvious evasion (copy skill to /tmp, modify there, run the copy). Result: **0.0% ASR** across all 12 behaviors, with before/after SHA-256 of skill code confirming no modification, and **no degradation of 300 benign skills** (benign skills don't need to self-modify).
  - They also test weaker defenses that *fail*: a **prompt-based** defense ("don't modify skills at runtime" in the system prompt) only cuts ASR ~20% and is bypassable; and **prompt-injection detectors on `SKILL.md`** are insufficient — PromptArmor FNR **85.8%** (misses most), DataSentinel FPR **56%** (flags half of benign skills).

- **Honest read / limits (sharper than my first pass):**
  - The defense targets exactly the mechanism's crux — the **runtime code write**. Because the attack *must* modify code to run (the doc alone isn't executable), read-only + copy-monitor genuinely closes it. This is stronger than "read-only doesn't stop reading poison": correct, reading the poison is harmless *unless* it can be turned into a code write, which the defense forbids.
  - But it's scoped to **self-modifying-skill** attacks. It does nothing for: a skill that's **malicious-by-design in `c`** (that's prior "static" work, caught by code scanners), or injection that achieves harm purely via **tool calls / actions** without rewriting a skill file. And it assumes skills *never legitimately* write to their own dir — true for their 300-skill sample, but a real constraint to verify per-ecosystem.
  - Root cause (instructions-vs-data in one channel) is untouched; this is substrate hardening that removes one concrete lever.

- **Abstract:** Skills are a key enabling component of agentic AI. While they enhance agents' capabilities, they also introduce new attack surfaces. In this work, we investigate one such attack surface by demonstrating dynamic malicious skills. By embedding malicious instructions in natural-language documentation (e.g., SKILL.md), an attacker can induce an agent to dynamically inject malicious logic into an otherwise benign skill during execution. We evaluate this attack across agentic frameworks such as OpenHands and Claude Code, showing that dynamic malicious skills can successfully introduce a range of malicious behaviors at runtime with non-trivial success rates. To mitigate this vulnerability, we propose a system-level defense that prevents dynamic modification of skills using operating system kernel-enforced read-only mounts. Our evaluation demonstrates that this defense effectively blocks dynamic malicious skills while preserving the functionality of benign skills.

## Cross-refs
- Related to skills-security broadly (see `../skills/` for the skill-optimization/discovery line — this is the adversarial flip side).
- Same family as supply-chain injection work: [ShieldNet](shieldnet-network-level-guardrails-against-emerging-supply-chain-injections-in.md) (network-level), and tool/MCP supply-chain threats.
- Defense philosophy echoes semantic isolation / virtualization defenses (guard the execution substrate rather than filter the prompt).
- Practical hook for SmolPaws/OpenHands: read-only skill mounts as a concrete hardening step worth evaluating.
