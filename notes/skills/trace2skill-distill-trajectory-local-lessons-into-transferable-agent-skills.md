# Trace2Skill: Distill Trajectory-Local Lessons into Transferable Agent Skills

**Paper:** [arXiv:2603.25158](https://arxiv.org/abs/2603.25158)
**Authors:** Jingwei Ni, Yihao Liu, Xinpeng Liu, Yutao Sun, Mengyu Zhou, Pengyu Cheng, Dexin Wang, Erchao Zhao, Xiaoxi Jiang, Guanjun Jiang
**Date:** March 2026; revised April 2026
**Code:** [https://github.com/Qwen-Applications/Trace2Skill](https://github.com/Qwen-Applications/Trace2Skill)

## One-Line Summary

Analyze many execution traces in parallel, extract local lessons, and hierarchically merge them into a single transferable skill directory instead of editing skills one trajectory at a time.

## Core Idea

Trace2Skill targets the scalability bottleneck in skill authoring. Manual skill writing is expensive; naive automatic skill generation tends to be shallow; sequentially editing a skill after each trace can overfit to recent examples and drift.

The paper's answer is **trajectory-grounded distillation**: process a broad pool of executions, derive local patches from each, and consolidate them into a coherent skill artifact through inductive reasoning.

The important distinction is many-to-one consolidation:

| Sequential skill editing | Trace2Skill |
|---|---|
| Updates after one trace or small batch | Freezes the initial skill while analyzing many traces |
| Order-dependent | Order-insensitive parallel analysis |
| Can drift toward recent failures | Merges recurring patterns across a population |
| Often creates fragmented lessons | Produces a unified skill directory |

## Method

### Pipeline

1. **Collect trajectories:** Run an agent on a task distribution and gather successes, failures, logs, and artifacts.
2. **Dispatch analyst sub-agents:** Parallel analysts inspect disjoint trajectory batches.
3. **Extract local lessons:** Each analyst proposes targeted edits or references grounded in verified success/failure mechanisms.
4. **Hierarchical merge:** Merge local patches layer by layer, deduplicating conflicts and abstracting common patterns.
5. **Produce a skill directory:** Output a primary `SKILL.md` plus supporting references/resources.
6. **Evaluate transfer:** Test the evolved skill across model scales and out-of-distribution tasks.

### Key Design Choices

- **Agentic error analysis:** Analysts can inspect artifacts and validate fixes, not just read logs.
- **Parallelism:** Large trajectory sets can be processed in one analyst round plus a logarithmic merge tree.
- **No test-time retrieval:** The final skill is consumed directly; there is no external memory bank to query at inference.
- **Deepening and creation modes:** The system can improve a human-written skill or create a new skill from a parametric seed.

## Results

The main experiments focus on spreadsheet skills, with additional VisionQA and math reasoning evaluations.

Important reported results:

- On SpreadsheetBench and WikiTableQuestions, trajectory-grounded skills improve over human-written and parametric skill baselines across many settings.
- Skills evolved by Qwen3.5-35B on its own trajectories improve a Qwen3.5-122B agent by up to **+57.65 absolute points** on WikiTableQuestions.
- Parallel consolidation outperforms sequential editing on the 122B model across SpreadsheetBench metrics, while being much faster in wall-clock terms.
- A single portable skill folder outperforms a ReasoningBank-style retrieval baseline in same-model deepening.
- Agentic error analysis beats a single-call LLM error analyzer in weighted average across all four author/mode combinations.

## Why This Matters for SmolPaws

Trace2Skill is one of the closest papers to practical skill maintenance.

1. **Do not update from one failure blindly.** Aggregate many failures and look for reusable patterns.
2. **Artifact inspection matters.** Good skill edits often require checking files, outputs, and intermediate products.
3. **The output should be a normal skill folder.** No special retrieval machinery means easier deployment across harnesses.
4. **Skill transfer is real but uneven.** Cross-model and OOD transfer should be measured, not assumed.
5. **Merge quality is the hard part.** The value comes from turning local trajectory lessons into general procedures.

## Relationship to SkillOpt

Trace2Skill and SkillOpt share the belief that skills should be trained from trajectories without updating model weights. Their difference is emphasis:

| Trace2Skill | SkillOpt |
|---|---|
| Broad parallel consolidation across many traces | Iterative optimization with bounded edit steps |
| Builds/deepens skill directories | Trains one compact domain skill |
| Strong focus on many-to-one merge | Strong focus on learning-rate-like edit budgets and validation gates |
| No retrieval at inference | No extra inference cost at deployment |

A strong implementation could combine them: Trace2Skill-style parallel patch generation followed by SkillOpt-style validation-gated bounded updates.

## Caveats / Limits

- The source describes the paper as work in progress.
- Spreadsheet results dominate the core evidence; broader domain coverage is still developing.
- Merge quality depends heavily on analyst and merger prompts.
- The method needs a pool of trajectories and evaluators before it can improve a skill.

## Key Quotes

> "Instead of reacting sequentially to individual trajectories, Trace2Skill dispatches a parallel fleet of sub-agents to analyze a diverse pool of executions."

> "The evolved skill is consumed directly, making it natively compatible with any agent harness."
