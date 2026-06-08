# SkillReducer: Optimizing LLM Agent Skills for Token Efficiency

**Paper:** [arXiv:2603.29919](https://arxiv.org/abs/2603.29919)
**Authors:** Yudong Gao, Zongjie Li, Yuanyuan Yuan, Zimo Ji, Pingchuan Ma, Shuai Wang
**Affiliations:** HKUST, Tsinghua University, Zhejiang University of Technology
**Date:** March 2026

## One-Line Summary

55K skills are bloated — 26% have no routing description, 60%+ of body content is non-actionable; compressing them by 39–48% actually *improves* quality by 2.8% (less-is-more effect).

## Core Idea

Skills (SKILL.md files, context files, microagents) are the pre-packaged instructions that extend coding agent capabilities. They're meant to save tokens by encapsulating reusable knowledge. Ironically, **skills as currently written often increase token consumption** — they're bloated with background explanations, redundant examples, and non-actionable filler.

SkillReducer does two things:
1. **Empirical study** of 55,315 public skills: measures the problem's severity.
2. **Optimization framework** that compresses skills while preserving (and improving) their functional quality.

The central finding: a **less-is-more effect** where removing non-essential content reduces distraction in the context window and actually makes the agent perform better.

## The Problem (Empirical Study)

### 55,315 skills analyzed from three sources

| Source | Count | Description |
|--------|-------|-------------|
| Wild (GitHub) | 55,315 | Public repos with SKILL.md files |
| SkillHub (marketplace) | 100 | Editorially curated skills |
| Community (forums) | 620 | Developer-shared skills |

### What's wrong with them

**Routing layer (descriptions):**
- **26.4%** of skills have no description at all — the routing mechanism can never match them, so their tokens are wasted on every call
- **44.1%** are missing or under 20 tokens
- Existing descriptions are often verbose with non-routing content (feature lists, usage examples, trigger phrase enumerations)

**Body content breakdown:**

| Content Type | Percentage | Role |
|-------------|------------|------|
| Core rules | 38.5% | Actionable instructions the agent must follow |
| Background | 40.7% | Explanations and rationale (non-actionable) |
| Examples | 12.9% | Illustrative code snippets |
| Templates | 7.6% | Boilerplate for copy-paste |
| Redundant | 0.3% | Repeated content |

Over 60% of body content (background + examples + templates + redundant) is not directly actionable. Every non-actionable token is attention dilution and monetary cost.

**Reference files:**
- 14.8% of skills include external reference files
- These can inject tens of thousands of tokens per invocation
- Average reference overlap with the body is 34% — a third of reference content is already in the skill body

## Method: SkillReducer

### Stage 1: Description optimization

Uses **adversarial delta debugging** — treats semantic clauses in a description as elements and uses DDMIN algorithm to find the minimal subset that preserves routing correctness.

Two phases:
1. **Fast compression:** Segment description → binary-search minimal routing-preserving subset → selectively rewrite surviving units shorter
2. **Real-agent validation:** Test compressed descriptions against actual agent routing. If routing breaks, selectively restore removed units.

Result: **48% mean description compression** (56.5% for existing descriptions, 44.6% for generated ones).

### Stage 2: Body restructuring (Progressive Disclosure)

Inspired by program slicing — identify which content directly affects task execution, defer the rest.

1. **Content classification:** LLM classifies each paragraph into core rule / background / example / template / redundant
2. **Type-specific compression:**
   - Core rules → merge by semantic similarity, tighten into concise bullets
   - Examples → group by concept, keep only one representative per concept (60–70% reduction)
   - Templates → deduplicate by concept
   - Background → summarize to concise paragraph preserving facts
   - Redundant → discard
3. **Progressive disclosure:** Core rules stay in always-loaded body. Examples, templates, and background become on-demand reference files loaded only when the agent explicitly requests them via `read_file`.
4. **Cross-file deduplication:** Remove overlap between reference files and the body.

### Self-correcting feedback loop

Two quality gates:
- **Gate 1 (faithfulness):** LLM verifies compressed core preserves all actionable instructions from the original.
- **Gate 2 (task evaluation):** Run actual tasks against compressed vs. original skill. If compressed underperforms, promote missing items back to core. Loop at most twice.

Result: **39% mean body compression**, with quality *improvement* of 2.8%.

## Results

### Compression

| Component | Mean Reduction | Median |
|-----------|---------------|--------|
| Description | 48.0% | 59.0% |
| Body | 39.0% | 43.0% |
| SkillsBench bodies | 75.0% (curated skills are more compressible) | — |
| Wild skills (Gate 1 only) | 77.5% | 81.5% |

End-to-end token savings: **26.8%** in the best case.

### Quality: the less-is-more effect

| Metric | Score |
|--------|-------|
| Compressed (C) vs. Original (A) | C > A in **25.3%** of cases, C < A in **14.0%** |
| Mean quality: No skill (D) | 0.684 |
| Mean quality: Original skill (A) | 0.722 |
| Mean quality: **Compressed skill (C)** | **0.742** |
| Statistical significance | p=0.002 (Wilcoxon), d=0.107 |

**The compressed version outperforms the original.** Removing non-actionable content doesn't just save tokens — it reduces noise in the context window, letting the agent focus on what matters.

### Cross-model transfer

Tested across 5 models from 4 families:
- Mean retention: **0.965** (compressions made with one model transfer to others)
- Also generalizes to an independent agent framework

### Cost

Compressing 600 skills costs ~$14–18 total. One-time expense amortized within a few hundred invocations per skill.

## Concrete Example

**marketing-strategy-pmm skill:**
- Stage 1: description 87 → 32 tokens (63% reduction). DDMIN finds trigger-phrase list is redundant — router infers triggers from keywords alone.
- Stage 2: 2,543-token body classified into:
  - Core rules (KPIs, methodology, decision criteria) → 540 tokens
  - On-demand: templates.md (327 tok), examples.md (684 tok), background.md (602 tok)
- End-to-end: **12,019 → 540 tokens** for core-only tasks (95.5% reduction)
- Quality: compressed scores 1.0 vs. original's 0.93 — **compression improved it**

## Arguments and Key Claims

1. **Skills are a new class of software artifact.** They're authored, versioned, shared via marketplaces, and maintained — but lack the optimization ecosystem that traditional code enjoys. SkillReducer starts that ecosystem.

2. **The routing layer is broken at scale.** 26.4% of skills can never be routed to because they have no description. Even well-described skills waste tokens on non-routing content.

3. **Progressive disclosure > monolithic injection.** Instead of dumping everything into the context window, keep the actionable core always loaded and let the agent pull examples/templates/background on demand. Same idea as lazy loading in software.

4. **The less-is-more effect is real and measurable.** Removing 39% of body content improves quality by 2.8% (p=0.002). Non-actionable content is not just wasteful — it actively hurts by diluting attention.

5. **Delta debugging works for prompt optimization.** Adapting DDMIN from test-case minimization to description compression is novel and effective — it finds the minimal set of semantic units that preserve routing.

## Why This Matters for OpenHands / SmolPaws

**Direct implications for our skill system:**

1. **SmolPaws skills should be audited.** How much of each SKILL.md is core rules vs. background/examples? The paper suggests >60% is non-actionable in typical skills.

2. **Progressive disclosure pattern.** Instead of loading entire skills into context, load only the core rules. Let the agent `read_file` for examples or templates when needed. This maps naturally to OpenHands' file system — put examples in a sibling file.

3. **Description quality matters for routing.** Every skill needs a concise, routing-optimized description. Missing or verbose descriptions waste the routing budget.

4. **Context loading review.** SmolPaws loads IDENTITY.md, SOUL.md, TOOLS.md, MEMORY.md, HEARTBEAT.md, USER.md, etc. on every conversation. How much of this is "core rules" vs. "background"? The SOUL.md origin story is beautiful but is it actionable?

5. **Automated compression.** SkillReducer's pipeline could be applied to our own skills. $14–18 to compress 600 skills is trivial.

## Relationship to Other Papers

| Paper | Focus | Shared finding |
|-------|-------|----------------|
| Evaluating AGENTS.md (2602.11988) | Context files hurt more than help | Less is more — unnecessary context is harmful |
| SkillsBench (in this repo) | Benchmark for skill quality | Used as external evaluation set |
| SkillOpt (in this repo) | Optimize skill *content* via rollout reflection | Complementary — SkillOpt edits skill text, SkillReducer compresses structure |

## Caveats / Limits

- Evaluation uses single-model compression (DeepSeek-V3) with cross-model transfer validation — but compression quality might vary with the compressor model.
- The "less-is-more" effect could partly be a measurement artifact: compressed skills are evaluated by the same type of LLM that generated them.
- Gate 2 task evaluation uses auto-generated tasks, not real-world usage scenarios.
- The paper doesn't study the interaction between multiple simultaneously loaded skills — which is the real-world scenario.
- Wild skill scalability test uses Gate 1 only (faithfulness, no task evaluation), so the 77.5% compression for wild skills is less validated than the 39% on the evaluation set.

## Key Quotes

> "26.4% lack routing descriptions entirely, over 60% of body content is non-actionable, and reference files can inject tens of thousands of tokens per invocation."

> "SkillReducer achieves 48% description compression and 39% body compression while improving functional quality by 2.8%, revealing a less-is-more effect."

> "Removing non-essential content reduces distraction in the context window."

> "A 10,000-token skill costs $0.03 to $0.15 per invocation, and teams with frequent agent usage can spend hundreds of dollars monthly on skill content alone."
