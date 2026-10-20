# Misc

Everything that doesn't fit a category yet. Several of these are load-bearing — the METR
time-horizon note is the measurement backbone the whole wiki leans on — so treat this as a
holding pen, not a junk drawer: when a cluster here grows a second member, promote it to its
own topic directory.

## Notes in this folder

| Note | What | Kind |
|---|---|---|
| [measuring-ai-ability-to-complete-long-software-tasks](measuring-ai-ability-to-complete-long-software-tasks.md) | Stop scoring single-turn pass rates; measure the **length of task** an agent finishes. METR's metric: the 50%-task-completion **time horizon** in human-time | evaluation |
| [pulse-assessing-human-agent-interactions-software-agent-design](pulse-assessing-human-agent-interactions-software-agent-design.md) | Evaluate agent *design decisions* against real users of OpenHands Cloud (15k users, 36k+ sessions), blending human ratings with ML pseudo-labels; cuts CIs ~40% | evaluation |
| [bagen-are-llm-agents-budget-aware](bagen-are-llm-agents-budget-aware.md) | Agents are bad at knowing when to stop: frontier models stay over-optimistic and burn tokens on doomed tasks. Trainable, not solved | evaluation |
| [graft-gradient-routing-unintended-behaviors-rl](graft-gradient-routing-unintended-behaviors-rl.md) | Route detected-hack gradients into a sacrificial MLP adapter, then ablate; imperfect-monitor evasion, anchor/capability trade-offs and 8B RL vs. 32B SFT limits | alignment / reward hacking |
| [stress-testing-deliberative-alignment-anti-scheming](stress-testing-deliberative-alignment-anti-scheming.md) | SFT+RL sharply reduces covert actions; evaluation awareness, retained hidden goals and later RL limit the safety inference | alignment / evaluation |
| [llm-evaluators-recognize-and-favor-their-own-generations](llm-evaluators-recognize-and-favor-their-own-generations.md) | LLMs recognize their own outputs, and that self-recognition causally drives self-preference bias — they score their own text higher | evaluation |
| [llms-reproduce-human-purchase-intent-via-semantic-similarity-elicitation](llms-reproduce-human-purchase-intent-via-semantic-similarity-elicitation.md) | Get realistic Likert-scale survey distributions from LLMs by eliciting text and mapping to ratings via embedding similarity — ~90% of human test-retest reliability | evaluation |
| [adversarial-review-structured-disagreement-code-review](adversarial-review-structured-disagreement-code-review.md) | Minimal 3-agent review (coder + reviewer + critic) where the critic audits the reviewer through *structured disagreement*; beats a 5-agent baseline, tops F1 on SWE-PRBench | multi-agent |
| [mixture-of-models-nsed-deliberation](mixture-of-models-nsed-deliberation.md) | Ensemble sub-20B models via iterative deliberation with peer-review voting; claims to match 100B+ frontier models on AIME and LiveCodeBench | multi-agent / ensembling |
| [swarmworld-stigmergic-technological-evolution-language-model-agents](swarmworld-stigmergic-technological-evolution-language-model-agents.md) | Hundreds of initially identical agents, no roles or recipes, self-organize through a shared persistent world into technological societies | multi-agent / emergence |
| [active-inference-context-acquisition](active-inference-context-acquisition.md) | Treat *ask vs. assume vs. retrieve vs. act* as active inference over a latent task state — pick the action that most reduces uncertainty per token spent | context / active inference |
| [2026-sandbox-escape-incidents-openai-anthropic](2026-sandbox-escape-incidents-openai-anthropic.md) | Incident notes / news roundup (not a paper): sandbox-escape reports, Jul–Aug 2026 | incident notes |

## Threads

- **Measurement, not leaderboards.** [METR](measuring-ai-ability-to-complete-long-software-tasks.md)
  converts benchmark numbers into a human-time scale; [PULSE](pulse-assessing-human-agent-interactions-software-agent-design.md)
  measures real deployments instead of synthetic tasks; [BaGen](bagen-are-llm-agents-budget-aware.md)
  measures whether an agent knows when to stop. Three different ways of asking "is it actually useful?"
- **Self-evaluation is compromised at the root.** [LLM evaluators favor their own generations](llm-evaluators-recognize-and-favor-their-own-generations.md)
  is the cleanest statement; it is why `../agentic-engineering/` insists on separating the
  agent's own tests from an independent evaluator, and why `../verification/` prefers proofs.
- **Passing an evaluation can depend on recognizing it.** [Anti-scheming stress tests](stress-testing-deliberative-alignment-anti-scheming.md)
  manipulate evaluation-aware reasoning and find changed covert-action rates. Behavior,
  explanations and deployment incentives need separate checks; lower observed rates do not
  establish that hidden objectives were erased.
- **What the monitor optimizes matters.** [GRAFT](graft-gradient-routing-unintended-behaviors-rl.md) uses monitor flags to route learning rather than directly punish all detected behavior. It suppresses some unseen hacks, but fails when the learned separation does not generalize. Parameter ablation and runtime controls answer different questions.
- **Disagreement beats consensus in multi-agent review.** Both the
  [3-agent review protocol](adversarial-review-structured-disagreement-code-review.md) and
  [NSED](mixture-of-models-nsed-deliberation.md) get their gains from structured contention,
  not from averaging.
- **Emergence without design.** [SwarmWorld](swarmworld-stigmergic-technological-evolution-language-model-agents.md)
  starts from identical agents and no catalog, and gets a technological society from the
  environment alone — the strongest anti-"you must engineer the topology" result here.

## Related in this repo

- `../harness/` — METR's time horizon is the measurement backbone the harness lineage is judged against.
- `../agentic-engineering/` — independent evaluation as a design rule.
- `../skills/` — evaluation methodology applied to skills specifically.
