# Agent Memory on arXiv (2023-2026)

This folder is a **systematic working corpus** for papers on **deployed / inference-time memory** in AI agents, LLM agents, conversational agents, and embodied agents.

It currently contains **79 paper notes** (plus the legacy [Memory and RAG Papers](./memory-and-rag.md) reading list kept in this folder):
- **Pass 1:** a core mechanism-focused corpus (21 papers)
- **Pass 2:** a broader sweep adding more 2026 mechanisms, benchmarks/evaluation papers, surveys/taxonomies, and memory-security papers (16 more)
- **Pass 3:** a breadth pass adding more personalization, systems, benchmark, and security papers from the remaining 2026 candidate pool (10 more)
- **Post-cutoff targeted additions:** requested later papers recorded separately from the systematic three-pass corpus (9)
- **Later additions:** memory platforms/engines, further lifecycle mechanisms, further benchmarks, and further security work added after the passes (23)

## Scope
- **Source:** arXiv only
- **Date window:** systematic passes cover 2023-01-01 through 2026-04-04; explicitly requested later papers are listed as post-cutoff targeted additions
- **Preference:** ICL-style or prompt-time memory (retrieved experiences, workflows, summaries, skills)
- **Also included:** other live-agent memory mechanisms (episodic / semantic / hierarchical / personalization memory)
- **Pass-two expansion:** benchmark, survey, taxonomy, and security papers that are directly useful for understanding or evaluating deployed memory systems
- **Pass-three expansion:** additional personalization, memory-systems, reward-model, and multi-user evaluation papers from the remaining 2026 pool
- **Excluded by default:** papers centered on pretraining, fine-tuning, or memory architectures without a deployed-agent angle

## Related working lists
- [Memory and RAG Papers](./memory-and-rag.md) is a broader legacy reading list that mixes memory, RAG, and prompting references; it is kept here because its center of gravity is memory/retrieval rather than long-context prompting or skills.

## Search method used so far
### Pass 1: core mechanism sweep
1. Sweep arXiv title/abstract with overlapping query families:
   - `agent memory`, `LLM memory`, `long-term memory`, `episodic memory`, `working memory`, `persistent memory`, `memory bank`
   - memory-adjacent terms for agent work that often behaves like memory without saying so directly: `reflection`, `experience`, `workflow`, `skill library`, `context management`
2. Deduplicate results across query families.
3. Screen abstracts for:
   - inference-time / deployed use,
   - explicit memory mechanism or memory-management contribution,
   - relevance to agents / multi-session assistants / embodied agents.
4. Keep a **core first pass** of papers whose primary contribution is a reusable memory mechanism or memory organization strategy.

### Pass 2: broader supporting sweep
1. Revisit the remaining candidate pool with extra emphasis on:
   - `graph memory`, `hierarchical memory`, `temporal memory`, `lifelong memory`
   - `benchmark`, `evaluation`, `taxonomy`, `survey`
   - `memory poisoning`, `memory injection`, `persistent control`, `memory security`
2. Add papers that are not core mechanisms but are still directly useful for:
   - comparing memory systems,
   - evaluating structure or memory-to-action behavior,
   - understanding attack surfaces of persistent memory.

### Pass 3: breadth expansion over the remaining 2026 pool
1. Add more papers from the unresolved candidate list with emphasis on:
   - personalization and selective-memory use,
   - memory as a systems / latency / lifecycle problem,
   - reward-model or benchmark infrastructure for memory evaluation,
   - additional privacy / pollution / poisoning defenses.
2. Keep the same one-note-per-paper format so the corpus remains navigable while breadth increases.

## Notes on borderline papers
A few files are tagged as **borderline include** because they are clearly about deployed agent memory but also rely on learned memory controllers or RL-tuned memory-management policies. They were kept so the corpus does not erase an important current trend in the literature.

## Included papers

### Core mechanisms from pass 1
#### 2023
- [Reflexion](./reflexion-language-agents-with-verbal-reinforcement-learning.md)
- [Generative Agents](./generative-agents-interactive-simulacra-of-human-behavior.md)
- [MemoryBank](./memorybank-enhancing-large-language-models-with-long-term-memory.md)
- [Voyager](./voyager-an-open-ended-embodied-agent-with-large-language-models.md)
- [ExpeL](./expel-llm-agents-are-experiential-learners.md)
- [MemGPT](./memgpt-towards-llms-as-operating-systems.md)

