# Recursive Language Models

**Paper:** [arXiv:2512.24601](https://arxiv.org/abs/2512.24601)
**Authors:** Alex L. Zhang, Tim Kraska, Omar Khattab
**Affiliations:** MIT CSAIL (the DSPy group)
**Date:** December 2025 (updated May 2026)
**Code:** [github.com/alexzhang13/rlm](https://github.com/alexzhang13/rlm)

## One-Line Summary

Let an LLM programmatically examine, decompose, and recursively call itself over snippets of a long prompt stored in an external REPL — processing inputs 100× beyond the context window.

## Core Idea

Even frontier models with long context windows suffer from **context rot**: quality degrades as prompts get longer, and it degrades *faster* on harder tasks. A 272K-token model doesn't actually work well at 272K tokens — especially when the task requires reasoning over most of the input (not just finding a needle).

RLMs solve this by treating the long prompt as **external data in a Python REPL**, not as context window content. The model writes code to slice, probe, and process the prompt programmatically, and can recursively call itself on shorter sub-prompts.

The key mechanism: instead of stuffing everything into the context window, the model:
1. Stores the prompt as a variable in a Python REPL
2. Writes code to examine/decompose it (e.g., `prompt[:5000]`, `for chunk in chunks(prompt, 1000)`)
3. Can invoke `sub_rlm(sub_prompt)` — a recursive call to itself on a smaller piece
4. Stitches results together in the REPL
5. Returns the final answer from a REPL variable

```python
# RLM trajectory example (simplified):
# prompt is already in the REPL as variable `P`

# Probe the structure
lines = P.split('\n')
print(f"Total lines: {len(lines)}")
print(lines[:10])  # peek at the start

# Decompose and recursively process
results = []
for chunk in chunks(P, 2000):
    answer = sub_rlm(f"Classify each line in this text: {chunk}")
    results.append(answer)

# Aggregate
final = aggregate(results)
state['Final'] = final
```

## Why This Is Different from CodeAct

The paper directly compares to CodeAct and explains three critical design differences:

| Design Choice | CodeAct | RLM |
|---------------|---------|-----|
| Where the prompt lives | In the LLM's context window | In a REPL variable (external) |
| How the model sees the prompt | Reads it directly from context | Programmatically slices/probes it |
| Sub-LLM calls | Available as a tool, but invoked verbally | Invoked programmatically inside code loops |

**Flaw #1 in CodeAct (per the paper):** The prompt sits in the context window. This inherits all the window's limitations — context rot, length limits, attention degradation.

**Flaw #2:** CodeAct generates output directly, so outputs can't be longer than the context window.

**Flaw #3:** CodeAct can call sub-LLMs, but only by explicitly verbalizing each call. An RLM can write `for chunk in chunks: sub_rlm(chunk)` — launching O(|P|) or even O(|P|²) sub-calls programmatically. This is the "recursive" part that gives the approach its power.

## Method

### Algorithm

The RLM is defined as Algorithm 1 in the paper:

1. Initialize a Python REPL with the user prompt stored as a variable
2. Register `sub_rlm()` as a callable function in the REPL
3. Loop: LLM generates code → REPL executes it → stdout is truncated and fed back
4. Terminate when `state['Final']` is set (can be from REPL or from the LLM)

The recursion depth is a hyperparameter:
- **depth=0**: REPL access but no sub-LLM calls (already helpful for long inputs)
- **depth=1**: Can call `sub_rlm()` which gets a fresh context window for each call
- **depth=2+**: Sub-calls can themselves make sub-calls

### Tasks (scaling complexity)

The paper carefully designs evaluation around **how task complexity scales with input length**:

| Task | Complexity scaling | What it tests |
|------|-------------------|---------------|
| S-NIAH | O(1) — needle is constant | Basic retrieval in long context |
| BrowseComp-Plus | O(1) multi-hop — few gold docs | Multi-document reasoning |
| OOLONG | O(n) — must process every line | Semantic labeling + aggregation |
| OOLONG-Pairs | O(n²) — must process all pairs | Pairwise reasoning at scale |
| LongBench-v2 CodeQA | Fixed files | Code repository understanding |

The key finding: vanilla LLMs degrade fastest on high-complexity tasks (quadratic worst), while RLMs maintain performance because they can programmatically decompose the work.

### Baselines compared

- Vanilla LLM (GPT-5, Qwen3-Coder-480B)
- CodeAct + BM25 retriever
- CodeAct + sub-calls
- Compaction agent (iterative summarization)
- OpenCode / Claude Code (with and without context offloading)

## Results

### Headline numbers

On **OOLONG-Pairs** (the hardest, O(n²) task):
- GPT-5 base: **0.1%** F1
- RLM(GPT-5, depth=1): **58.0%** F1
- Claude Code: **0.1%** F1
- Claude Code + context offloading: **6.5%** F1

On **OOLONG** (O(n) task):
- GPT-5 base: **36.0**
- RLM(GPT-5, depth=1): **48.0** (+28.4%)
- Qwen3-Coder base: **44.1**
- RLM(Qwen3-Coder, depth=1): **48.0** (+33.3% over Qwen3 base on OOLONG-Pairs)

On **LongCoT-mini** (long reasoning, not just long context):
- GPT-5.2 base: **38.7%**
- RLM(GPT-5.2, depth=1): **50.6%** (+30.7%)
- RLM + decomposition hints: **65.6%** (+69.5%)

### Cost comparison

RLMs are **comparable or cheaper** than most baselines on average. The median RLM run is cheaper than the median base model run. But there are outlier trajectories where the RLM struggles and costs spike.

### RLM-Qwen3-8B (post-trained small model)

Fine-tuning Qwen3-8B on distilled RLM trajectories from Qwen3-Coder-480B:
- Outperforms base Qwen3-8B by **28.3%** median across benchmarks
- Approaches vanilla GPT-5 quality on three long-context tasks
- 3× faster inference due to better decision-making and fewer errors
- Exhibits **length generalization**: training on shorter contexts transfers to longer ones

## Key Observations from the Paper

1. **RLMs scale to 10M+ tokens** — processing inputs well beyond any model's context window by keeping the prompt external and processing it programmatically.

2. **The REPL is necessary, recursion is beneficial.** Even depth=0 (REPL without sub-calls) helps. Adding recursive sub-calls (depth=1) is critical for information-dense tasks where every line matters.

3. **Performance degrades with input length and task complexity for vanilla LLMs, but not for RLMs.** This is the central finding: RLMs decouple the model's effective capability from its context window size.

4. **Deeper recursion can hurt.** The reproduction paper ("Think, But Don't Overthink", arXiv:2603.02615) finds that depth=2 causes overthinking on simple tasks — exponentially inflating cost (3.6s → 344.5s) while degrading accuracy. Depth=1 is the sweet spot for most tasks.

5. **First decomposition matters.** How the model chooses to decompose the task on its first attempt strongly affects success. In-context examples that demonstrate decomposition strategies significantly improve performance.

6. **Training transfers across domains.** Fine-tuning on RLM trajectories from one domain improves RLM performance on unrelated tasks — the decomposition and sub-calling patterns are general.

## Arguments and Key Claims

1. **Context windows are a misleading metric.** A model advertised at 272K tokens doesn't work at 272K tokens for real tasks. The effective context window depends on task complexity — and for hard tasks, it's much shorter than the nominal limit.

2. **Inference-time compute for context, not just reasoning.** Just as reasoning models (o1, etc.) spend more compute to think harder, RLMs spend more compute to process longer contexts. This is a natural extension of inference-time scaling.

3. **The REPL changes what "context" means.** When the prompt is a variable in a REPL, the model treats it as data to be processed, not text to be read. This is a fundamental shift — from passive reading to active computation over the input.

4. **Recursive self-invocation is the key primitive.** The ability to programmatically call yourself on sub-problems — inside loops, with dynamically constructed prompts — is what separates RLMs from CodeAct agents with sub-call tools. It's the difference between "ask a colleague for help" and "write a MapReduce job."

5. **Small models can learn RLM behavior.** RLM-Qwen3-8B shows that the decomposition patterns are learnable and transferable, not just emergent in frontier models. This democratizes the approach.

## Concrete Examples

### OOLONG task decomposition
The model processes a corpus of questions that each need semantic labeling. Instead of reading all questions at once (which causes context rot), the RLM:
1. Probes the input to understand its structure
2. Splits into chunks
3. For each chunk, calls `sub_rlm("Classify each question: {chunk}")`
4. Aggregates classifications in the REPL

### OOLONG-Pairs (quadratic complexity)
Must reason about *pairs* of entries. The RLM writes nested loops:
```python
for i, entry_a in enumerate(entries):
    for j, entry_b in enumerate(entries):
        if i < j:
            result = sub_rlm(f"Compare {entry_a} with {entry_b}...")
            pairs.append(result)
```
This is impossible in a single context window but natural in a REPL with recursive calls.

### Self-debugging
Like CodeAct, RLMs benefit from error feedback — syntax errors in REPL code get fed back, and the model fixes them. The paper notes that incorrect trajectories have significantly more syntax errors (Figure 4b), suggesting that cleaner code execution correlates with task success.

## Why This Matters for OpenHands / SmolPaws

RLMs represent the next evolution in the ReAct → CodeAct lineage:

| Generation | Key innovation | Limitation addressed |
|------------|---------------|---------------------|
| **ReAct** (2022) | Interleave reasoning + acting | Hallucination from pure reasoning |
| **CodeAct** (2024) | Code as universal action space | Constrained tool definitions |
| **RLM** (2025) | Recursive self-invocation + prompt as external data | Context window limits |

For SmolPaws and OpenHands, the implications are:
- **Long conversations and large codebases** could be handled better by offloading context to the environment rather than cramming it into the context window.
- **Recursive sub-agent calls** are a natural extension of the current architecture — the model could spawn sub-tasks on slices of a problem.
- **The REPL-first philosophy** is already how OpenHands works (persistent shell, file system). RLMs formalize why this is better than pure prompt-based approaches.
- **Context compaction** (which OpenHands uses via condensers) is shown to be inferior to RLM-style programmatic decomposition for complex tasks.

The paper also directly benchmarks against **Claude Code** and **OpenCode** — showing that RLMs outperform them, particularly when context offloading is not used. This suggests that even sophisticated coding agents benefit from the explicit "prompt as external variable" design.

## Relationship to ReAct and CodeAct

RLMs build directly on CodeAct (which builds on ReAct):
- They use the same Thought/Code/Observation loop
- They add the REPL as the primary home for the prompt (not the context window)
- They add `sub_rlm()` as a first-class recursive primitive
- The paper explicitly credits CodeAct and compares against it as a baseline

The authors (Khattab, Kraska) are from the DSPy group at MIT, which has a different lineage than the OpenHands group (Wang, Peng, Ji at UIUC). But the ideas compose naturally.

## Caveats / Limits

- **Overthinking risk:** Deeper recursion (depth≥2) can hurt on simple tasks. The model wastes compute decomposing problems that don't need decomposition.
- **Latency:** RLM trajectories can take much longer than direct inference. The reproduction paper reports 3.6s → 344.5s for depth=2 on some tasks.
- **Outlier costs:** While median cost is comparable, worst-case costs spike when the model struggles with decomposition.
- **Evaluation is narrow:** Five benchmarks, two models. The paper doesn't test on real-world agent tasks (code editing, web browsing, etc.).
- **GPT-5 dependency:** Many results use GPT-5, which isn't publicly available for reproduction. The Qwen3 results are more reproducible.
- **The "recursive" framing overstates depth=1.** Most gains come from depth=1 (one level of sub-calls), which is just "call yourself on sub-problems" — not deeply recursive. True deep recursion (depth≥2) is often counterproductive.

## Key Quotes

> "We find that RLMs can successfully process inputs up to two orders of magnitude beyond model context windows."

> "On OOLONG-Pairs, both GPT-5 and Qwen3-Coder make little progress with F1 scores of ≤0.1%, while the RLM(depth=1) using these models achieve F1 scores of 58.0% and 23.1% respectively."

> "The effective context window of an LLM cannot be understood independently of the specific task."

> "Unlike [CodeAct], RLMs do not load the context directly into the model."

> "Deeper recursion causes models to overthink." — from the reproduction paper (arXiv:2603.02615)
