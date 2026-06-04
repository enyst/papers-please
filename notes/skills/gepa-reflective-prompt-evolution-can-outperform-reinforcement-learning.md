# GEPA: Reflective Prompt Evolution Can Outperform Reinforcement Learning

**Paper:** [arXiv:2507.19457](https://arxiv.org/abs/2507.19457)
**Authors:** Lakshya A. Agrawal, Shangyin Tan, Dilara Soylu, Noah Ziems, Rishi Khare, Krista Opsahl-Ong, Arnav Singhvi, Herumb Shandilya, Michael J. Ryan, Meng Jiang, Christopher Potts, Koushik Sen, Alexandros G. Dimakis, Ion Stoica, Dan Klein, Matei Zaharia, Omar Khattab
**Date:** July 2025; revised February 2026
**Project:** [DSPy](https://dspy.ai)

## One-Line Summary

Use execution traces and natural-language reflection to evolve prompts through a Pareto-guided genetic search, getting large gains from far fewer rollouts than reinforcement learning.

## Core Idea

GEPA treats prompts inside a compound AI system as optimizable artifacts. Instead of learning from sparse scalar rewards alone, it asks an LLM to read failed and successful trajectories, extract high-signal lessons, and mutate prompts so those lessons become persistent behavior.

The central claim is that language is a richer optimization substrate than policy-gradient rewards for many agent tasks. A single rollout can contain enough diagnostic information to justify a large prompt edit, if the optimizer can inspect the trace, evaluator feedback, and module-level behavior.

GEPA stands for **Genetic-Pareto**:

| Component | Role |
|---|---|
| Genetic search | Build a tree of prompt candidates through reflective mutations. |
| Pareto illumination | Keep candidates that are best for different training examples, not just one aggregate winner. |
| Reflection | Convert trajectory-level observations into explicit prompt rules. |
| Merge | Combine complementary prompt lessons when useful. |

## Method

### Pipeline

1. **Run the current language program:** Execute the system on task instances and collect traces, outputs, and scores.
2. **Reflect on trajectories:** Use textual feedback to diagnose what went wrong or what strategy worked.
3. **Mutate prompts:** Propose new prompt versions that encode the discovered lesson.
4. **Track a Pareto frontier:** Retain candidates that cover different examples or strategy niches.
5. **Evaluate candidates:** Score prompt variants on held-out or validation examples.
6. **Optionally merge:** Combine compatible lessons from different candidates to produce stronger prompts.

### Key Design Choices

- **Trace-aware updates:** The optimizer sees intermediate module calls, not just final answers.
- **Instance-level coverage:** Pareto tracking prevents the search from collapsing around the easiest examples.
- **No weight updates:** All adaptation happens in prompt text.
- **Prompt-level target:** GEPA optimizes system/module prompts, not reusable skill folders.

## Results

The paper reports GEPA outperforming strong prompt optimizers and RL-style adaptation across multiple agent benchmarks, including HotpotQA, IFBench, HoVer, PUPA/Papillon, FSABench, AIME-2025, and LiveBench-Math.

Headline results from the paper:

- On Qwen3-8B, GEPA improves aggregate score by about **+12.1 points**, while GRPO after 24K rollouts improves by about **+5.7 points**.
- GEPA can match or exceed GRPO while using a small fraction of the rollout budget.
- On GPT-4.1 mini, GEPA+Merge reaches about **+14.4 aggregate points** over baseline in the main table, roughly doubling MIPROv2's gain.
- Compared with TextGrad as a baseline in the GEPA experiments, GEPA's Pareto/frontier machinery yields stronger generalization.

## Why This Matters for SmolPaws

GEPA is relevant because it gives a concrete algorithm for improving language artifacts from agent traces. Even though it targets prompts, not skills, the mechanics are directly useful:

1. **Use traces, not vibes.** A skill-editing loop should inspect exact task trajectories and evaluator failures.
2. **Keep diverse winners.** Different tasks expose different procedural gaps; a single aggregate score can hide important niches.
3. **Prefer textual lessons.** The optimizer should write explicit rules that humans can inspect and reject.
4. **Validate before adopting.** GEPA's gains come from candidate evaluation, not blind self-revision.

## Relationship to SkillOpt

SkillOpt can be read as applying GEPA-like reflective optimization to a more deployable artifact: a persistent skill document. GEPA optimizes prompt modules inside a language program; SkillOpt optimizes `best_skill.md` with stronger controls around bounded edits, validation gates, rejected-edit memory, and slow/meta updates.

In short:

| GEPA | SkillOpt |
|---|---|
| Prompt optimizer | Skill optimizer |
| Pareto prompt candidates | Candidate skill edits |
| Reflection over traces | Reflection over skill-conditioned rollouts |
| Prompt remains inside system | Skill can be exported and reused |

## Caveats / Limits

- Prompt edits may be tightly coupled to the specific program, module layout, or model.
- Pareto search can produce larger prompt artifacts unless merged and pruned carefully.
- The method assumes reliable textual feedback from a strong optimizer model.
- It does not directly solve skill packaging, progressive disclosure, scripts/resources, or cross-harness skill loading.

## Key Quotes

> "Given any AI system containing one or more LLM prompts, GEPA samples trajectories ... and reflects on them in natural language to diagnose problems, propose and test prompt updates, and combine complementary lessons from the Pareto frontier of its own attempts."

> "GEPA can often turn even just a few rollouts into a large quality gain."
