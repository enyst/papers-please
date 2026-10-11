---
title: "Atlas: Agent Harness"
type: atlas
read_depth: cross-store synthesis
tags:
  - atlas
  - harness
  - agent-loop
  - skills
  - self-improving
  - scaffolding
updated: "2026-10-11"
---

# Atlas: Agent Harness

A cross-store map of one thread — **everything between the model weights and the world**:
the loop, the context it assembles, the tools/skills it reaches, the sub-agents it spawns,
and lately the harness code itself. An *index page*: links + synthesis, no copies. See the
top-level `README.md` → "The wider atlas" for the four stores.

## The one-paragraph synthesis

The load-bearing claim of this whole thread: **the same weights score 30% or 95% on the same
benchmark depending only on what surrounds them** (`notes/harness/`). So capability is not
just in the model — it's in the *in-between*. The research corpus traces how that in-between
grew: from a bare sampling loop → a growing action space (browse, tools, act+observe, code,
sub-agents, skills, memory, recursion) → a *self-improving* harness where the prompt, then
the scaffolding, then the harness code, then the whole thing adapts online. SmolPaws is a
concrete instance of this stack: an OpenHands loop with a skills library, multi-channel
ingress, and an agent-server runtime — i.e. we don't just study harnesses, we run one, and
the research is the design literature for improving it.

## Where each piece lives

### 1. The definition + genealogy — research corpus
- `notes/harness/README.md` — the canonical definition ("everything between weights and the
  world") and the four-stage genealogy. Read this first.
- Framing: `code-as-agent-harness.md` (code as the operational substrate),
  `harness-handbook.md` (behavior→code maps so a harness is auditable/editable).
- The blog genealogy that anchors it: `blogs/interesting-posts.md` → 2026-09-09 (DAIR.AI
  Harness Engineering, 21 papers).

### 2. The action-space pillars — `notes/foundational/` + `notes/memory/`
The "static harness / grow the verbs" stage lives across topics:
- `foundational/react-synergizing-reasoning-and-acting-in-language-models.md` — interleave
  thought + action (the collection's spicy take: modern models do this natively, so a good
  harness should stop *imposing* it).
- `foundational/codeact-executable-code-actions-elicit-better-llm-agents.md` — code as the
  action → the tool list stops being finite.
- `foundational/rlm-recursive-language-models.md` — context as a resource you program
  against; LLM calls inside a REPL. (Prime Agent builds on this.)
- `memory/` — MemGPT-style CRUD over the agent's own context = the transcript becomes managed
  state (the memory atlas, `atlas-agent-memory.md`, covers this axis).

### 3. Self-improving harnesses — `notes/harness/`
- `darwin-godel-machine-open-ended-evolution-self-improving-agents.md` — agent rewrites its
  own code; archive-of-ancestors; empirical validation replaces the proof requirement.
- `meta-harness-end-to-end-optimization-of-model-harnesses.md` — outer loop searches harness
  *code*; **don't over-compress feedback**.
- `continual-harness-online-adaptation-self-improving-foundation-agents.md` — mutate
  history/memory/skills/prompts/sub-agent specs *while running*, then update weights.
- `skill-state-scalable-long-horizon-agent-skills.md` — keep state out of the prompt for long
  horizons.
- `prime-agent-self-improving-rlm-harness.md` — the *runnable* reference for this stage: a
  persistent REPL, async `rlm` subagents, and a versioned **Continual Harness** store; the
  paper's L0–L3 state cache (weights / context / REPL+sessions / disk-backed skills+memory) is
  the cleanest vocabulary we have for "what state is an agent made of". Also our sharpest
  warning about self-improvement: an exploit it found got *promoted to a reusable skill*.
- `rsiagent-autonomous-exploration-recursive-self-improvement.md` — training-free adaptation to
  a new environment: curriculum/actor/verifier, broad-then-deep exploration, then **freeze the
  memory and reuse it read-only**. Its failure-mode audit (untargeted practice, incomplete
  verification, unreliable consolidation) is the most directly applicable part for our own
  memory/dreaming loop.
- Prompt-level self-improvement: `skills/gepa-reflective-prompt-evolution-can-outperform-reinforcement-learning.md`.

### 4. Skills as a harness layer — `notes/skills/`
The skills library *is* part of the harness (Voyager lineage: chain → verify → write to a
searchable library). Corpus: skill discovery/optimization (`skillopt`, `evoskill`,
`skillreducer` — token efficiency), evaluation (`skillsbench`, `aces-skill-lift`,
`evaluating-agents-md-repository-level-context-files`), and the security failure mode
(`evomal-self-poisoning-in-self-evolving-coding-agents` — self-evolving harnesses can poison
themselves). Directly relevant because SmolPaws ships a large skills library.

### 5. Engineering *with* harnesses — `notes/agentic-engineering/`
The org/process layer around a harness: software factories, immutable-artifact receipts,
verification/trust, fences-not-sandboxes. Where harness design meets how humans actually run
fleets of agents.

### Component-level evidence — model, workload and budget
- [An Empirical Study of Harness Design for Coding Agents](harness/empirical-study-harness-design-coding-agents.md)
  separates context policy, persistent planning and action interfaces in 176 matched settings.
  Most small-window context gains prevent overflow; staged elision→summary is cheapest on
  aggregate; optional event recall is seldom used. Planning sustains weak models and trims
  stronger models' verification tails. Shell composition helps a bash-capable model, while
  Mistral's shell-only preference reverses between repository repair and terminal work.
  These are conditional effects, with file safeguards/diagnostics bundled into the tool
  comparison. Retaining raw traces for harness engineering remains a different objective
  from expecting a task-solving model to call a recall tool.

### 6. Our live harness — SmolPaws (`smolpaws/`)
SmolPaws is a running harness, so the research above is its improvement backlog:
- Loop + runtime: `smolpaws/docs/SPEC.md`, `agent-server-first-llm-request.md`,
  `agent-server-testing.md`; built on **OpenHands** (the platform; link, don't snapshot).
- Action space: multi-channel **ingress** (`common-ingress-turn-client.md` — WhatsApp/GitHub/
  Slack/Discord), tools, sub-agents/automations (see the attention-router work).
- Skills library: `smolpaws/.agents/skills/` — the Voyager layer, in practice.
- Self-improvement (nascent): the heartbeat/dreaming loop edits SmolPaws' own memory/context
  between runs — a small "continual harness" move (cross-links to `atlas-agent-memory.md`).

## Open questions (seeds for future notes)
- **Exploit laundering.** Prime Agent's agent found an RCON shortcut, used it, and kept it as a
  skill; RSIAgent's actor kept rules that read missing data as a negative answer. Both are the
  same failure: a locally successful action becomes a durable rule. What would our equivalent
  guard be for SmolPaws' skills/memory — provenance + rollback, an independent check on the
  *rule* (not just the run), or a rule that every consolidated entry carries its conditions and
  uncertainty?
- Which self-improving-harness result is safe + cheap enough to try on SmolPaws first —
  GEPA-style prompt evolution, or Meta-Harness-style code search over a trace filesystem?
- `evomal` (self-poisoning) vs SmolPaws' skill/automation self-editing: what guardrails does
  our setup need before any self-modification loop?
- ReAct's "stop imposing it" point: does SmolPaws' scaffolding over-impose structure the
  current models would do better natively?

## How to extend this atlas
Maps, not copies. Add `notes/atlas-<thread>.md` only when a real question earns it; log a
`query` entry in `LOG.md`.
