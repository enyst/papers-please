# EvoSkill: Automated Skill Discovery for Multi-Agent Systems

**Paper:** [arXiv:2603.02766](https://arxiv.org/abs/2603.02766)
**Authors:** Salaheddin Alzubi, Noah Provenzano, Jaydon Bingham, Weiyuan Chen, Tu Vu
**Date:** March 2026
**Code:** [https://github.com/sentient-agi/EvoSkill](https://github.com/sentient-agi/EvoSkill)

## One-Line Summary

Evolve reusable agent skill folders by repeatedly analyzing failures, proposing new or revised skills, and retaining only candidates that improve held-out validation performance.

## Core Idea

EvoSkill argues that agent improvement should happen at the skill abstraction level, not only by changing prompts, code, or weights. A coding-agent harness can gain domain expertise by accumulating structured skill folders: procedural instructions, trigger metadata, helper scripts, and references.

The loop is failure-driven. When an agent gets examples wrong, a proposer diagnoses the failure mode, a skill-builder materializes a skill or skill edit, and validation decides whether the new agent program survives.

## Method

### Agents in the Loop

1. **Executor Agent:** Runs tasks with the current program and skill set.
2. **Proposer Agent:** Reads failed traces and ground-truth answers to identify missing capabilities or bad procedures.
3. **Skill-Builder Agent:** Converts proposals into concrete skill folders with `SKILL.md` and optional scripts/resources.

### Evolution Loop

1. Maintain a frontier of high-scoring agent programs.
2. Select a parent program from the frontier.
3. Run the parent on a training batch and collect failures.
4. Generate a skill proposal from failure analysis and accumulated feedback history.
5. Materialize a child program with the new or edited skill.
6. Evaluate the child on held-out validation.
7. Admit the child to the frontier only if it improves selection criteria.
8. Evaluate final skills on a separate held-out test set.

### Key Design Choices

- **Frozen base model:** Only skills and metadata evolve.
- **Skill folders as artifacts:** The output is inspectable and reusable.
- **Feedback history:** Avoids repeating failed proposals and lets the proposer refine partially useful ideas.
- **Pareto frontier:** Keeps multiple useful programs rather than one winner.
- **Held-out validation:** Filters plausible but harmful skills.

## Results

The paper evaluates EvoSkill with Claude Code + Opus 4.5 on two main benchmarks:

- **OfficeQA:** Grounded reasoning over U.S. Treasury Bulletins.
  - Baseline exact-match accuracy: **60.6%**.
  - Best merged skill library: about **67.9%** in the abstract, a **+7.3 point** gain.
  - Independent runs discover complementary skills, and merging unique skills performs best.
- **SealQA:** Search-augmented QA with noisy or conflicting retrieval.
  - Accuracy improves from **26.6% to 38.7%**, a **+12.1 point** gain.
  - The discovered `search-persistence-protocol` skill enforces exhaustive search, source verification, and completeness checks.
- **Transfer:** A skill evolved on SealQA transfers zero-shot to BrowseComp, improving accuracy by **+5.3 points** without modification.

Representative discovered skills include Treasury table extraction verification, quantitative financial analysis methodology, and search persistence protocols.

## Why This Matters for SmolPaws

EvoSkill is directly actionable for a skill repository:

1. **Skills should be born from repeated failures.** The best skill is often a named response to a recurring failure mode.
2. **Use validation gates.** Do not merge a skill just because it sounds good.
3. **Keep skills modular.** Separate triggerable capabilities are easier to inspect, compose, and transfer.
4. **Merging independent runs can help.** Different runs expose different failure modes.
5. **Transfer is the prize.** A good skill should help adjacent tasks without retraining.

## Relationship to SkillOpt

EvoSkill is the closest harness-side competitor named in the SkillOpt summary. It already evolves skill folders, validates candidates, and keeps a frontier. SkillOpt adds tighter training controls for one compact skill:

| EvoSkill | SkillOpt |
|---|---|
| Discovers and refines skill libraries | Optimizes one domain skill document |
| Failure-analysis proposer + skill-builder | Optimizer model proposes bounded edits |
| Frontier of agent programs | Candidate skill selected by validation gate |
| Skill folders can include scripts/resources | Deployed `best_skill.md` is compact and static |
| Broad evolutionary search | Deep-learning-style learning rate, rejected-edit buffer, slow/meta updates |

## Caveats / Limits

- Experiments appear expensive and are often single-run due to Opus 4.5 cost.
- Ground-truth answers are used for failure diagnosis during evolution, so careful separation from generated skill content is essential.
- The strongest evidence is on OfficeQA and SealQA; broader domains remain future work.
- Skill quality depends on the proposer and skill-builder prompts.

## Key Quotes

> "EvoSkill analyzes execution failures, proposes new skills or edits to existing ones, and materializes them into structured, reusable skill folders."

> "Rather than evolving code or prompts directly, EvoSkill evolves skills: structured, reusable capability modules that persist across tasks."
