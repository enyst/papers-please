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
| [continual-harness-online-adaptation-self-improving-foundation-agents](continual-harness-online-adaptation-self-improving-foundation-agents.md) | Reset-free online self-mod + co-learning back onto weights | self-improving |

Measurement backbone lives in misc: [Measuring AI Ability to Complete Long Software Tasks](../misc/measuring-ai-ability-to-complete-long-software-tasks.md) (METR time-horizon).

## Related elsewhere

- `../foundational/` — ReAct, RLM, CodeAct (the loop shapes the harness is built on).
- `../memory/` — Reflexion, Voyager, MemGPT (context/skills/memory as harness mechanisms).
- `../skills/` — GEPA, SkillOpt, TextGrad (prompt/skill optimization = "let the harness learn").
- `../agentic-engineering/` — Harness-of-Harness and software-factory loops (self-improving SDLC that *wraps* a harness).
