# What Is Agent Memory?

An LLM without memory is a brilliant amnesiac. It can reason, write code, explain quantum mechanics — but every conversation starts from zero. It doesn't know what you discussed yesterday. It doesn't remember that the last three approaches failed. It can't build on what it learned last week. Agent memory is everything that changes this.

## The Problem

Modern LLMs have a fixed context window. Once a conversation exceeds that window, information falls off the edge. Even within the window, the model treats each conversation as a fresh start — there's no persistence between sessions, no accumulation of experience, no learning from past mistakes (at inference time, without fine-tuning).

This matters because real work is *longitudinal*. A software engineering agent that forgets yesterday's debugging session will re-explore the same dead ends. A personal assistant that can't remember your preferences is just a chatbot with extra steps. An agent that can't recall which approaches worked and which failed on similar tasks is condemned to repeat history.

## What Memory Gives an Agent

Agent memory serves several distinct functions, often in the same system:

**Continuity across sessions.** The most basic function: remembering what happened in prior conversations. Without this, every interaction is a first meeting. Mem0 ([Chhikara et al., 2025](https://arxiv.org/abs/2504.19413)) builds an entire production architecture around extracting and persisting salient conversational facts to avoid replaying full conversation history.

**Learning from experience.** Agents can store reflections on what worked and what didn't, then retrieve those reflections to improve future behavior. Reflexion ([Shinn et al., 2023](https://arxiv.org/abs/2303.11366)) demonstrated this clearly: an agent that stores verbal self-critiques in an episodic buffer improves across trials *without any weight updates*. The learning lives entirely in prompt-time language.

**Skill accumulation.** Rather than remembering facts, some agents remember *how to do things*. Voyager ([Wang et al., 2023](https://arxiv.org/abs/2305.16291)) builds a growing library of executable code skills in Minecraft, retrieving relevant skills as reusable action abstractions for future tasks. Agent Workflow Memory ([Wang et al., 2024](https://arxiv.org/abs/2409.07429)) generalizes this to web navigation, inducing reusable workflows from prior trajectories.

**User modeling.** Persistent agents need to adapt to individual users — their preferences, habits, communication style. This is the personalization dimension, covered by systems like HiMeS ([hippocampus-inspired](https://arxiv.org/abs/2501.11768)) and benchmarked by PERMA ([event-driven preference evaluation](https://arxiv.org/abs/2502.13379)) and BenchPreS ([preference selectivity](https://arxiv.org/abs/2502.16729)).

**World knowledge organization.** Agents that operate over time accumulate knowledge about their environment — project states, team dynamics, codebase patterns. Generative Agents ([Park et al., 2023](https://arxiv.org/abs/2304.03442)) showed this at scale: 25 agents maintaining memory streams of observations, synthesizing reflections, and using them to plan socially coherent behavior over multiple simulated days.

## A Taxonomy of Memory Types

The literature draws on cognitive science to classify agent memory, though the boundaries are blurry in practice:

### By Duration
- **Short-term / working memory** — the current context window. What the agent sees right now. Fast, limited, volatile.
- **Long-term memory** — anything that persists beyond the current session. Must be explicitly stored and retrieved.

### By Content
- **Episodic memory** — records of specific events: "on Tuesday, the user asked about deployment, and we discovered the config was wrong." Time-stamped, situated.
- **Semantic memory** — distilled facts and knowledge: "the user prefers Python over TypeScript" or "the production database is PostgreSQL 15." Timeless, abstracted.
- **Procedural memory** — how to do things: skill libraries, workflows, tool-use patterns. Executable or semi-executable.

### By Structure
- **Flat** — unstructured text buffers, conversation logs, append-only stores.
- **Structured** — key-value pairs, structured triples, tagged entries.
- **Graph** — nodes and edges representing entities and relationships. See Graph Memory.
- **Hierarchical** — tiered systems with different levels of abstraction or access speed. See Hierarchical Memory.

The survey by Wu et al. ([2026](https://arxiv.org/abs/2604.01707)) unifies existing methods into a modular framework and finds that *combinations* of these types often outperform any single approach — the best memory system is usually a hybrid.

## The Lifecycle of Memory

Memory isn't just storage and retrieval. It's a cycle:

1. **Extraction** — what gets remembered? Not everything should be stored. UMEM ([Ye et al., 2025](https://arxiv.org/abs/2505.06126)) shows that bad memory often starts at extraction time, not retrieval time. The agent must decide what's worth keeping.

2. **Storage** — how is it organized? Flat buffers are simple but don't scale. Graph structures capture relationships. Hierarchical designs offer different granularities. The choice shapes what queries are possible later.

3. **Retrieval** — how does the agent find relevant memories? Recency, relevance, importance scoring (as in Generative Agents). Semantic search, temporal filtering, associative traversal. This is where most systems succeed or fail in practice.

4. **Consolidation** — how does memory evolve over time? Raw memories are compressed, contradictions resolved, stale facts pruned. See [Memory Consolidation & Lifecycle](memory-consolidation.md). This is where biology offers powerful analogies — sleep-time consolidation, Ebbinghaus forgetting curves, hippocampal replay.

5. **Evolution** — the memory system itself adapts. Topology changes (All-Mem, [Lv et al., 2026](https://arxiv.org/abs/2501.04770)), retrieval strategies update, the balance between tiers shifts. A living memory system, not a frozen one.

The graph-memory taxonomy by Yang et al. ([2026](https://arxiv.org/abs/2602.05665)) organizes the literature around this lifecycle, showing that most systems focus on only one or two stages while neglecting the others.

## Why This Is Hard

Several factors make agent memory genuinely difficult:

**The context window is not memory.** It's tempting to treat a large context window as memory: just dump everything in. But context windows are expensive per-token, don't persist between sessions, and their effective attention degrades with length ([Lost in the Middle](https://arxiv.org/abs/2307.03172)). Real memory requires selective persistence and retrieval.

**RAG is not memory either.** Retrieval-Augmented Generation retrieves relevant chunks at query time, but it re-derives knowledge from scratch every time. There's no accumulation, no synthesis, no contradiction detection. (See the raw notes in [`../notes/memory/`](../notes/memory/).)

**Evaluation is fragmented.** There's no agreed-upon benchmark for agent memory. Different papers test on different tasks with different metrics. The evaluation papers in our corpus — Mem-Gallery, Mem2ActBench, PERMA, BenchPreS, VehicleMemBench, MemoryRewardBench — each probe different aspects.

**Security is an afterthought.** If an agent trusts its own memories, and those memories can be poisoned by adversarial input, the agent can be persistently compromised. Zombie Agents ([Yang et al., 2024](https://arxiv.org/abs/2407.15054)) showed that a single injection can become self-reinforcing across sessions. See [Memory Security](memory-security.md).

## The State of the Field

As of mid-2026, agent memory is in a rapid expansion phase. The number of papers has grown from a handful of foundational works in 2023 (Reflexion, Generative Agents, MemGPT, Voyager) to dozens of specialized systems in 2025–2026 targeting specific memory types, architectures, and domains.

Key trends:
- **Graph structures are winning** for relational and entity-centric memory. Multiple 2025–2026 systems (A-MEM, GAAMA, Mnemis) use graph-based approaches.
- **Hierarchical designs are maturing** from simple two-tier (working + archival) to multi-level systems with explicit consolidation stages.
- **Security is emerging as a first-class concern**, with both attack papers (Zombie Agents, ER-MIA, Memory Poisoning) and defense papers (AgentSys, SuperLocalMemory) appearing.
- **Benchmarks are proliferating but not converging** — the field lacks a standard evaluation protocol.
- **Production deployment is real but early** — Mem0 and Letta (the company behind MemGPT) are the most visible deployed systems.

The gap between research and practice remains wide. Most papers demonstrate memory on constrained tasks or benchmarks. Building memory that works in a real, long-running agent — with messy inputs, adversarial environments, and months of accumulated state — is a different challenge entirely. That's what we're working on.

---

## Papers Referenced

| Paper | Year | Key Contribution |
|-------|------|-----------------|
| [Reflexion](https://arxiv.org/abs/2303.11366) | 2023 | Verbal self-reflection as episodic memory |
| [Generative Agents](https://arxiv.org/abs/2304.03442) | 2023 | Memory stream + reflection + planning loop |
| [Voyager](https://arxiv.org/abs/2305.16291) | 2023 | Executable skill library as memory |
| [MemGPT](https://arxiv.org/abs/2310.08560) | 2023 | OS-inspired virtual context management |
| [Agent Workflow Memory](https://arxiv.org/abs/2409.07429) | 2024 | Reusable workflows from trajectories |
| [Zombie Agents](https://arxiv.org/abs/2407.15054) | 2024 | Persistent memory poisoning attacks |
| [Mem0](https://arxiv.org/abs/2504.19413) | 2025 | Production persistent memory with fact extraction |
| [UMEM](https://arxiv.org/abs/2505.06126) | 2025 | Unified memory extraction framework |
| [All-Mem](https://arxiv.org/abs/2501.04770) | 2026 | Topology-evolving lifelong memory |
| [Graph Memory Taxonomy](https://arxiv.org/abs/2602.05665) | 2026 | Survey of graph-based memory approaches |
| [Memory in the LLM Era](https://arxiv.org/abs/2604.01707) | 2026 | Unified comparison framework for memory methods |

---

*See also: [Memory Consolidation & Lifecycle](memory-consolidation.md) · [Memory Security](memory-security.md) · the raw notes in [`../notes/memory/`](../notes/memory/) and the [agent-memory atlas](../notes/atlas-agent-memory.md).*
