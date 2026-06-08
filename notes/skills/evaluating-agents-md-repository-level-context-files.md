# Evaluating AGENTS.md: Are Repository-Level Context Files Helpful for Coding Agents?

**Paper:** [arXiv:2602.11988](https://arxiv.org/abs/2602.11988)
**Authors:** Thibaud Gloaguen, Niels Mündler, Mark Müller, Veselin Raychev, Martin Vechev
**Affiliations:** ETH Zürich, Cursor
**Date:** February 2026

## One-Line Summary

Context files (AGENTS.md, CLAUDE.md) tend to *reduce* task success rates and increase cost by 20% — unnecessary requirements make tasks harder, and less is more.

## Core Idea

Everyone's doing it: writing AGENTS.md or CLAUDE.md files to tell coding agents how to work in a repository. Agent developers (OpenAI, Anthropic) strongly recommend it. Over 60,000 repos have context files. But nobody had actually measured whether they help.

This paper does the measurement. The answer is uncomfortable: **LLM-generated context files hurt performance more often than they help**, and even human-written context files only provide marginal improvement — while costing 20%+ more in inference.

## Method

### Two evaluation settings

1. **SWE-bench Lite** (300 tasks from popular repos) — no developer context files exist, so the authors test with LLM-generated ones following each agent vendor's recommended setup commands.
2. **AGENT BENCH** (new, 138 tasks from 12 repos) — all repos have real developer-committed context files. Tests three conditions: no context file, LLM-generated, and human-written.

### Agents tested

- Claude Code with Sonnet-4.5
- Codex with GPT-5.2 and GPT-5.1 Mini
- Qwen Code with Qwen3-30B-Coder

### Three settings per benchmark

| Setting | Description |
|---------|-------------|
| None | No context file |
| LLM | Auto-generated context file (each agent's recommended init command) |
| Human | Developer-committed context file (AGENT BENCH only) |

## Results

### LLM-generated context files: mostly harmful

- **5 out of 8** agent/benchmark combinations show *lower* success rates with LLM-generated context files vs. no context.
- Average resolution rate drops: −0.5% on SWE-bench Lite, −2% on AGENT BENCH.
- Cost increases in *every* setting: +20% on SWE-bench Lite, +23% on AGENT BENCH.
- Agents take more steps (2.5–4 more per task on average).

### Human-written context files: marginal improvement

On AGENT BENCH (the only benchmark with real human-written files):
- Human context files slightly improve resolution rates vs. no context in most settings.
- But the improvement is small and inconsistent across agents/models.
- Cost still increases compared to no context.

### Behavioral analysis

Context files change *how* agents work, even when they don't improve *outcomes*:
- **More thorough testing:** agents run tests more frequently and explore more files.
- **Agents obey the instructions:** when told to run specific commands or follow patterns, they do — even when those instructions are counterproductive for the specific task.
- **Broader exploration:** more file traversal, more tool calls, but not necessarily more success.

## Key Findings

1. **Less is more.** The paper's central conclusion: unnecessary requirements in context files make tasks harder. A context file that says "always run the full test suite" or "follow this specific code style" adds constraints that don't help (and often hurt) for any given task.

2. **LLM-generated context files are worse than nothing.** Auto-generating a context file with the vendor's recommended command and model produces bloated, generic instructions that distract the agent.

3. **Agents are too obedient.** When a context file says to do something, agents do it — even when task-level judgment would suggest otherwise. This is especially costly when the instructions are wrong or irrelevant.

4. **Cost overhead is consistent.** Context files always increase inference cost (more tokens in, more steps taken), regardless of whether they improve outcomes. The 20%+ cost increase is the most reliable finding.

5. **Human-written > LLM-generated, but barely.** Developer-committed context files slightly outperform auto-generated ones, suggesting humans better understand what's worth saying. But even human files don't consistently beat "no context."

## Why This Matters for OpenHands / SmolPaws

This is directly relevant to how we write AGENTS.md files and skills.

**Implications:**
- **Keep context files minimal.** Don't dump every possible instruction. Focus on things the agent genuinely can't figure out from the codebase alone.
- **Don't auto-generate context files.** The LLM-generated versions are actively harmful. If you want a context file, write it yourself with specific, minimal, task-relevant instructions.
- **Avoid unnecessary constraints.** "Always run tests before committing" sounds helpful but costs tokens and steps on tasks where it's irrelevant. Let the agent decide.
- **Skills have the same risk.** A verbose skill loaded into the context window faces the same problem: every non-actionable token is attention dilution and cost overhead.
- **SmolPaws' context loading** (IDENTITY.md, SOUL.md, TOOLS.md, MEMORY.md, etc.) should be reviewed with this paper in mind. How much of it actually helps task completion vs. diluting the agent's focus?

## Relationship to SkillReducer

Both papers converge on the same finding from different angles:
- This paper: giving agents *more* context (via AGENTS.md) often hurts.
- SkillReducer: over 60% of skill body content is non-actionable, and removing it *improves* quality by 2.8%.
- The shared lesson: **context is a budget, not a dump.**

## Caveats / Limits

- AGENT BENCH has only 138 instances across 12 repos — relatively small.
- The repos with developer-committed context files are self-selected (early adopters who care about agent tooling).
- The study uses single-sample evaluation (one completion per task) — variance is high for any individual task.
- Context files are still evolving rapidly; best practices may improve as the ecosystem matures.
- The paper doesn't study *optimal* context files — only existing ones. A well-crafted minimal context file might consistently help.

## Key Quotes

> "Context files tend to reduce task success rates compared to providing no repository context, while also increasing inference cost by over 20%."

> "Unnecessary requirements from context files make tasks harder, and human-written context files should describe only minimal requirements."

> "Both LLM-generated and developer-provided context files encourage broader exploration (e.g., more thorough testing and file traversal), and coding agents tend to respect their instructions."
