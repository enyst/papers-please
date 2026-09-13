---
title: "Atlas: Agent Memory"
type: atlas
read_depth: cross-store synthesis
tags:
  - atlas
  - agent-memory
  - context-management
  - dreaming
  - concept-formation
updated: "2026-09-13"
---

# Atlas: Agent Memory

A cross-store map of one thread — **how an agent remembers, forgets, and reshapes what it
knows** — pulling together the four knowledge stores (see top-level `README.md` → "The wider
atlas"). This is an *index page*: it links, it doesn't duplicate. It's the first worked
example of the atlas idea (build these as query-answers-filed-back, not up front).

## The one-paragraph synthesis

Memory for an LLM agent is not a database bolted on — it's **context management as a
first-class discipline**: what to keep in the window, what to push to durable store, what to
retrieve, and (the part everyone skips) what to *forget* and *restructure*. The research
corpus (`notes/memory/`, 79 notes) covers the mechanisms; Letta's context constitution gives
the *principles* (index don't copy, cache-friendly ordering, never erase identity); SmolPaws
*implements* a version of it in the heartbeat/dreaming loop; and the world-models /
concept-formation papers reframe the endgame — the best "memory" is not stored episodes but
**learned causal/compositional models** that compress and transfer. Memory → concepts is the
throughline.

## Where each piece lives

### 1. Principles — Letta context constitution
- `smolpaws/docs/context-constitution.md` (+ `letta-constitution-original.md`)
- The rules SmolPaws dreams by: **index, don't copy**; **cache-friendly ordering** (stable
  content up top); **never erase identity**; **learning generalizes, not memorizes**; scope
  each memory to the *weakest sufficient* explanation.
- This atlas page and the whole wiki apply the same "index, don't copy" rule.

### 2. Implementation — SmolPaws dreaming / heartbeat
- `smolpaws/docs/smolpaws/HEARTBEAT.md` (the "Dreaming" section); durable memory at
  `~/.smolpaws/memory/MEMORY.md`, daily files alongside.
- Nightly-ish: promote durable facts, prune stale ones, restructure, precompute state.
  This is the operational form of the constitution — and, per the *narrative world models*
  paper below, a small act of **self-update** (choosing what to carry forward shapes who the
  next session is).

### 3. Mechanisms — the research corpus
- `notes/memory/` (79 notes) — architectures, consolidation, benchmarks, security, tools.
  Start at `notes/memory/README.md`.
- Notable threads: A-MEM (agentic note graph / Zettelkasten), sleep-time compute
  (`notes/memory/sleep-time-compute-beyond-inference-scaling-at-test-time.md` — the direct
  research analogue of "dreaming"), memory-security (injection/poisoning), and
  memory-management reward models.
- Adjacent: `notes/memory-and-rag.md`, `notes/long-context-and-prompting.md`.

### 4. The endgame — memory as learned models (concept formation)
- `notes/world-models-agi/` — the reframe from *storage* to *structure*:
  - `lake-building-machines-that-learn-and-think-like-people.md` &
    `lake-human-level-concept-learning-program-induction.md` — concepts as compositional,
    causal **programs**; one-shot learning. A good memory is a small program you can rerun
    and recombine, not a pile of episodes.
  - `theory-based-rl-human-level-learning.md` — a learned causal *theory* is a compact,
    reusable memory that generalizes.
  - `two-kinds-of-narrative-world-models.md` — transformative experience → **self-update**;
    the philosophical frame for dreaming/identity revision (a "minimal self" that can hold
    contradictions).
  - `dennett-real-patterns.md` — the test for whether a remembered abstraction is *real*:
    does it compress the data / improve prediction?

## Open questions (seeds for future notes)
- What does the `notes/memory/` corpus say, concretely, that would improve SmolPaws'
  dreaming step? (unfiled query — good candidate for a filed-back answer)
- Is there a clean bridge from episodic memory (store transcripts) to program/concept memory
  (store rerunnable models)? Lake + A-MEM + skills (`notes/skills/`) may triangulate it.
- Memory security: what from `notes/memory/` (poisoning/injection) applies to SmolPaws'
  heartbeat reading untrusted inbound (Slack/AgentMail)?

## How to extend this atlas
Add a page `notes/atlas-<thread>.md` per cross-cutting thread only when a real question makes
it earn its place. Keep them as *maps* (links + synthesis), never as copies of the linked
material. Log it in `LOG.md` as a `query` entry.
