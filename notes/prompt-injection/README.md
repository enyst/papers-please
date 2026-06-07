# Prompt Injection — Attacks, Defenses, and the State of the Art

This folder tracks research on prompt injection in LLM agents — the fundamental vulnerability where untrusted input is confused with trusted instructions.

**Status as of June 2026:** Still an unsolved research problem. Every defense approach has fundamental limitations. The field is in an arms race where attacks consistently outpace defenses.

## The Problem

LLMs process instructions and data in the same channel (natural language). There is no hardware-level separation between "what the user told me to do" and "what this web page says." An attacker who controls any input the agent reads can potentially hijack the agent's behavior.

For agents specifically, this is worse than for chatbots because:
- Agents have **tools** — an injected instruction can trigger real-world actions (file deletion, API calls, data exfiltration)
- Agents have **memory** — an injection can persist across sessions (see [memory security](../memory/) papers)
- Agents have **autonomy** — they browse, read, and process untrusted content without human oversight

## Defense Approaches — Overview

### 1. Detection/Classification (Pre-filter)
**Idea:** Train a classifier to detect injection attempts before they reach the main model.

| Aspect | Assessment |
|--------|-----------|
| **How it works** | Neural classifier (GuardNet) or rule-based filter scans input for injection patterns |
| **Pros** | Low latency; model-agnostic; works as a pre-filter; cheap to run |
| **Cons** | **Probabilistic** — can always be evaded; needs training data; false positives block legitimate queries; arms race with attackers |
| **Fundamental limit** | It's a classifier, not a guarantee. Adversarial examples exist for any classifier. |
| **Papers** | [GuardNet](guardnet-ensemble-strategies-of-shallow-neural-networks-for-robust-prompt.md) |

### 2. Activation Analysis (White-box Detection)
**Idea:** Monitor the model's internal activations to detect when it's about to execute an injected command.

| Aspect | Assessment |
|--------|-----------|
| **How it works** | Inspect model activations mid-inference; detect exfiltration patterns before output |
| **Pros** | Catches attacks *before* output; deeper signal than text-level detection; works for multi-turn attacks |
| **Cons** | Requires model internals (white-box only); may not transfer across models; adds inference latency |
| **Fundamental limit** | Only works if you have access to model weights. Closed API models (GPT, Claude) are opaque. |
| **Papers** | [Caught in the Act(ivation)](caught-in-the-act-ivation-toward-pre-output-and-multi-turn-detection-of.md) |

### 3. Semantic Isolation / Virtualization
**Idea:** Separate untrusted data from trusted instructions at the semantic level — give data its own "namespace."

| Aspect | Assessment |
|--------|-----------|
| **How it works** | Wrap untrusted content in semantic markers the model is trained to respect as data-only |
| **Pros** | Principled separation; works against indirect injection; no classifier needed |
| **Cons** | Requires framework integration; may reduce reasoning quality over untrusted content; novel, limited validation |
| **Fundamental limit** | Still relies on the model respecting the semantic boundary — which is a *training* property, not a *guarantee*. |
| **Papers** | [AgentVisor](agentvisor-defending-llm-agents-against-prompt-injection-via-semantic.md) |

### 4. Information Flow Analysis
**Idea:** Borrow taint tracking from programming language security — track which data flows came from untrusted sources and restrict what they can influence.

| Aspect | Assessment |
|--------|-----------|
| **How it works** | Treat the LLM as a program boundary; apply dataflow analysis to track tainted inputs |
| **Pros** | Principled (PL security foundations); can be automated; catches flows no other method sees |
| **Cons** | Requires program analysis tooling; LLM is opaque (breaks dataflow chain); early-stage |
| **Fundamental limit** | The LLM is a black box in the dataflow — you can't track taint *through* it, only around it. |
| **Papers** | [Where Code Meets NL](where-code-meets-natural-language-taxonomy-driven-information-flow-analysis-for.md) |

### 5. Network/Infrastructure-Level Guards
**Idea:** Filter at the tool/MCP/API boundary rather than at the prompt level.

