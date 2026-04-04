# Agent Memory on arXiv (2023-2026)

This folder is a **systematic working corpus** for papers on **deployed / inference-time memory** in AI agents, LLM agents, conversational agents, and embodied agents.

It currently contains **37 paper notes**:
- **Pass 1:** a core mechanism-focused corpus (21 papers)
- **Pass 2:** a broader sweep adding more 2026 mechanisms, benchmarks/evaluation papers, surveys/taxonomies, and memory-security papers (16 more)

## Scope
- **Source:** arXiv only
- **Date window:** 2023-01-01 through 2026-04-04
- **Preference:** ICL-style or prompt-time memory (retrieved experiences, workflows, summaries, skills)
- **Also included:** other live-agent memory mechanisms (episodic / semantic / hierarchical / personalization memory)
- **Pass-two expansion:** benchmark, survey, taxonomy, and security papers that are directly useful for understanding or evaluating deployed memory systems
- **Excluded by default:** papers centered on pretraining, fine-tuning, or memory architectures without a deployed-agent angle

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

## Still likely candidates for a future pass
This corpus is much broader after pass two, but it is still not the last word. Good future targets include:
- `HiMeS`, `HyMem`, `BenchPreS`, `VehicleMemBench`
- `SuperLocalMemory`, `Mind Your HEARTBEAT`, `MemBuilder`, `MemoryRewardBench`
- any additional 2026 papers that refine graph, temporal, or persona-memory evaluation after the current cutoff date
