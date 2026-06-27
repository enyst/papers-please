# ReAct: Synergizing Reasoning and Acting in Language Models

**Paper:** [arXiv:2210.03629](https://arxiv.org/abs/2210.03629)
**Authors:** Shunyu Yao, Jeffrey Zhao, Dian Yu, Nan Du, Izhak Shafran, Karthik Narasimhan, Yuan Cao
**Affiliations:** Princeton University, Google Research (Brain team)
**Date:** October 2022 (ICLR 2023)
**Project:** [react-lm.github.io](https://react-lm.github.io/)

## One-Line Summary

Interleave reasoning traces and environment actions in a single LLM generation loop, so thinking guides doing and doing grounds thinking.

## Core Idea

Before ReAct, LLM reasoning (chain-of-thought) and LLM acting (tool use, environment interaction) were studied separately. Chain-of-thought generates reasoning traces but is a "static black box" — it hallucinates because it never checks the real world. Act-only agents interact with environments but lack the ability to plan, track progress, or handle exceptions.

ReAct fuses both into one prompt format: the model alternates between **Thought** (free-form reasoning in natural language) and **Action** (a command to an external environment), receiving **Observation** (environment feedback) after each action.

```
Thought: I need to search for X to find Y.
Action: Search[X]
Observation: X is a ... founded in 1844 ...
Thought: The passage says 1844. Now I need to find Z.
Action: Search[Z]
Observation: Z was established in 1989 ...
Thought: 1844 < 1989, so the answer is X.
Action: Finish[X]
```

The key insight is **bidirectional synergy**:
- **Reason to act:** Reasoning traces help the model induce, track, and update action plans, and handle exceptions ("X wasn't found, let me try searching for Y instead").
- **Act to reason:** Actions let the model gather real information from external sources (Wikipedia, environments), grounding its reasoning in facts instead of hallucinated knowledge.

## Method

ReAct is prompt-based — no training required. The authors craft few-shot examples (1–6) that demonstrate the interleaved Thought/Action/Observation format for a given task, then prompt the LLM (PaLM-540B) to generate trajectories in the same format.

### Domains tested

| Domain | Task | Action Space | What reasoning adds |
|--------|------|--------------|---------------------|
| HotpotQA | Multi-hop QA | Wikipedia Search/Lookup | Decomposes questions, tracks sub-answers, avoids hallucination |
| Fever | Fact verification | Wikipedia Search/Lookup | Extracts evidence, reasons about support/refute |
| ALFWorld | Text-based household tasks | Game actions (go to, pick up, put) | Plans search strategy, tracks which locations checked |
| WebShop | Web shopping | Click, search, select | Evaluates product attributes against requirements |

### Thought types observed (HotpotQA)

The paper categorizes the kinds of reasoning that emerge in the Thought steps:
- **Decomposition:** "I need to search X, find Y, then find Z"
- **Information extraction:** "The paragraph says X was started in 1844"
- **Commonsense/arithmetic:** "X is not Y, so Z must be..." or "1844 < 1989"
- **Search reformulation:** "Maybe I can search for X instead"
- **Answer synthesis:** "Based on all this, the answer is X"

### Combining internal and external knowledge

ReAct alone is strong but not always best. The paper proposes hybrid strategies:
- **ReAct → CoT-SC:** If ReAct fails to find an answer within N steps, fall back to chain-of-thought with self-consistency (majority voting over multiple samples).
- **CoT-SC → ReAct:** If chain-of-thought's majority answer has low confidence (appears less than n/2 times), fall back to ReAct for grounded search.

These combinations consistently outperform either method alone.

## Results

### Knowledge-intensive tasks (PaLM-540B)

| Method | HotpotQA (EM) | Fever (Acc) |
|--------|---------------|-------------|
| Standard | 28.7 | 57.1 |
| CoT | 29.4 | 56.3 |
| CoT-SC (21 samples) | 33.4 | 60.4 |
| Act-only | 25.7 | 58.9 |
| **ReAct** | **27.4** | **60.9** |
| CoT-SC → ReAct | 34.2 | 64.6 |
| ReAct → CoT-SC | **35.1** | 62.0 |
| Supervised SoTA | 67.5 | 89.5 |

ReAct consistently beats Act-only. The hybrid ReAct + CoT-SC combinations beat everything.

### Decision-making tasks (PaLM-540B, 1–2 shot)

| Method | ALFWorld (success %) | WebShop (success %) |
|--------|---------------------|---------------------|
| Imitation learning (10³–10⁵ examples) | ~40% | ~29% |
| Reinforcement learning | ~30% | ~29% |
| Act-only (1–2 shot) | 45% | 30.1% |
| **ReAct (1–2 shot)** | **71%** | **40%** |

ReAct with just 1–2 examples dramatically outperforms models trained on thousands of examples. The reasoning traces are essential — they help the agent plan its search, recover from dead ends, and track state.

### Error analysis

On HotpotQA, the authors manually inspect 50 ReAct failure cases:
- **Successful traces:** 94% have correct reasoning, 86% have correct actions. Most failures come from incomplete Wikipedia coverage or early stopping.
- **Hallucination comparison:** Only 6% of ReAct traces have hallucination issues, vs. 14% for CoT (chain-of-thought without grounding).
- **Common failure mode:** Search returns too much irrelevant information, overwhelming the model's context.

## Arguments and Key Claims

1. **Reasoning and acting are complementary, not competing.** Neither alone is sufficient. Reasoning without acting hallucinates; acting without reasoning is brittle and fails to plan.

2. **Interleaving is the mechanism.** The specific contribution is not reasoning or acting themselves, but the *interleaved* format that creates a feedback loop between the two.

3. **Few-shot prompting suffices.** No fine-tuning needed. 1–6 examples are enough to teach the format. This makes ReAct immediately applicable to any LLM.

4. **Interpretability as a first-class benefit.** The reasoning traces are human-readable. You can inspect exactly why the model took each action. This is not just nice to have — it enables diagnosis, trust, and human-in-the-loop correction.

5. **Grounding reduces hallucination.** The ability to check facts against real sources (Wikipedia) measurably reduces hallucination compared to pure reasoning approaches.

## Why This Matters for OpenHands / SmolPaws

ReAct is the foundational paradigm that OpenHands builds on. The CodeActAgent's loop of Thought → Action → Observation is a direct descendant of ReAct, with code replacing the constrained action space.

Key lineage:
- ReAct established that interleaved reasoning + acting works and that few-shot prompting is sufficient.
- CodeAct (Wang et al., 2024) took the "Action" part and replaced it with executable Python code, dramatically expanding what an agent can do.
- OpenHands operationalized this into a full platform with persistent environments, file editing, browser automation, and multi-turn conversations.

The Thought step in ReAct became the `think` tool in OpenHands. The Action step became terminal commands, file edits, and browser actions. The Observation step is the environment's response. The loop is the same.

## Caveats / Limits

- Results are on PaLM-540B, which was not publicly available. Smaller models struggle more with the interleaved format.
- The action spaces tested are relatively constrained (3 Wikipedia actions, game commands). The paper doesn't address open-ended code execution.
- HotpotQA and Fever improvements over CoT are modest; the big wins are in decision-making tasks (ALFWorld, WebShop).
- The few-shot examples require careful human curation — different tasks need different example trajectories.

## Key Quotes

> "Reasoning traces help the model induce, track, and update action plans as well as handle exceptions, while actions allow it to interface with external sources to gather additional information."

> "ReAct overcomes issues of hallucination and error propagation prevalent in chain-of-thought reasoning by interacting with a simple Wikipedia API."

> "On two interactive decision making benchmarks, ReAct outperforms imitation and reinforcement learning methods by an absolute success rate of 34% and 10% respectively, while being prompted with only one or two in-context examples."