#### 2024
- [Agent Workflow Memory](./agent-workflow-memory.md)

#### 2025
- [A-MEM](./a-mem-agentic-memory-for-llm-agents.md)
- [Mem0](./mem0-building-production-ready-ai-agents-with-scalable-long-term-memory.md)

#### 2026
- [BMAM](./bmam-brain-inspired-multi-agent-memory-framework.md)
- [MemCtrl](./memctrl-using-mllms-as-active-memory-controllers-on-embodied-agents.md)
- [AgentSys](./agentsys-secure-and-dynamic-llm-agents-through-explicit-hierarchical-memory-management.md)
- [M2A](./m2a-multimodal-memory-agent-with-dual-layer-hybrid-memory-for-long-term-personalized-interactions.md)
- [TraceMem](./tracemem-weaving-narrative-memory-schemata-from-user-conversational-traces.md)
- [UMEM](./umem-unified-memory-extraction-and-management-framework-for-generalizable-memory.md)
- [REMem](./remem-reasoning-with-episodic-memory-in-language-agent.md)
- [PlugMem](./plugmem-a-task-agnostic-plugin-memory-module-for-llm-agents.md)
- [Omni-SimpleMem](./omni-simplemem-autoresearch-guided-discovery-of-lifelong-multimodal-agent-memory.md)
- [DeltaMem](./deltamem-towards-agentic-memory-management-via-reinforcement-learning.md)
- [ByteRover](./byterover-agent-native-memory-through-llm-curated-hierarchical-context.md)
- [Hierarchical Memory Orchestration](./hierarchical-memory-orchestration-for-personalized-persistent-agents.md)

### Pass-two mechanism additions
- [HiMem](./himem-hierarchical-long-term-memory-for-llm-long-horizon-agents.md)
- [Hippocampus](./hippocampus-an-efficient-and-scalable-memory-module-for-agentic-ai.md)
- [Mnemis](./mnemis-dual-route-retrieval-on-hierarchical-graphs-for-long-term-llm-memory.md)
- [Chronos](./chronos-temporal-aware-conversational-agents-with-structured-event-retrieval-for-long-term-memory.md)
- [All-Mem](./all-mem-agentic-lifelong-memory-via-dynamic-topology-evolution.md)
- [Memori](./memori-a-persistent-memory-layer-for-efficient-context-aware-llm-agents.md)
- [GAAMA](./gaama-graph-augmented-associative-memory-for-agents.md)

### Pass-two benchmarks / evaluation / meta papers
- [Mem-Gallery](./mem-gallery-benchmarking-multimodal-long-term-conversational-memory-for-mllm-agents.md)
- [Mem2ActBench](./mem2actbench-a-benchmark-for-evaluating-long-term-memory-utilization-in-task-oriented-autonomous-agents.md)
- [Evaluating Memory Structure in LLM Agents](./evaluating-memory-structure-in-llm-agents.md)
- [PERMA](./perma-benchmarking-personalized-memory-agents-via-event-driven-preference-and-realistic-task-environments.md)
- [Graph-based Agent Memory: Taxonomy, Techniques, and Applications](./graph-based-agent-memory-taxonomy-techniques-and-applications.md)
- [Memory in the LLM Era: Modular Architectures and Strategies in a Unified Framework](./memory-in-the-llm-era-modular-architectures-and-strategies-in-a-unified-framework.md)

### Pass-two security / robustness papers
- [Memory Poisoning Attack and Defense on Memory Based LLM-Agents](./memory-poisoning-attack-and-defense-on-memory-based-llm-agents.md)
- [ER-MIA](./er-mia-black-box-adversarial-memory-injection-attacks-on-long-term-memory-augmented-large-language-models.md)
- [Zombie Agents](./zombie-agents-persistent-control-of-self-evolving-llm-agents-via-self-reinforcing-injections.md)

