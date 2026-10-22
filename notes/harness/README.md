# Agent Harnesses

## Working definition

> **A harness is everything between the model weights and the world** — the loop, the context it assembles, the tools and skills it can reach for, the sub-agents it can spawn, and lately the code of the harness itself.

We adopt this definition (from the DAIR.AI [Harness Engineering collection](../../blogs/interesting-posts.md), YC Paper Club: Harness Edition, 2026-08-26) as the canonical one for this folder. It's cleaner than "the subsystem that makes an agent operational" because it draws the boundary by *position* — weights on one side, world on the other, harness in between — which makes the key claim fall out directly:

> The same weight file can score 30% or 95% on the same benchmark depending only on what surrounds it.

(Running example in the collection: Prime Agent takes ARC-AGI-3 from 30% → 95.5% on identical weights.) Everything in this folder is a way of engineering that "in between."

## The genealogy (why these papers sit together)

The harness grew in stages, each "giving the loop something new it is allowed to do":

1. **V0 / in-context** — the bare sampling loop; the only levers are what you put in the window (few-shot) and how many tokens you let it spend (CoT).
2. **Static harnesses — grow the action space** — fixed harness code, more verbs: browse, call tools, act+observe, self-critique, run code, spawn peers, write skills, edit memory, recurse. (ReAct, Reflexion, Voyager, MemGPT, RLM live here — noted under `../foundational/` and `../memory/`.)
3. **Self-improving harnesses — the fixed part stops being fixed** — first the prompt is optimized, then the scaffolding, then the harness *code* itself, then the whole thing adapts online while running.
4. **Measurement** — harness progress only counts if the *time horizon* a system can work over is actually getting longer.

## Notes in this folder

| Note | What | Stage |
|---|---|---|
| [code-as-agent-harness](code-as-agent-harness.md) | Survey: code as the operational substrate for reasoning/acting/verification | framing |
| [harness-handbook](harness-handbook.md) | Behavior→code maps to make a harness auditable/editable | framing |
| [skill-state-scalable-long-horizon-agent-skills](skill-state-scalable-long-horizon-agent-skills.md) | State-out-of-prompt runtime for long horizons (+ Prime Agent pointer) | static/self-improving |
| [darwin-godel-machine-open-ended-evolution-self-improving-agents](darwin-godel-machine-open-ended-evolution-self-improving-agents.md) | Agent rewrites its own code; archive-of-ancestors, empirical-not-proof | self-improving |
| [meta-harness-end-to-end-optimization-of-model-harnesses](meta-harness-end-to-end-optimization-of-model-harnesses.md) | Outer loop searches harness *code*; don't over-compress feedback | self-improving |
| [object-oriented-harness-specialization-routing](object-oriented-harness-specialization-routing.md) | Evolve inheriting specialists, route from base trajectories, preserve base; cluster-local search, total-cost caveat and OOD abstention | self-improving / routing |
| [continual-harness-online-adaptation-self-improving-foundation-agents](continual-harness-online-adaptation-self-improving-foundation-agents.md) | Reset-free online self-mod + co-learning back onto weights | self-improving |
| [prime-agent-self-improving-rlm-harness](prime-agent-self-improving-rlm-harness.md) | The runnable reference: persistent REPL + `rlm` subagents + versioned Continual Harness state (L0–L3) | self-improving |
| [rsiagent-autonomous-exploration-recursive-self-improvement](rsiagent-autonomous-exploration-recursive-self-improvement.md) | Explore a new environment, verify, consolidate memory, freeze, reuse — plus its three failure modes | self-improving |
| [harness-learning-generalizable-test-time-adaptation](harness-learning-generalizable-test-time-adaptation.md) | RL-trained harness editor transfers to unseen tasks; frozen test-time weights, sequential feedback and strong fixed-baseline caveats | learned adaptation |
| [empirical-study-harness-design-coding-agents](empirical-study-harness-design-coding-agents.md) | 176 matched settings: context elision→summary, persistent planning and workspace interfaces; effects depend on model, workload and context budget | component measurement |

### Stateful evidence and controlled restarts

- [LongHarness](longharness-stateful-evidence-management.md) — evidence ledger + separate conclusions/gaps, explicit revision/retraction; full history still replayed, not bounded-context memory.
- [Scaling Discovery Requires Forgetting](scaling-discovery-requires-forgetting.md) — restart scored program search from the best artifact; hide session/candidate history but retain the archive; matched-prefix reset test and joint communication/reset caveat.
- Related memory mechanism: [ReHarness](../memory/reharness-recurrent-agentic-continual-learning.md) — revise retrieved lessons against their original evidence after later feedback; fewer tokens can still cost more.

### Research orchestration and verification

- [The Agentic Scientist](agentic-scientist-orchestrating-coding-agents.md) — typed hypothesis/rubric contracts → parallel experiments → retrospective ablations → artifact-grounded reports; full 88-page paper, human corrections, missed metric changes and judge-dependent figure scores.

Measurement backbone lives in misc: [Measuring AI Ability to Complete Long Software Tasks](../misc/measuring-ai-ability-to-complete-long-software-tasks.md) (METR time-horizon).

## Related elsewhere

- `../foundational/` — ReAct, RLM, CodeAct (the loop shapes the harness is built on).
- `../memory/` — Reflexion, Voyager, MemGPT (context/skills/memory as harness mechanisms).
- `../skills/` — GEPA, SkillOpt, TextGrad (prompt/skill optimization = "let the harness learn").
- `../agentic-engineering/` — Harness-of-Harness and software-factory loops (self-improving SDLC that *wraps* a harness).
