# SkillOpt: Executive Strategy for Self-Evolving Agent Skills

**Paper:** [arXiv:2605.23904](https://arxiv.org/abs/2605.23904)
**Authors:** Yifan Yang, Ziyang Gong, Weiquan Huang, Qihao Yang, Ziwei Zhou, Zisu Huang, Yan Li, Xuemei Gao, Qi Dai, Bei Liu, Kai Qiu, Yuqing Yang, Dongdong Chen, Xue Yang, Chong Luo
**Affiliation:** Microsoft, Shanghai Jiao Tong University, Tongji University, Fudan University
**Date:** May 2026
**Code:** [https://aka.ms/SkillOpt](https://aka.ms/SkillOpt)

## One-Line Summary

Treat agent skill documents as trainable parameters: use a separate optimizer model to make bounded add/delete/replace edits on a skill file, accepting only edits that improve a held-out validation score — like gradient descent, but in text space.

## Core Idea

Agent skills today are either hand-crafted, generated one-shot by an LLM, or evolved through loosely controlled self-revision. None of these reliably improve over their starting point under feedback. SkillOpt reframes skill improvement as *optimization*: the skill document is the parameter, rollout trajectories are the training data, and a separate optimizer model proposes bounded edits that are validated before acceptance.

The deep-learning analogy is deliberate and operational:

| Deep Learning | SkillOpt |
|---|---|
| Parameter | Skill document (`best_skill.md`) |
| Gradient direction | Trajectory-derived edit direction |
| Learning rate | Edit budget (max edits per step) |
| Validation check | Held-out selection gate |
| Batch/schedule | Rollout batch, minibatch reflection, cosine schedule |
| Momentum | Epoch-wise slow/meta update |

The key constraint: the *target model is frozen*. Only the skill text changes. At deployment, the optimized skill is a static markdown file — zero additional inference cost.

## Method

### Pipeline

1. **Forward pass (rollout):** Frozen target model executes tasks with current skill. Collect scored trajectories.
2. **Minibatch reflection:** Optimizer model analyzes successes and failures in small batches, proposes bounded edits (add/delete/replace).
3. **Batch-level merge:** Deduplicate and resolve conflicts across minibatch proposals.
4. **Bounded update:** Rank merged edits by expected utility, clip to edit budget `Lt` (decayed via cosine schedule).
5. **Validation gate:** Evaluate candidate skill on held-out set. Accept only if it *strictly* improves the score. Rejected edits go to a buffer as negative feedback.
6. **Epoch-wise slow/meta update:** After each epoch, compare previous-epoch vs current-epoch skill on the same samples. Write a protected "slow-update field" capturing durable lessons. Separate meta-skill (optimizer-side only) summarizes what worked/failed.

### Key Design Choices

- **Edit budget as learning rate:** Controls how far a skill can move per step. Cosine schedule: larger edits early, smaller consolidation later.
- **Rejected-edit buffer:** Failed edits aren't wasted — they become negative feedback so the optimizer avoids repeating the same mistakes.
- **Validation gating:** Prevents plausible-sounding but harmful edits from accumulating. Ties are rejected.
- **Slow/meta update separation:** Fast per-step edits learn from the current batch. Epoch-wise slow update captures cross-epoch patterns. Meta-skill stays optimizer-side only, never shipped with the deployed skill.

## Results

### Scale of Improvement

Tested across 6 benchmarks, 7 target models, 3 execution harnesses (direct chat, Codex, Claude Code). SkillOpt is **best or tied on all 52 evaluated cells**.

On GPT-5.5 direct chat, average improvement over no skill:
- **+23.5 points** (58.8 → 82.3 average across 6 benchmarks)
- Beats the best per-cell competitor by +5.4 points on average

Biggest gains on procedural benchmarks:
- SpreadsheetBench: 41.8 → 80.7 (+38.9)
- OfficeQA: 33.1 → 72.1 (+39.0)
- LiveMathematicianBench: 37.6 → 66.9 (+29.3)

Inside agentic harnesses:
- Codex: +24.8 points over no skill, +14.0 over EvoSkill
- Claude Code: +19.1 points over no skill, +3.2 over EvoSkill

### Transfer

Optimized skills transfer across:
- **Models:** SpreadsheetBench skill trained on GPT-5.4 improves GPT-5.4-mini and GPT-5.4-nano
- **Harnesses:** Codex-trained spreadsheet skill transfers to Claude Code with +59.7 gain
- **Benchmarks:** OlympiadBench skill gives positive gains on Omni-MATH

No transfer row falls below the target's no-skill baseline — uniformly positive.

### Ablations

Each component matters:
- Removing learning rate: -2.5 to -5.5 points
- Removing rejected-edit buffer: -1.6 to -4.6 points
- Removing slow/meta update: -2.0 to -22.5 points (huge on SpreadsheetBench)

### Skill Artifacts

Optimized skills are compact: 300–2,000 tokens after 1–4 accepted edits. They're inspectable, procedural, not instance-specific. The output is literally a `best_skill.md` file.

## Why This Matters for SmolPaws

This paper is directly relevant to how we build and maintain skills:

1. **We already use skills extensively** — our `.agents/skills/` directory contains hand-crafted SKILL.md files for autoreview, security scanning, frontend design, etc. These are exactly the artifacts SkillOpt would optimize.

2. **Our skills grow organically.** The openclaw autoreview skill is 300+ lines of increasingly specific rules, many born from specific failure cases. SkillOpt suggests there's a principled way to evolve skills from feedback rather than manual patching.

3. **The architecture maps cleanly.** We could implement a simplified SkillOpt loop:
   - Use a benchmark of real tasks the skill should handle
   - Run the skill, collect scored outcomes
   - Use a strong optimizer model to propose bounded edits
   - Gate on validation
   - Export the improved skill

4. **Transfer results are promising for our use case.** Skills optimized for one model or harness transfer to others. If we optimize a skill for Codex, it'll likely work in Claude Code too.

5. **The "skill as trainable state of a frozen model" framing** validates our architectural choice: skills as external text artifacts, not model fine-tuning.

### What We Could Do

- **Short term:** Nothing — our skills are hand-crafted and working. But keep this in mind as skills accumulate.
- **Medium term:** When a skill underperforms on a specific benchmark or task class, try the SkillOpt loop: collect rollouts, optimize bounded edits, validate.
- **Long term:** Build a lightweight SkillOpt harness that runs during idle time (heartbeat?) to continuously improve our skill portfolio against real task outcomes.

### Connection to Autoreview Skill

The openclaw `autoreview` SKILL.md that Engel asked about is a perfect case study. It's a hand-crafted, organically grown skill document with ~300+ lines of increasingly specific rules. SkillOpt's research suggests:
- A SkillOpt-optimized version could outperform the hand-crafted version
- The optimized version would likely be more compact (300-2000 tokens)
- It would transfer across review engines (Codex → Claude) without manual adaptation

## Baselines Compared

| Method | Type | Key Limitation |
|---|---|---|
| No skill | Baseline | No domain adaptation |
| Human skill | Hand-crafted | Can't self-correct from failures |
| LLM skill | One-shot generated | Never updated |
| Trace2Skill | Trajectory distillation | No validation gate |
| TextGrad | Gradient-style prompt optimization | Optimizes prompts, not persistent skills |
| GEPA | Pareto reflective evolution | Targets prompts/configs, not reusable skills |
| EvoSkill | Skill-folder evolution | No bounded learning rates or rejected-edit memory |

## Key Quotes

> "The skill should instead be trained as the external state of a frozen agent, with the same discipline that makes weight-space optimization reproducible."

> "A textual learning-rate budget, rejected-edit buffer, and epoch-wise slow/meta update make skill training stable while adding zero inference-time model calls at deployment."

> "Bounded textual learning outperforms uncontrolled rewriting, held-out gating prevents harmful proposals from accumulating."

## Related Work We Should Track

- **EvoSkill** — skill-folder evolution under failure analysis (strongest harness-side competitor)
- **GEPA** — Pareto reflective prompt evolution
- **Trace2Skill** — trajectory-level skill distillation
- **TextGrad** — gradient-style natural-language prompt optimization
- **SkillsBench** — benchmark for evaluating agent skills
- **ABSTRAL** — multi-agent design document evolution
