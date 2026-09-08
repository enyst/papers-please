# Harness-of-Harness: Multi-Day Autonomous Software Development with Continual Improvement

**Paper:** [arXiv:2609.01481](https://arxiv.org/abs/2609.01481)
**Authors:** Haoyang Yan, Min-le Su, Hangfan Zhang, Zhanhao Li, Chen Zhang, Shao Zhang, Yang Chen, Lei Bai, Shuyue Hu (Shanghai AI Lab et al.)
**Date:** 2026-09-01 · **Subjects:** cs.AI · Code + project page released
**Flagged by:** @dair_ai top-papers-of-the-week (#2).

## One-Line Summary

Coding agents are good for **a session** and unreliable for **a week**. Harness-of-Harness (**HoH**) wraps *whatever* coding harness you already run and organizes its runs into repeated **plan → code → test** increments, so a project keeps building for **days** without a human. It's a meta-layer, not a new harness: +52.25% average relative gain over the standalone harnesses, and a multi-day run (**70+ iterations**) that autonomously builds a playable FPS game.

## The Method

HoH sits **on top of** an existing coding-agent harness and turns single-shot execution into a sustained loop. Three roles around one evolving artifact:

- **Project Planner** — turns the spec + accumulated **test evidence** into a *new* development plan each iteration (not "continue the transcript").
- **Developer** — builds against that plan.
- **QA Tester** — evaluates across quality dimensions and returns an **evidence bundle**; the next iteration starts from that bundle, not the raw conversation.

Design principles that make a long run not collapse:
- **Split testing in two.** Implementation-time testing (the agent's own tests) is kept **separate from independent evaluation** — so the agent can't grade its own work with the same tests it wrote to pass. (This is the sharp bit.)
- **Constrain the outputs, not the workflow.** HoH scopes work into **small verifiable increments** and constrains *verifiable outputs* rather than prescribing how the agent should work.
- **Balance repair vs. capability growth** — so a long run neither stalls on one broken subsystem nor wanders into unplanned features.
- **Progressive exposure + reuse.** Deliverables, role-specific tools, and skills are exposed progressively; **reuse over recreation**; **versioned project histories** are maintained.

## Key Results

- **Three harness-model pairs:** Codex+GPT-5.5, OpenCode+DeepSeek-V4-Pro, Pi+MiniMax-M3.
- **Benchmarks:** GameCraft-Bench, FrontierSWE, ProgramBench.
- **HoH beats the corresponding standalone harness in all cases:** avg **+52.25%** relative gain, max **+82.86%** after **three** iterations.
- **Multi-day deployment (70+ iterations):** autonomously develops a first-person-shooter with coherent storyline, implemented core mechanics, human-playable experience, polished visuals + integrated audio.

## Why It Matters To Us

- **The cleanest "outer loop" in the software-factory family.** It's the same shape as Lloyd's factory, Uber's managed agents, and poteto's Benny — but stated as a **portable wrapper over any harness** you already run. Sits alongside JIT-Agent (synthesize a harness) and Prime Agent (compounding harness) as the "self-improving loop over the SDLC" cluster.
- **"Separate implementation-time testing from independent evaluation" is the load-bearing idea for us.** It's the concrete fix to the failure mode our verification notes keep naming: an agent grading itself with the tests it wrote to pass. This is a mechanism, not a slogan — plan/build/QA with a *distinct* evaluator. Directly relevant to any autonomous loop SmolPaws runs.
- **"Constrain outputs, not workflow" ≈ our guardrail-tier + verification thesis.** Don't script the agent's steps; verify the deliverable. Same spirit as Vero (verify the artifact), SKILL.state (runtime owns validity), and Balocco's guardrail tiering.
- **Plan-from-test-evidence, not from transcript** is the same "start from a bundle, not history" move as Rosen's receipts and the memory/context-out-of-prompt papers — here applied to the *planning* step across days.

## Where It's Thin / Skeptic's Notes

- **"+52.25% relative" is over the standalone harness after 3 iterations** — i.e. it's the value of *adding an outer loop*, which of course helps; the honest question is cost (3+ iterations × full harness runs) vs. that gain.
- **The FPS-game showcase is a demo, not a benchmark.** Impressive and legible, but a single hand-picked multi-day run; "70+ iterations → playable game" is existence, not distribution.
- **Benchmarks are code-gen suites** (GameCraft/FrontierSWE/ProgramBench); the independent-evaluation split is the transferable idea, the exact numbers are harness/model/date-bound.
- **Still an orchestration wrapper** — it inherits the reliability of the harness underneath; HoH improves the *loop*, not the base agent's judgment.

## Related

- `software-factories-zach-lloyd.md`, `software-factory-uber-scale.md`, `software-factory-design-patterns-ai-that-works.md` — the software-factory family; HoH is the portable outer-loop version.
- `verification-and-trust-lauren-tan-poteto.md` — Benny ≈ HoH's plan→build→QA loop; and "verification is the bottleneck."
- `two-camps-synthesis-vitor-balocco.md` — "constrain outputs, not workflow" = guardrail-first; grow rails from evidence.
- `../verification/vero-can-ai-agents-build-formally-verified-software-repositories.md` — verify the artifact, not the agent's self-report.
- `../harness/` — Prime Agent (compounding harness) and SKILL.state; HoH wraps a harness rather than replacing it.
