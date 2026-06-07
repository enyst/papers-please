# Prompt Enforcement — Compiling Instructions into Deterministic Safety

This folder tracks research on **deterministic enforcement of agent instructions** — the idea that natural-language rules ("don't delete my database", "authenticate before accessing data") should be compiled into deterministic checks (hooks, monitors, capability guards) rather than relying on the LLM's probabilistic compliance.

## The Core Insight

LLMs are probabilistic. When a user writes "never delete production data" in a system prompt, the model will *usually* comply — but "usually" is not "always." The agent might hallucinate a reason to violate the rule, misinterpret it, or simply forget it deep in a long context.

The solution: **use a good model to interpret instructions, then generate deterministic enforcement mechanisms** — git hooks, file system guards, API permission checks, action validators — that make violations *impossible*, not just *unlikely*.

## Business Idea: Prompt Shield

A service that:
1. Takes agent instructions/system prompts/skills as input
2. Uses a frontier model to interpret and extract safety constraints
3. Generates deterministic enforcement scripts/hooks (e.g., for Claude Code, OpenHands, Cursor)
4. Installs them as pre-execution validators

Example: "do not modify files in /prod" → a file system hook that blocks writes to `/prod/*` regardless of what the LLM decides.

## Papers

### Closest Prior Art
- **[AgentSpec](agentspec-customizable-runtime-enforcement-for-safe-and-reliable-llm-agents.md)** — natural-language specs → formal runtime monitors. The most direct existing work.
- **[VeriGuard](veriguard-enhancing-llm-agent-safety-via-verified-code-generation.md)** — formal verification of generated code wrappers. Strongest guarantees.

### Constraint Enforcement
- **[Enforcing Temporal Constraints](enforcing-temporal-constraints-for-llm-agents.md)** — action ordering rules enforced deterministically.
- **[Agent libOS](agent-libos-a-library-os-inspired-runtime-for-capability-controlled-llm-agents.md)** — OS-level capability isolation for agents.
- **[Data Flow Control](data-flow-control-data-safety-policies-for-ai-agents.md)** — data safety policies at the infrastructure level.
- **[AgenTRIM](agentrim-tool-risk-mitigation-for-agentic-ai.md)** — tool permission management for agents.

### Theoretical Foundations
- **[Position: AI Safety Requires Effective Controllability](position-ai-safety-requires-effective-controllability.md)** — alignment is not controllability.
- **[Auditing Agent Harness Safety](auditing-agent-harness-safety.md)** — harness-level safety auditing.

## Key Open Questions
- How well can a model parse arbitrary natural-language instructions into formal constraints?
- What enforcement hooks are available across different agent frameworks?
- Can we make a universal enforcement layer that works with Claude Code, OpenHands, Cursor, etc.?
- What's the right granularity — per-action checks vs. pre-execution plan validation?
