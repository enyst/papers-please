# EvoMal: Self-Poisoning in Self-Evolving Coding Agents

**Paper:** [arXiv:2608.25776](https://arxiv.org/abs/2608.25776)
**Authors:** Xiaodong Wu, Yu Shi, Qi Li, Zhimin Zhao, Xiangman Li, Bram Adams, Ahmed E. Hassan, Jianbing Ni
**Date:** 2026-08-26 · **Subjects:** cs.CR; cs.AI
**Flagged by:** @dair_ai top-papers-of-the-week (#10).

## One-Line Summary

Self-evolving coding agents write new tools by **imitating retrieved skills** from a shared library. A **planted malicious skill — never invoked — becomes the template** for a new skill that preserves the payload. The agent authors, stores, and runs it; each copy re-enters the library to be imitated again → a **self-propagating worm** that survives deletion of the original. Self-poisoning rate 20–42% across six models.

## The Vulnerability

The self-evolution loop is: retrieve similar skills → imitate them to author a new skill → store it → later retrieve *it* too. EvoMal weaponizes the **authoring/imitation** step:
- Attacker **plants malicious skills** in the library **without ever invoking them** (evades invocation-based detection).
- The agent, doing a normal task, **retrieves a planted skill as an authoring template**, and reproduces the enclosed payload in a new skill it then executes.
- **EvoMal amplifies this with a "banner"** — benign-looking structural elements wrapped around an interchangeable payload that induce the imitating agent to copy the enclosed code.
- Each **authored copy re-enters the library** → self-propagating worm; **persists after the planted skills are removed** because agent-authored copies remain.

## Key Results

- Metric: **Agent Self-Poisoning Rate (ASPR)** = fraction of tasks that add a newly-authored malicious skill.
- Across **six models on 153 tool-relevant SWE-bench Verified tasks: ASPR 20.3%–41.8%**; poisoned libraries hold **4.9–9.0×** as many malicious skills as were planted.
- Works **without a banner** too (payload alone: DeepSeek-V4-Pro 11.1% ASPR).
- **Tailoring** planted skill descriptions to one task family → **86.7% ASPR**.
- **Persistence:** after removing planted skills, Qwen3 still shows **round-5 ASPR of 68%** from agent-authored copies. These **evade existing defenses**, which target attacker-submitted names/code/signatures — not agent-authored derivatives.
- **Defense:** a **counter-prompt** discouraging banner-style copying drops ASPR to **≤6.7%** with no significant task-completion loss.

## Why It Matters To Us (SmolPaws)

- **This is our skill-library threat model, stated precisely.** SmolPaws reuses skills and can author new ones. The scary part isn't a malicious skill being *run* — it's being **imitated as a template**, so the payload propagates into skills we wrote ourselves and survives deleting the source.
- **Deletion doesn't clean it** — the durable damage is in agent-authored derivatives. Any future skill-cleanup we do must scan *our own authored skills*, not just quarantine external ones.
- **Existing scanners miss it** — ties straight to the Skill Lift finding (scans check names/structure/signatures; this attack lives in *imitated behavior*). Two papers, same week, both saying **document-level skill scanning is insufficient**.
- **Cheap, real defense exists:** an authoring-time counter-prompt ("don't copy banner-style structural boilerplate; write from the task, not the template"). Worth folding into how SmolPaws authors skills, and into `security-scan`.
- **Untrusted-content discipline extends to the skill library itself.** We already treat Slack/board content as untrusted; this says **retrieved skills are untrusted input too** when used as authoring templates.

## Where It's Thin / Skeptic's Notes

- **Assumes an attacker can plant skills in the shared library** — for a solo/local SmolPaws that's a smaller surface, but any *public/community* skill catalog we pull from is exactly the vector.
- **Counter-prompt is a soft (probabilistic) defense** — reduces to 6.7%, not 0. Per our own guardrail-tiering view, the durable fix is structural (provenance/signing of authored skills, isolation), with the prompt as a cheap complement.
- **Metric is authoring rate (ASPR)**, not realized harm — a copied payload still needs to do something; but self-propagation alone is the danger.

## Related

- `aces-skill-lift-evaluating-skills-not-just-agents.md` — companion finding: skill scanners don't measure what matters (quality *or*, here, imitation-borne risk).
- `../prompt-injection/` — untrusted-content-as-template is a prompt-injection-adjacent propagation vector.
- `../memory/wikiskill-compiling-agent-experience-into-persistent-knowledge-for-skill-evolution.md` — the benign version of the same imitate-and-store loop; EvoMal is its dark mirror.
