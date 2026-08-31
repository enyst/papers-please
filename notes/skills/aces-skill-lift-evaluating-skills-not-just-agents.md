# ACES / Skill Lift: Evaluating Skills, Not Just Agents

**Paper:** [arXiv:2608.20614](https://arxiv.org/abs/2608.20614) — "Evaluating Skills, Not Just Agents: Agentic Continuous Evaluation of Skills"
**Authors:** Christopher Kevin, Narendran Raghavan, Jean-Francois Puget, Roshni Malani, Meghana Puvvadi, Moshe Abramovitch, Mohit Gupta, Rama Akkiraju (**NVIDIA**)
**Date:** 2026-08-20 · **Code:** NVIDIA SkillEvaluator (open source)
**Flagged by:** @dair_ai top-papers-of-the-week (#2).

## One-Line Summary

The gate most teams use to approve a shared skill — a **scanner** that checks structure/style/security — **barely predicts whether the skill actually helps** (Spearman ρ = 0.14 vs. LLM-judge quality). Instead, measure **Skill Lift**: run the same task twice, once with the skill loaded and once without, same model/sandbox/workspace/scorer, and diff what the agent completed.

## The Core Argument

Enterprise agent programs are moving to production, where reusable skills/tools/workflow packages get reviewed. Current gates **scan the artifact** (structure, style, security) but don't answer the deployment question: *does this capability package help a live agent complete tasks under the same model, sandbox, and grading?*

Their measurement: on **145 real skills** (internal + public catalogs), structural-scan scores correlate with LLM-judge quality at **ρ = 0.14** — i.e. passing the scanner tells you the skill is well-formatted, essentially nothing about whether it works.

## The Method: ACES + Skill Lift

- **ACES (Agentic Continuous Evaluation of Skills):** a repository-native framework that evaluates skills as *executable agent artifacts*, not documents.
- **Paired live trials:** run each task **with** and **without** the target skill under a fixed model/sandbox/workspace/scorer; **Skill Lift = the delta** in completion.
- **ATIF (Agent Trajectory Interchange Format):** normalizes trajectories so a skill's lift in **Claude Code** can be compared against its lift in **Cursor** — cross-harness comparison.
- Six default runtime metrics; supports comparing baseline / skill / bundle / team-skill / plugin targets.

## Key Results

- Scan-vs-quality correlation **ρ = 0.14** (scans measure a *complementary* facet, not quality).
- **947 scored paired cases** from 58/64 production skills across **four harnesses**: mean composite Skill Lift **0.2134** (95% CI [0.1967, 0.2301]); mean outcome-only lift 0.1799; composite lift **positive in 72.8%** of paired cases.
- Largest process-metric gains in **skill execution, behavior check, skill efficiency** — signals about discovery, routing, workflow-following, tool use that *document scans cannot observe*.

## Why It Matters To Us (SmolPaws)

- **Direct hit on how we vet skills.** SmolPaws has a `security-scan` skill and a growing skill library. This says: a scan is necessary hygiene but **near-useless as a quality gate**. If we ever gate skills on scan alone, we're gating on formatting.
- **Adopt the paired-run design.** "Run the task with and without the skill, diff the outcome" is a cheap, honest way to know if a SmolPaws skill actually earns its context cost — and it's exactly the kind of thing our dreaming/self-eval loop could automate.
- **Slots into the guardrail-tier debate** (`../agentic-engineering/two-camps-synthesis-vitor-balocco.md`): the *scanner* is a weak (structural) rail; *Skill Lift* is an outcome measurement. Don't confuse "passes the linter" with "helps."
- **Cross-harness comparability (ATIF)** is relevant if we ever run skills across OpenHands + other harnesses and want apples-to-apples.

## Where It's Thin / Skeptic's Notes

- **Paired runs cost 2× compute** per evaluated skill, plus a scorer — real overhead at library scale (though far cheaper than shipping a useless skill).
- **The "quality" ground truth is an LLM judge** — so ρ=0.14 is scan-vs-*judge*, not scan-vs-*reality*. Still damning, but the judge is itself imperfect (see the Netflix "judge lifecycle" paper #1).
- **Enterprise framing** (NVIDIA, production catalogs); the mechanism generalizes, the specific metrics are theirs.

## Related

- `../memory/wikiskill-compiling-agent-experience-into-persistent-knowledge-for-skill-evolution.md` — evolving skills; Skill Lift is how you'd *evaluate* each evolution.
- `evomal-self-poisoning-in-self-evolving-coding-agents.md` — the security side of shared skill libraries (scans miss this too).
- `../agentic-engineering/` — guardrail tiering; measure outcomes, not documents.
