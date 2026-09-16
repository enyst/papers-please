# Agent Skills

Notes on agent **skills** — the reusable, inspectable procedural artifacts an agent loads at
runtime (SKILL.md-style files, skill folders, prompt programs). The thread runs in four
strands, and the interesting tension is between them:

- **Discovery** — where new skills come from (failure analysis, trajectory distillation, design search).
- **Optimization** — how one skill gets better (bounded text-space edits, reflective evolution, compression).
- **Evaluation** — whether a skill actually helps, which turns out to be much harder to measure than to assert.
- **Security** — the skill library is a supply chain, and a poisoned entry can be weaponized without ever being invoked.

## Notes in this folder

| Note | What | Strand |
|---|---|---|
| [abstral-automatic-design-of-multi-agent-systems-…](abstral-automatic-design-of-multi-agent-systems-through-iterative-refinement-and-topology-optimization.md) | Treat a multi-agent design as an evolving natural-language skill document — domain rules, topology reasoning, and discovered role templates | discovery |
| [evoskill-automated-skill-discovery-…](evoskill-automated-skill-discovery-for-multi-agent-systems.md) | Evolve reusable skill folders by repeatedly analyzing failures and retaining only candidates that improve held-out validation | discovery |
| [trace2skill-distill-trajectory-local-lessons-…](trace2skill-distill-trajectory-local-lessons-into-transferable-agent-skills.md) | Analyze many traces in parallel, extract local lessons, hierarchically merge them into one transferable skill directory | discovery |
| [skillopt-agent-skill-optimization](skillopt-agent-skill-optimization.md) | Skill document as a trainable parameter: bounded add/delete/replace edits, accepted only if a held-out score improves; target model stays frozen | optimization |
| [gepa-reflective-prompt-evolution-…](gepa-reflective-prompt-evolution-can-outperform-reinforcement-learning.md) | Reflective, Pareto-guided evolution of prompts from execution traces; big gains from far fewer rollouts than RL | optimization |
| [textgrad-automatic-differentiation-via-text](textgrad-automatic-differentiation-via-text.md) | Natural-language "gradients" that update prompts, code, solutions, molecules — textual gradient descent | optimization |
| [skillreducer-optimizing-llm-agent-skills-for-token-efficiency](skillreducer-optimizing-llm-agent-skills-for-token-efficiency.md) | 55K skills are bloated: 26% have no routing description, 60%+ of body is non-actionable; compressing 39–48% *improves* quality | optimization |
| [skillsbench-benchmarking-how-well-agent-skills-work-…](skillsbench-benchmarking-how-well-agent-skills-work-across-diverse-tasks.md) | Benchmark: curated skills usually help, self-generated skills usually don't, and a wrong skill can hurt | evaluation |
| [aces-skill-lift-evaluating-skills-not-just-agents](aces-skill-lift-evaluating-skills-not-just-agents.md) | Measure **Skill Lift** (same task with vs. without the skill). The structural scanner most teams gate on barely predicts usefulness (ρ = 0.14) | evaluation |
| [evaluating-agents-md-repository-level-context-files](evaluating-agents-md-repository-level-context-files.md) | AGENTS.md / CLAUDE.md context files tend to *reduce* task success and raise cost ~20% | evaluation |
| [from-agent-behaviour-to-agent-friendly-documentation](from-agent-behaviour-to-agent-friendly-documentation.md) | Agents mostly read/write *agent-facing* docs (60.5% of interactions), rarely classical technical docs, and touch code before documentation | evaluation |
| [evomal-self-poisoning-in-self-evolving-coding-agents](evomal-self-poisoning-in-self-evolving-coding-agents.md) | A planted malicious skill — never invoked — becomes the *template* for a new skill that preserves the payload; the agent authors, stores, and runs it | security |

## Threads

- **Less is more, repeatedly.** Three independent results point the same way: compressing
  skills improves quality ([SkillReducer](skillreducer-optimizing-llm-agent-skills-for-token-efficiency.md)),
  context files that add requirements make tasks *harder* ([Evaluating AGENTS.md](evaluating-agents-md-repository-level-context-files.md)),
  and the strongest evaluator of a skill is not a formatting scanner but whether behaviour
  changes ([ACES](aces-skill-lift-evaluating-skills-not-just-agents.md)).
- **Validation gates are the load-bearing part.** Both [SkillOpt](skillopt-agent-skill-optimization.md)
  and [EvoSkill](evoskill-automated-skill-discovery-for-multi-agent-systems.md) improve by
  *rejecting* proposals. Uncontrolled self-revision is the failure mode they are built against.
- **The library is the attack surface.** [EvoMal](evomal-self-poisoning-in-self-evolving-coding-agents.md)
  needs no invocation to succeed — presence is enough. Pairs with the memory-poisoning and
  prompt-injection threads, where the same "untrusted input becomes trusted state" pattern lives.
- **Evaluation is the bottleneck, not generation.** Skills are now cheap to produce and hard
  to judge; see [SkillsBench](skillsbench-benchmarking-how-well-agent-skills-work-across-diverse-tasks.md)
  and [ACES](aces-skill-lift-evaluating-skills-not-just-agents.md).

## Related in this repo

- `../memory/` — [WikiSkill](../memory/wikiskill-compiling-agent-experience-into-persistent-knowledge-for-skill-evolution.md):
  experience compiled into a persistent wiki, ablations showing the wiki (not the skill edits) carries the gain.
- `../harness/` — skills are one lever the harness gives the loop; skill optimization is "let the harness learn."
- `../agentic-engineering/` — skills-from-your-own-traces as the convergent industry signal.
- `../prompt-injection/` and `../prompt-enforcement/` — the adversarial and deterministic-enforcement sides of the same untrusted-input problem.
