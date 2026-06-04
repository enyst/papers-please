# SkillsBench: Benchmarking How Well Agent Skills Work Across Diverse Tasks

**Paper:** [arXiv:2602.12670](https://arxiv.org/abs/2602.12670)
**Authors:** Xiangyi Li et al.
**Date:** February 2026; revised March 2026
**Site:** [https://www.skillsbench.ai/](https://www.skillsbench.ai/)

## One-Line Summary

A benchmark showing that curated agent skills usually help, self-generated skills usually do not, and skills can hurt when they add the wrong procedural bias.

## Core Idea

SkillsBench treats agent skills as first-class evaluation artifacts. Rather than assuming a skill is useful because it looks helpful, it measures the delta between running an agent with no skills, with curated skills, and with self-generated skills.

The benchmark's definition of a skill is operational and useful:

| Criterion | Meaning |
|---|---|
| Procedural content | The artifact says how to do a class of tasks, not just facts. |
| Task-class applicability | It generalizes beyond one instance. |
| Structured components | It includes a `SKILL.md` plus optional resources. |
| Portability | It is file-based and usable across harnesses. |

SkillsBench explicitly excludes ordinary prompts, RAG retrieval, few-shot examples, and tool docs when they lack reusable procedural guidance.

## Benchmark Design

### Dataset

- **84-86 tasks** depending on paper revision/counting, spanning **11 domains**.
- Tasks are containerized and include task instructions, environments, oracle solutions, and deterministic verifiers.
- Skills are paired with tasks but must not leak task-specific answers.
- Deterministic `pytest`-style verifiers avoid LLM-as-judge variance.

### Conditions

1. **No skills:** Agent runs without skill augmentation.
2. **Curated skills:** Human-curated skill packages are available.
3. **Self-generated skills:** The model authors its own skill-like guidance where supported.

### Harnesses

The paper evaluates commercial agent harnesses including Claude Code, Gemini CLI, and Codex CLI across seven agent-model configurations, totaling **7,308 trajectories**.

## Results

Main findings:

- Curated skills improve average pass rate by **+16.2 percentage points** across evaluated configurations.
- Effects vary substantially by domain: gains range from small improvements in software engineering to very large gains in domains like healthcare.
- **16 of 84 tasks** show negative deltas from skills, meaning skills can actively hurt.
- Self-generated skills provide negligible or negative benefit on average, around **-1.3 points** in the paper's summary.
- Focused skills with **2-3 modules** outperform comprehensive documentation.
- Smaller models with good skills can match or exceed larger models without skills on procedural tasks.

## Why This Matters for SmolPaws

SkillsBench is the evaluation counterpart to SkillOpt. It answers the question: once we have a skill, how do we know it works?

Practical takeaways:

1. **Always measure the skill delta.** A skill should be evaluated against no-skill and alternative-skill baselines.
2. **Self-generated does not mean useful.** Models can consume procedural knowledge better than they can reliably author it.
3. **Less can be more.** A focused skill beats a large documentation dump when the task requires crisp procedural action.
4. **Skills can be harmful.** Skill loading should be selective, and skills need regression tests.
5. **Deterministic verifiers matter.** Skill optimization should use pass/fail tests or objective metrics whenever possible.

## Relationship to SkillOpt

SkillOpt needs benchmark discipline like SkillsBench. SkillOpt trains a skill; SkillsBench defines how to prove that skill helps. The two fit together naturally:

| SkillsBench | SkillOpt |
|---|---|
| Measures skill efficacy | Optimizes skill content |
| Compares no/curated/self-generated skills | Produces a curated-like optimized skill |
| Uses deterministic verifiers | Uses held-out validation gates |
| Finds skills can hurt | Rejects edits that do not strictly improve validation |

## Caveats / Limits

- The benchmark focuses on terminal/containerized tasks; GUI and long-running production workflows are less represented.
- Results are harness-dependent: skill loading and tool orchestration differ across agents.
- A positive average skill delta can hide task-level regressions.
- Self-generated skill baselines may improve as generation methods get stronger, but the paper's result is a warning against assuming that.

## Key Quotes

> "Curated Skills raise average pass rate by 16.2 percentage points(pp), but effects vary widely by domain ... and 16 of 84 tasks show negative deltas."

> "Self-generated Skills provide no benefit on average, showing that models cannot reliably author the procedural knowledge they benefit from consuming."