### Pass-three mechanism / systems additions
- [AMA](./ama-adaptive-memory-via-multi-agent-collaboration.md)
- [HyMem](./hymem-hybrid-memory-architecture-with-dynamic-retrieval-scheduling.md)
- [AMV-L](./amv-l-lifecycle-managed-agent-memory-for-tail-latency-control-in-long-running-llm-systems.md)

### Pass-three borderline training-heavy additions
- [MemBuilder](./membuilder-reinforcing-llms-for-long-term-memory-construction-via-attributed-dense-rewards.md)
- [HiMeS](./himes-hippocampus-inspired-memory-system-for-personalized-ai-assistants.md)

### Pass-three benchmarks / evaluation papers
- [MemoryRewardBench](./memoryrewardbench-benchmarking-reward-models-for-long-term-memory-management-in-large-language-models.md)
- [BenchPreS](./benchpres-a-benchmark-for-context-aware-personalized-preference-selectivity-of-persistent-memory-llms.md)
- [VehicleMemBench](./vehiclemembench-an-executable-benchmark-for-multi-user-long-term-memory-in-vehicle-agents.md)

### Pass-three security / privacy papers
- [SuperLocalMemory](./superlocalmemory-privacy-preserving-multi-agent-memory-with-bayesian-trust-defense-against-memory-poisoning.md)
- [Mind Your HEARTBEAT](./mind-your-heartbeat-claw-background-execution-inherently-enables-silent-memory-pollution.md)

### Post-cutoff targeted additions
- [ReHarness](./reharness-recurrent-agentic-continual-learning.md) — later feedback repairs retrieved reflections using their original sources; fixed weights, streaming evaluation, nonzero grounding leakage and output-token cost caveat. Full paper/appendices read.
- [Can a Language Model Learn Facts Continually in Its Weights?](./can-a-language-model-learn-facts-continually-in-its-weights.md)
- [WikiSkill: Compiling Agent Experience into Persistent Knowledge for Skill Evolution](./wikiskill-compiling-agent-experience-into-persistent-knowledge-for-skill-evolution.md) — Google; three-layer raw/wiki/skills workspace; ablations show the persistent wiki (not the skill edits) carries most of the gain.
- [The Compaction Cliff in Long-Running AI Agent Memory](./the-compaction-cliff-in-long-running-ai-agent-memory.md) — compaction summarizes safety rules at the same rate as logs (53%→10% over 5 rounds); Knowledge Triage routes each knowledge type through its own retention policy.
- [Context as an Environment (Scroll)](./context-as-an-environment-scroll-programmatic-context-management.md) — Alibaba; session = append-only event log + persistent Python kernel; model programs its own context, only printed projections enter the prompt; eviction is recoverable.
- [Recuris: Recursive Experiential-Working Memory Evolution](./recuris-recursive-experiential-working-memory-evolution.md) — split working/experiential memory grounds skill selection in current state and localizes failures to a memory component; validation-gated meta-agent updates.
- [Trace as State](./trace-as-state-reasoning-traces-as-conditional-states.md) — placing the reasoning trace *before* the long context (not appended after) lifts long-context accuracy up to ~50 pts; training-free ordering rule.
- [Selective Forgetting](./selective-forgetting-graph-based-memory-framework.md) — myth-busting: at matched retrieval budget, graph memory *loses* to a flat vector baseline on LongMemEval (F1 0.42 vs 0.47); the validated pruning module removes ~10% of nodes with no quality loss.
- [Runtime-Independent Persistent Agents](./runtime-independent-persistent-agents.md) — SmolPaws' own thesis, formalized: persistent (identity, memory, code) vs. replaceable (model, harness, host); migration preserves lineage; mechanical continuity ≠ behavioral invariance.

### Later additions — memory systems and platforms
- [Letta](./letta-stateful-agents-platform.md) — the platform built by the MemGPT authors (OSS + commercial); "advanced memory that can learn and self-improve."
- [Zep](./zep-temporal-knowledge-graph-architecture-for-agent-memory.md) — temporal knowledge-graph memory layer; open-source engine Graphiti; beats MemGPT on Deep Memory Retrieval.
- [Supermemory](./supermemory-memory-and-context-engine.md) — "the memory and context layer for AI"; SDK + MCP server + local binary, with drive connectors.
- [Cognee](./cognee-ai-memory-platform.md) — self-hosted agent-memory platform (Apache-2.0) with an active community.
- [GBrain](./gbrain-opinionated-agent-brain.md) — Garry Tan's opinionated "company brain" (TypeScript, MIT); the one we run locally.

