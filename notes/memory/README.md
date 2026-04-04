# Agent Memory on arXiv (2023-2026)

This folder is a **systematic first-pass corpus** for papers on **deployed / inference-time memory** in AI agents, LLM agents, conversational agents, and embodied agents.

## Scope
- **Source:** arXiv only
- **Date window:** 2023-01-01 through 2026-04-04
- **Preference:** ICL-style or prompt-time memory (retrieved experiences, workflows, summaries, skills)
- **Also included:** other live-agent memory mechanisms (episodic / semantic / hierarchical / personalization memory)
- **Excluded by default:** papers centered on pretraining, fine-tuning, or memory architectures without a deployed-agent angle

## Search method used for this pass
1. Sweep arXiv title/abstract with overlapping query families:
   - `agent memory`, `LLM memory`, `long-term memory`, `episodic memory`, `working memory`, `persistent memory`, `memory bank`
   - memory-adjacent terms for agent work that often behaves like memory without saying so directly: `reflection`, `experience`, `workflow`, `skill library`, `context management`
2. Deduplicate results across query families.
3. Screen abstracts for:
   - inference-time / deployed use,
   - explicit memory mechanism or memory-management contribution,
   - relevance to agents / multi-session assistants / embodied agents.
4. Keep a **core first pass** of papers whose primary contribution is a reusable memory mechanism or memory organization strategy.

## Notes on borderline papers
A few files are tagged as **borderline include** because they are clearly about deployed agent memory but also rely on learned memory controllers or RL-tuned memory-management policies. They were kept so the corpus does not erase an important current trend in the literature.

## Included papers
### 2023
- [Reflexion](./reflexion-language-agents-with-verbal-reinforcement-learning.md)
- [Generative Agents](./generative-agents-interactive-simulacra-of-human-behavior.md)
- [MemoryBank](./memorybank-enhancing-large-language-models-with-long-term-memory.md)
- [Voyager](./voyager-an-open-ended-embodied-agent-with-large-language-models.md)
- [ExpeL](./expel-llm-agents-are-experiential-learners.md)
- [MemGPT](./memgpt-towards-llms-as-operating-systems.md)

### 2024
- [Agent Workflow Memory](./agent-workflow-memory.md)

### 2025
- [A-MEM](./a-mem-agentic-memory-for-llm-agents.md)
- [Mem0](./mem0-building-production-ready-ai-agents-with-scalable-long-term-memory.md)

### 2026
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

## Deliberately not in this first-pass note set
These are worth a later pass, but were left out of the one-file-per-paper core corpus because they are surveys, taxonomies, or evaluation/meta papers rather than mechanism papers:
- *Memory in the LLM Era: Modular Architectures and Strategies in a Unified Framework* (survey)
- *Evaluating Memory Structure in LLM Agents* (evaluation)
- *Graph-based Agent Memory: Taxonomy, Techniques, and Applications* (taxonomy)

## Suggested next additions after this PR
If this sub-project grows, the next arXiv sweep should inspect newer 2026 work around `HiMem`, `Chronos`, `Hippocampus`, `All-Mem`, and related persistent-memory benchmarks to decide which deserve one-note-per-paper treatment.
