# Memory Security

The more useful agent memory becomes, the more dangerous it becomes. Every paper in this wiki describes a system where the agent *trusts its own memories*. But if those memories can be poisoned — by adversarial web content, by a malicious user in a multi-tenant system, by a compromised tool output — then persistent memory turns a one-time attack into a permanent backdoor.

This isn't theoretical. The attack papers in this corpus demonstrate working exploits against real memory architectures. And the defense papers suggest that this problem is fundamentally harder than per-session prompt injection defense, because the attack surface *compounds over time*.

## The Threat Model

Traditional prompt injection is ephemeral: the attacker gets one shot per conversation, and the injection disappears when the session ends. Memory changes this in three ways:

1. **Persistence.** A poisoned memory survives across sessions. The agent carries the attacker's payload forward indefinitely.
2. **Self-reinforcement.** If the agent writes memories based on its own behavior, and its behavior is influenced by poisoned memories, the poison can strengthen itself over time.
3. **Delayed activation.** The injection and the exploit can be separated in time. Poison injected during a benign task can trigger weeks later in a completely different context.

## Attack Vectors

### Zombie Agents: Self-Reinforcing Persistent Control

The most alarming result in the corpus. Yang et al. ([2026](https://arxiv.org/abs/2602.15654)) show that a single indirect injection — through an attacker-controlled web page that the agent reads during a normal task — can be written into the agent's long-term memory through the agent's own normal update process. Once there, the payload persists across sessions and can trigger unauthorized tool use later.

The attack works in two phases:
- **Infection:** the agent reads poisoned content while completing a benign task. The payload is crafted to look like useful information, so the agent stores it as memory.
- **Trigger:** in a later session, the poisoned memory is retrieved (or carried forward) and causes the agent to execute attacker-controlled actions.

The paper designs persistence strategies specific to common memory architectures — sliding-window memory, retrieval-augmented memory — that resist the natural defenses of truncation and relevance filtering. The conclusion is stark: **per-session prompt filtering is not sufficient for agents with persistent memory.**

### ER-MIA: Black-Box Memory Injection

Piehl et al. ([2026](https://arxiv.org/abs/2602.15344)) demonstrate a different angle: adversarial memory injection attacks that work in a black-box setting, without knowledge of the memory system's internals. The attack exploits the embed-and-retrieve pipeline that most long-term memory systems use — crafting inputs that, once embedded, will be retrieved in contexts the attacker chooses.

This is particularly concerning because it works against systems where the attacker cannot directly observe or modify the memory store. The attacker only needs the ability to provide input that the agent processes normally.

### Memory Poisoning: Attack and Defense

The foundational attack-and-defense paper by the Memory Poisoning team ([2025](https://arxiv.org/abs/2502.02563)) catalogs multiple attack vectors against memory-based agents and proposes initial defense mechanisms. It establishes that the problem is real, measurable, and not solved by existing prompt-safety techniques.

### Silent Memory Pollution via Background Execution

"Mind Your HEARTBEAT" ([2026](https://arxiv.org/abs/2503.16248)) — yes, that title hits close to home — shows that agents running background processes (heartbeats, scheduled checks, autonomous browsing) can have their memory silently polluted through content encountered during those autonomous operations. The paper specifically targets the Claw framework pattern where background execution inherently expands the attack surface.

This matters because the most useful agents are autonomous ones — the ones that check Slack, browse the web, monitor systems without being asked. Those same autonomy features create windows where adversarial content can enter memory without any human in the loop.

## Defense Approaches

### Memory Isolation: AgentSys

The most architecturally principled defense comes from AgentSys (Wen et al., [2026](https://arxiv.org/abs/2602.07398)). Inspired by OS process memory isolation, it organizes agents hierarchically: a main agent spawns worker agents for tool calls, each running in an isolated memory context. External data and tool outputs never directly enter the main agent's memory — only schema-validated return values can cross isolation boundaries through deterministic JSON parsing.

Results: isolation alone cuts attack success to 2.19%. Adding a validator/sanitizer further improves defense. The key insight is that **memory management is a security boundary problem, not just a relevance-ranking problem.** Don't try to detect poisoned memories — prevent untrusted content from reaching memory in the first place.

### Privacy-Preserving Multi-Agent Memory: SuperLocalMemory

SuperLocalMemory ([2026](https://arxiv.org/abs/2503.01945)) takes a defense-in-depth approach for multi-agent systems. It adds Bayesian trust scoring to memory operations: memories from untrusted or low-confidence sources get lower trust scores and are either quarantined or given less weight at retrieval time.

The system demonstrates trust separation (gap = 0.90) and 72% trust degradation for detected sleeper attacks. It also addresses GDPR compliance with erasure support — a practical concern that most research papers ignore.

### What Defense Looks Like in Practice

From the papers and our own experience building SmolPaws, effective memory security requires multiple layers:

1. **Input isolation.** Don't let raw external content write directly to memory. Validate, summarize, and filter at the boundary. AgentSys's hierarchical isolation is the strongest version of this.

2. **Source tracking.** Every memory entry should know where it came from. Memories derived from untrusted sources (web content, tool outputs, messages from unknown senders) get different trust levels than memories derived from the agent's own reasoning or from trusted humans.

3. **Anomaly detection.** Monitor memory writes for patterns that look like injection: instructions embedded in what should be factual content, formatting that triggers tool use, content that references the agent's own capabilities or tools.

4. **Consolidation as defense.** The [consolidation process](memory-consolidation.md) is a natural defense point. When the agent "dreams" — reviewing, compressing, and reorganizing memories — it can detect inconsistencies, flag suspicious content, and prune memories that don't cohere with the agent's overall knowledge.

5. **Humans in the loop.** For high-stakes memory operations (tool execution triggered by retrieved memory, changes to persistent configuration), require human confirmation. Not as a default for everything — that defeats the purpose of autonomy — but as a circuit breaker for sensitive actions.

### Memory Auditing: MemAudit

What if prevention fails? MemAudit ([2026](https://arxiv.org/abs/2605.23723)) takes a detect-after-the-fact approach: use causal attribution and structural anomaly detection to identify poisoned entries in an existing memory store. Instead of trying to prevent every poisoned write (which the attack papers show is extremely hard), periodically audit the memory store for signs of compromise. This complements prevention-based defenses with a detection layer.

### Cryptographic Provenance: MemLineage

MemLineage ([Ouyang & Hou, 2026](https://arxiv.org/abs/2605.14421)) attaches both cryptographic provenance and LLM-mediated derivation lineage to every memory entry. At retrieval time, the system can enforce policies based on where a memory came from and how it was derived. This is the strongest per-entry defense in the corpus — every memory gets a birth certificate.

### Trust-Aware Retrieval

"Beyond Similarity: Trustworthy Memory Search" ([2026](https://arxiv.org/abs/2606.06054)) adds trust dimensions to memory search beyond semantic similarity — provenance, recency, confidence, and user verification status. The insight: retrieval should consider *trust*, not just *relevance*. A highly relevant but untrusted memory is worse than a moderately relevant trusted one.

### Consolidation as Attack Surface

Perhaps the most unsettling recent finding: OEP ([Wang et al., 2026](https://arxiv.org/abs/2605.18930)) shows that the consolidation process itself — which we earlier described as a defense point — can be an attack vector. The attack constructs adversarial experiences that are *locally correct* but *non-transferable*: they work in the specific context where they were created but fail catastrophically when the agent generalizes from them. During memory consolidation, the agent over-trusts its own reflections and distills these localized experiences into high-priority but over-generalized rules. ASR above 50% against GPT-4o agents.

This directly complicates the "consolidation as defense" narrative. Yes, consolidation is a checkpoint where you can detect anomalies. But it's also a moment of vulnerability where the agent is making high-stakes decisions about what to keep, what to generalize, and what to discard.

### Stealthy Trojan Injection: MemPoison

Hijacking Agent Memory ([Wang et al., 2026](https://arxiv.org/abs/2605.29960)) demonstrates MemPoison, which bypasses selective memory extraction mechanisms that were thought to provide some protection. The attack uses semantic relational bridges (binding triggers to payloads as coherent statements), entity masquerading (triggers that look like named entities to resist rewriting), and joint embedding optimization (creating tight clusters in embedding space while maintaining stealth). Attack success rate: 0.95 against real memory pipelines. The paper evaluates multiple defense strategies and "demonstrates their fundamental limitations."

## Open Problems

**No standard threat model.** The attack papers use different assumptions about attacker capabilities (black-box vs. white-box, direct vs. indirect injection, single-shot vs. persistent access). The field needs a shared threat taxonomy.

**Defense vs. utility tradeoff.** Strict isolation prevents attacks but also prevents useful memory. If tool outputs can never enter memory, the agent can't learn from tool use. The right balance is domain-dependent and not well characterized.

**Multi-session evaluation.** Most security evaluations test single sessions. The real threat from memory poisoning unfolds over multiple sessions — the poison persists, reinforces, and triggers later. Evaluation protocols need to match this.

**Self-evolving agents.** The most capable agents update their own memory, prompts, and even code over time. This makes them both more powerful and more vulnerable. A poisoned memory in a self-evolving agent can alter the agent's behavior in ways that further entrench the poison.

**Consolidation is both defense and attack surface.** OEP shows that the dreaming/consolidation step where agents generalize from experience can be exploited. We need consolidation processes that are skeptical of their own inputs — which is a hard design problem.

---

## Papers Referenced

| Paper | Year | Key Contribution |
|-------|------|-----------------|
| [Memory Poisoning Attack and Defense](https://arxiv.org/abs/2502.02563) | 2025 | Foundational attack/defense catalog |
| [Zombie Agents](https://arxiv.org/abs/2602.15654) | 2026 | Self-reinforcing persistent memory attacks |
| [ER-MIA](https://arxiv.org/abs/2602.15344) | 2026 | Black-box memory injection via embeddings |
| [AgentSys](https://arxiv.org/abs/2602.07398) | 2026 | Hierarchical memory isolation as defense |
| [Mind Your HEARTBEAT](https://arxiv.org/abs/2503.16248) | 2026 | Silent pollution through background execution |
| [SuperLocalMemory](https://arxiv.org/abs/2503.01945) | 2026 | Bayesian trust defense for multi-agent memory |
| [Hijacking Agent Memory (MemPoison)](https://arxiv.org/abs/2605.29960) | 2026 | Stealthy trojans that bypass selective extraction |
| [OEP](https://arxiv.org/abs/2605.18930) | 2026 | Consolidation-time poisoning via correct-but-non-transferable experiences |
| [MemAudit](https://arxiv.org/abs/2605.23723) | 2026 | Post-hoc auditing via causal attribution |
| [MemLineage](https://arxiv.org/abs/2605.14421) | 2026 | Cryptographic provenance + derivation lineage |
| [Trustworthy Memory Search](https://arxiv.org/abs/2606.06054) | 2026 | Trust-aware retrieval beyond semantic similarity |

---

*See also: [Memory Consolidation](memory-consolidation.md) (consolidation as a defense mechanism) · [What Is Agent Memory?](what-is-agent-memory.md) · the raw notes in [`../notes/memory/`](../notes/memory/) and the [agent-memory atlas](../notes/atlas-agent-memory.md).*