### Later additions — mechanisms and lifecycle
- [MemCog](./memcog-from-memory-as-tool-to-memory-as-cognition-in-conversational-agents.md) — memory is cognition you do, not a tool you call; reasoning over memory rather than retrieving from it.
- [Beyond Semantic Organization](./beyond-semantic-organization-memory-as-execution-state-management-for-long.md) — memory as execution state to manage, not a knowledge base to search.
- [ReCMem](./recmem-recurrence-based-memory-consolidation-for-efficient-and-effective-long.md) — recurrence-based consolidation: repeated passes each distill memory further.
- [Sleep-Time Compute](./sleep-time-compute-beyond-inference-scaling-at-test-time.md) — think offline about a context before queries arrive; ~5× less test-time compute at equal accuracy.
- [Auto-Dreamer](./auto-dreamer-learning-offline-memory-consolidation-for-language-agents.md) — first paper to learn a consolidation policy for offline memory processing; directly validates the sleep-time pattern.
- [Rethinking How to Remember](./rethinking-how-to-remember-beyond-atomic-facts-in-lifelong-llm-agent-memory.md) — atomic facts are the wrong unit of memory; richer context-preserving representations win.
- [MemoryWire](./memorywire-a-vendor-neutral-wire-format-for-agent-memory-operations.md) — a vendor-neutral wire format for memory operations, so frameworks can interoperate.
- [MyLM](./mylm-self-personalizing-lm-weight-memory.md) — memory in the weights: a small self-personalizing LM (MLX), code-only experiment.

### Later additions — benchmarks and evaluation
- [EvoMemBench](./evomembench-benchmarking-agent-memory-from-a-self-evolving-perspective.md) — does memory actually make the agent better over time? Tests self-evolution, not just recall.
- [MemGym](./memgym-a-long-horizon-memory-environment-for-llm-agents.md) — tests memory as it forms during execution, not recall of pre-stored facts.
- [Cross-Scenario Generality](./exploring-cross-scenario-generality-of-agentic-memory-systems-diagnostics-and-a.md) — most memory systems are overfit to their benchmark; cross-scenario testing exposes the gaps.
- [Agent Memory Characterization](./agent-memory-characterization-and-system-implications-of-stateful-long-horizon.md) — treats memory as a systems workload to characterize and optimize, not only an AI capability.

### Later additions — security and robustness
- [Hijacking Agent Memory](./hijacking-agent-memory-stealthy-trojan-attacks-through-conversational.md) — stealthy trojan attack; 0.95 ASR against modern selective memory pipelines.
- [MemAudit](./memaudit-post-hoc-auditing-of-poisoned-agent-memory-via-causal-attribution-and.md) — detect-after-the-fact: audit a memory store for poisoning without needing write-time prevention.
- [MemLineage](./memlineage-lineage-guided-enforcement-for-llm-agent-memory.md) — every memory entry gets cryptographic provenance plus derivation lineage.
- [OEP](./oep-poisoning-self-evolving-llm-agents-via-locally-correct-but-non-transferable.md) — poisons the consolidation process itself: locally correct experiences become globally harmful rules.
- [Taming Zombie Agents](./taming-zombie-agents-a-markov-state-aware-framework-for-resilient-multi-agent.md) — state-aware transitions let agents recover from transient failures instead of being written off.
- [Beyond Similarity](./beyond-similarity-trustworthy-memory-search-for-personal-ai-agents.md) — memory search should weigh trust, not just relevance.

## Still likely candidates for a future pass
This corpus is broad after pass three, but it is still not literally exhaustive. Good future targets include:
- additional post-cutoff 2026 papers that refine graph, temporal, persona, or multi-user memory evaluation
- later 2026 work that extends privacy-preserving memory or memory-contamination defenses
- any strong new benchmark papers that become standard references for evaluating long-term deployed memory
