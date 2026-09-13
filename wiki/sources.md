# Source Corpus

63 papers from arXiv (2023–2026) on deployed/inference-time memory in AI agents. Each paper has been read, annotated, and integrated into the topic articles in this wiki.

**Scope:** ICL-style and prompt-time memory — retrieved experiences, workflows, summaries, skills. Also episodic, semantic, hierarchical, and personalization memory. Benchmarks, surveys, and security papers where they directly inform the synthesis. Papers centered on pretraining or fine-tuning are excluded.

---

## 2023 — Foundations

| Paper | Citation | One-line take |
|-------|----------|--------------|
| [ExpeL: LLM Agents Are Experiential Learners](https://arxiv.org/abs/2308.10144) | Zhao et al., 2023 | Makes the case that agents can learn from prior episodes through retrieved language insights, not parameter updates. |
| [Generative Agents: Interactive Simulacra of Human Behavior](https://arxiv.org/abs/2304.03442) | Park et al., 2023 | Introduces the observation-memory-reflection-planning loop that made long-horizon believable agent behavior a concrete systems pattern. |
| [MemGPT: Towards LLMs as Operating Systems](https://arxiv.org/abs/2310.08560) | Packer et al., 2023 | Frames long-term agent memory as a systems problem: who decides what stays in active context and what gets paged out. |
| [MemoryBank: Enhancing Large Language Models with Long-Term Memory](https://arxiv.org/abs/2305.10250) | Zhong et al., 2023 | An early long-term dialogue memory system that treats persistent conversational memory as a first-class runtime component. |
| [Reflexion: Language Agents with Verbal Reinforcement Learning](https://arxiv.org/abs/2303.11366) | Shinn et al., 2023 | A foundational paper for experience-as-text memory: the agent improves across trials by remembering verbal critiques instead of updating weights. |
| [Voyager: An Open-Ended Embodied Agent with Large Language Models](https://arxiv.org/abs/2305.16291) | Wang et al., 2023 | A canonical example of memory as reusable executable skill rather than raw text or retrieved facts. |

## 2024 — Expanding the Pattern

| Paper | Citation | One-line take |
|-------|----------|--------------|
| [Agent Workflow Memory](https://arxiv.org/abs/2409.07429) | Wang et al., 2024 | Treats memory as reusable routines rather than isolated facts, which is especially compelling for web and tool-using agents. |

## 2025 — Scaling Up

| Paper | Citation | One-line take |
|-------|----------|--------------|
| [A-MEM: Agentic Memory for LLM Agents](https://arxiv.org/abs/2502.12110) | Xu et al., 2025 | A memory-first design that pushes beyond flat retrieval by letting the agent build and revise a linked note graph over time. |
| [Mem0: Building Production-Ready AI Agents with Scalable Long-Term Memory](https://arxiv.org/abs/2504.19413) | Chhikara et al., 2025 | A production-leaning memory architecture built around selective extraction and retrieval of salient conversational facts. |

## 2026 — The Explosion

### Mechanisms

| Paper | Citation | One-line take |
|-------|----------|--------------|
| [All-Mem: Agentic Lifelong Memory via Dynamic Topology Evolution](https://arxiv.org/abs/2501.04770) | Lv et al., 2026 | Treats lifelong memory as a topology that can evolve without destructively collapsing old evidence. |
| [AMA: Adaptive Memory via Multi-Agent Collaboration](https://arxiv.org/abs/2601.20352) | Huang et al., 2026 | A multi-agent memory manager that adapts retrieval granularity and actively repairs inconsistent memory. |
| [AMV-L: Lifecycle-Managed Agent Memory for Tail-Latency Control](https://arxiv.org/abs/2603.04443) | Bamidele, 2026 | Focused on working-set control and tail-latency stability rather than just answer quality. |
| [BMAM: Brain-inspired Multi-Agent Memory Framework](https://arxiv.org/abs/2601.09264) | Zhang et al., 2026 | Builds a dual episodic/semantic store and explores encoding, consolidation, and retrieval across agent pools. |
| [ByteRover: Agent-Native Memory Through LLM-Curated Hierarchical Context](https://arxiv.org/abs/2603.03420) | Shen et al., 2026 | Lets the agent organically shape a hierarchical context tree instead of requiring a fixed memory schema. |
| [Chronos: Temporal-Aware Conversational Agents](https://arxiv.org/abs/2602.07694) | Chen et al., 2026 | Adds temporal structure to conversational memory so the agent can reason about when things happened. |
| [DeltaMem: Towards Agentic Memory Management via RL](https://arxiv.org/abs/2502.09747) | Gao et al., 2026 | An RL-trained memory policy that decides what to remember, forget, and update. |
| [GAAMA: Graph Augmented Associative Memory for Agents](https://arxiv.org/abs/2602.09548) | He et al., 2026 | A graph-augmented memory bank with associative retrieval designed for multi-hop reasoning over accumulated context. |
| [Hierarchical Memory Orchestration for Personalized Persistent Agents](https://arxiv.org/abs/2603.15942) | Hu et al., 2026 | Combines hierarchical memory with personalization — adaptive layering of short/long-term stores tuned to individual users. |
| [HiMem: Hierarchical Long-Term Memory for LLM Long-Horizon Agents](https://arxiv.org/abs/2601.20831) | Dorbala et al., 2026 | Memory as a budgeting problem: what should survive online when context is scarce. |
| [Hippocampus: An Efficient and Scalable Memory Module for Agentic AI](https://arxiv.org/abs/2602.01658) | Chen et al., 2026 | Bio-inspired efficient memory module with hippocampal replay mechanisms. |
| [HyMem: Hybrid Memory Architecture with Dynamic Retrieval Scheduling](https://arxiv.org/abs/2601.19382) | Zhao et al., 2026 | Combines multiple memory types with a dynamic scheduler that picks the retrieval strategy per query. |
| [M2A: Multimodal Memory Agent with Dual-Layer Hybrid Memory](https://arxiv.org/abs/2602.07776) | Chen et al., 2026 | Extends memory to multimodal inputs — text, images, audio — with dual-layer organization. |
| [MemCtrl: Using MLLMs as Active Memory Controllers on Embodied Agents](https://arxiv.org/abs/2602.15453) | Yang et al., 2026 | Uses multimodal LLMs as active memory controllers for embodied agents — deciding what to remember from visual/sensor input. |
| [Memori: A Persistent Memory Layer for Efficient, Context-Aware LLM Agents](https://arxiv.org/abs/2603.19935) | Borro et al., 2026 | Frames persistent memory as a data-structuring layer that can sit above whichever LLM API you use. |
| [Mnemis: Dual-Route Retrieval on Hierarchical Graphs](https://arxiv.org/abs/2602.15313) | Tang et al., 2026 | System 1 + System 2 memory retrieval: fast associative lookup plus deliberate graph traversal. |
| [Omni-SimpleMem: Autoresearch-Guided Discovery of Lifelong Multimodal Agent Memory](https://arxiv.org/abs/2604.01007) | Liu et al., 2026 | Autonomous research can discover strong lifelong-memory system designs. |
| [PlugMem: A Task-Agnostic Plugin Memory Module](https://arxiv.org/abs/2603.03296) | Yang et al., 2026 | The right memory unit is often abstract knowledge, not raw trajectory text. |
| [REMem: Reasoning with Episodic Memory in Language Agent](https://arxiv.org/abs/2602.13530) | Shu et al., 2026 | Not just retrieval, but reasoning over remembered events. |
| [TraceMem: Weaving Narrative Memory Schemata](https://arxiv.org/abs/2602.09712) | Shu et al., 2026 | Turns conversation history into evolving narrative structure instead of snippets. |
| [UMEM: Unified Memory Extraction and Management Framework](https://arxiv.org/abs/2602.10652) | Ye et al., 2026 | Bad memory often starts at extraction time, not retrieval time. |

### Personalization & Training-Heavy

| Paper | Citation | One-line take |
|-------|----------|--------------|
| [HiMeS: Hippocampus-inspired Memory System for Personalized AI Assistants](https://arxiv.org/abs/2501.11768) | Xu et al., 2026 | Bio-inspired memory for personal AI with hippocampal consolidation. |
| [MemBuilder: Reinforcing LLMs for Long-Term Memory Construction](https://arxiv.org/abs/2601.19515) | Deng et al., 2026 | RL-tuned memory construction that builds better memories via reward signals. |

### Surveys & Taxonomies

| Paper | Citation | One-line take |
|-------|----------|--------------|
| [Graph-based Agent Memory: Taxonomy, Techniques, and Applications](https://arxiv.org/abs/2602.05665) | Yang et al., 2026 | Maps the graph-memory subfield by memory lifecycle stage. |
| [Memory in the LLM Era: Modular Architectures and Strategies](https://arxiv.org/abs/2604.01707) | Wu et al., 2026 | Unified comparison framework — combinations often outperform single approaches. |
| [Evaluating Memory Structure in LLM Agents](https://arxiv.org/abs/2601.14578) | Wu et al., 2026 | Memory quality is partly about structure (ledgers, trees), not just fact recall. |

### Benchmarks & Evaluation

| Paper | Citation | One-line take |
|-------|----------|--------------|
| [BenchPreS: Personalized Preference Selectivity Benchmark](https://arxiv.org/abs/2502.16729) | Seo et al., 2026 | Tests whether agents can selectively apply learned preferences vs. generic knowledge. |
| [Mem-Gallery: Benchmarking Multimodal Long-Term Conversational Memory](https://arxiv.org/abs/2601.14571) | Wang et al., 2026 | Multimodal benchmark for conversational memory across text and images. |
| [Mem2ActBench: Long-Term Memory Utilization in Task-Oriented Agents](https://arxiv.org/abs/2601.12716) | Qian et al., 2026 | Measures whether stored memories actually drive correct task actions. |
| [MemoryRewardBench: Benchmarking Reward Models for Memory Management](https://arxiv.org/abs/2601.11969) | Tang et al., 2026 | Can we evaluate memory management well with current reward models? |
| [PERMA: Event-Driven Preference and Realistic Task Environments](https://arxiv.org/abs/2603.23231) | Liu et al., 2026 | Pushes personalized memory evaluation beyond needle-in-a-haystack. |
| [VehicleMemBench: Multi-User Long-Term Memory in In-Vehicle Agents](https://arxiv.org/abs/2603.23840) | Chen et al., 2026 | Executable multi-user benchmark judged by real environment outcomes. |

### Security & Robustness

| Paper | Citation | One-line take |
|-------|----------|--------------|
| [AgentSys: Secure Agents Through Hierarchical Memory Management](https://arxiv.org/abs/2602.07398) | Wen et al., 2026 | Memory management as a security boundary problem, not just relevance-ranking. |
| [ER-MIA: Black-Box Adversarial Memory Injection Attacks](https://arxiv.org/abs/2602.15344) | Piehl et al., 2026 | Black-box attacks that exploit the embed-and-retrieve pipeline. |
| [Memory Poisoning Attack and Defense](https://arxiv.org/abs/2601.05504) | Sunil et al., 2026 | Foundational attack/defense catalog for memory-based agents. |
| [Mind Your HEARTBEAT: Silent Memory Pollution via Background Execution](https://arxiv.org/abs/2503.16248) | Zhang et al., 2026 | Background execution expands the memory pollution attack surface. |
| [SuperLocalMemory: Privacy-Preserving Multi-Agent Memory with Bayesian Trust](https://arxiv.org/abs/2503.01945) | Bhardwaj, 2026 | Local-first infrastructure with trust defense, not just attack analysis. |
| [Zombie Agents: Persistent Control via Self-Reinforcing Injections](https://arxiv.org/abs/2602.15654) | Yang et al., 2026 | Cross-session memory turns one-time exposure into durable compromise. |

## 2026 Q2 — Pass Four (May–June 2026)

### Consolidation & Lifecycle

| Paper | Citation | One-line take |
|-------|----------|--------------|
| [Auto-Dreamer: Learning Offline Memory Consolidation](https://arxiv.org/abs/2605.20616) | Zhang et al., 2026 | The first paper to explicitly learn a consolidation policy for offline sleep-time compute. |
| [RecMem: Recurrence-based Memory Consolidation](https://arxiv.org/abs/2605.16045) | Li et al., 2026 | Iterative consolidation passes that compress memory like a recurrent network. |
| [Rethinking How to Remember: Beyond Atomic Facts](https://arxiv.org/abs/2605.19952) | Chen et al., 2026 | Atomic facts are the wrong unit — richer representations preserving context outperform. |

### Architecture & Paradigm

| Paper | Citation | One-line take |
|-------|----------|--------------|
| [Agent Memory: System Implications of Stateful Long-Horizon Workloads](https://arxiv.org/abs/2606.06448) | — , 2026 | Agent memory as a systems workload to characterize and optimize. |
| [Beyond Semantic Organization: Memory as Execution State](https://arxiv.org/abs/2606.06090) | — , 2026 | Memory is not a knowledge base to search but an execution state to manage. |
| [MemCog: From Memory-as-Tool to Memory-as-Cognition](https://arxiv.org/abs/2605.28046) | Li et al., 2026 | Memory access as integral reasoning, not one-shot retrieval. SOTA on LoCoMo (92.98) and LongMemEval (95.8). |
| [memorywire: A Vendor-Neutral Wire Format for Agent Memory](https://arxiv.org/abs/2606.01138) | — , 2026 | A standard wire format so memory frameworks can interoperate. |

### Security

| Paper | Citation | One-line take |
|-------|----------|--------------|
| [Hijacking Agent Memory: Stealthy Trojan Attacks](https://arxiv.org/abs/2605.29960) | Wang et al., 2026 | Defeats selective memory extraction with 0.95 ASR. |
| [OEP: Poisoning via Locally Correct Experiences](https://arxiv.org/abs/2605.18930) | Wang et al., 2026 | Poisons the consolidation process itself — locally correct experiences become harmful rules. |
| [MemAudit: Post-hoc Auditing of Poisoned Agent Memory](https://arxiv.org/abs/2605.23723) | — , 2026 | Detect-after-the-fact via causal attribution and structural anomaly detection. |
| [MemLineage: Lineage-Guided Enforcement](https://arxiv.org/abs/2605.14421) | Ouyang & Hou, 2026 | Every memory entry gets cryptographic provenance plus derivation lineage. |
| [Beyond Similarity: Trustworthy Memory Search](https://arxiv.org/abs/2606.06054) | — , 2026 | Trust-aware retrieval beyond semantic similarity. |
| [Taming "Zombie" Agents: Markov State-Aware Framework](https://arxiv.org/abs/2605.17348) | Zhang et al., 2026 | State-aware transitions let agents recover from transient failures. |

### Benchmarks

| Paper | Citation | One-line take |
|-------|----------|--------------|
| [MemGym: Long-Horizon Memory Environment](https://arxiv.org/abs/2605.20833) | Xu et al., 2026 | Tests dynamic memory formation during execution, not just retrieval of stored facts. |
| [EvoMemBench: Self-Evolving Perspective](https://arxiv.org/abs/2605.18421) | — , 2026 | Does memory actually make the agent better over time? |
| [Cross-Scenario Generality of Agentic Memory Systems](https://arxiv.org/abs/2606.04315) | Chen et al., 2026 | Most memory systems are overfit to their benchmark. |

---

*Back to [Index](index.md)*