| Aspect | Assessment |
|--------|-----------|
| **How it works** | Inspect and filter tool calls, API requests, and supply-chain inputs at the infrastructure layer |
| **Pros** | Framework-level; catches supply-chain attacks; composable; works with any model |
| **Cons** | Doesn't help with direct injection; requires per-tool integration; reactive to known patterns |
| **Fundamental limit** | Only guards the boundary, not the reasoning. A sufficiently clever injection can produce tool calls that look legitimate. |
| **Papers** | [ShieldNet](shieldnet-network-level-guardrails-against-emerging-supply-chain-injections-in.md) |

### 6. Endogenous Security Awareness
**Idea:** Train the agent itself to recognize and resist injection — make security awareness part of the model.

| Aspect | Assessment |
|--------|-----------|
| **How it works** | Fine-tune or prompt the agent to detect injection patterns and refuse to comply |
| **Pros** | No external infrastructure; agent-native; can adapt to novel attacks; moves with the model |
| **Cons** | **Still probabilistic** — can be overridden by strong injections; hard to validate exhaustively; training may degrade on edge cases |
| **Fundamental limit** | You're asking the model to police itself. A strong enough adversary can always find the boundary between "legitimate unusual request" and "injection." |
| **Papers** | [ClawdGo](poster-clawdgo-endogenous-security-awareness-training-for-autonomous-ai-agents.md) |

### 7. Red-teaming + Integration-Aware Defense
**Idea:** Dynamically red-team the agent in its actual tool environment, then build defenses aware of the integration context.

| Aspect | Assessment |
|--------|-----------|
| **How it works** | Automated adversarial testing against real SaaS integrations; defenses tuned to specific tool combinations |
| **Pros** | Realistic threat model; integration-aware; finds real vulnerabilities; dynamic |
| **Cons** | Expensive to run; SaaS-specific; may not cover novel tool combinations; reactive |
| **Fundamental limit** | Red-teaming finds known-unknown vulnerabilities. Unknown-unknowns remain. |
| **Papers** | [AgentRedBench](agentredbench-dynamic-redteaming-and-integration-aware-defense-for-llm-agents.md) |

### 8. Deterministic Enforcement (see [prompt-enforcement/](../prompt-enforcement/))
**Idea:** Don't try to detect injection — instead, compile instructions into deterministic checks that make violations impossible regardless of what the model decides.

| Aspect | Assessment |
|--------|-----------|
| **How it works** | Parse safety instructions → generate hooks, monitors, capability guards at the execution layer |
| **Pros** | **Deterministic** — not probabilistic; can't be evaded by clever prompting; defense doesn't depend on model behavior |
| **Cons** | Only works for *enforceable* constraints (file access, tool permissions); can't enforce "be helpful" or "don't be rude"; requires framework hook points |
| **Fundamental limit** | Can only enforce constraints that are expressible as deterministic checks. Many safety properties (tone, relevance, correctness) are not. |
| **Papers** | [AgentSpec](../prompt-enforcement/agentspec-customizable-runtime-enforcement-for-safe-and-reliable-llm-agents.md), [VeriGuard](../prompt-enforcement/veriguard-enhancing-llm-agent-safety-via-verified-code-generation.md) |

## The Honest Assessment

No single defense solves prompt injection. The fundamental issue is that LLMs process instructions and data in the same modality (natural language), and there is no way to create a perfect separation within the model.

**What works best in practice:** Defense in depth — layers of different approaches:
1. Deterministic enforcement for hard constraints (don't delete X, don't access Y)
2. Detection classifiers as a pre-filter for obvious attacks
3. Semantic isolation for separating data from instructions
4. Infrastructure guards at tool/API boundaries
5. Memory isolation for persistent state (see [AgentSys](../memory/agentsys-secure-and-dynamic-llm-agents-through-explicit-hierarchical-memory-management.md))
6. Human-in-the-loop for high-stakes actions

**What doesn't work:** Relying on any single layer. Every defense has been demonstrated to be bypassable in isolation.

**The unsolved part:** Detecting *novel* injections that don't match known patterns, and preventing injections that produce tool calls indistinguishable from legitimate ones. This may require fundamental changes to how LLMs process instructions vs. data — not just better guardrails on top.

## Connection to Prompt Shield

The Prompt Shield idea (see [prompt-enforcement/](../prompt-enforcement/)) occupies layer 1 — the deterministic enforcement layer. It's the strongest individual layer because it doesn't depend on the model's behavior. But it only handles enforceable constraints. A complete defense still needs the other layers for everything else.
