# Executable Code Actions Elicit Better LLM Agents (CodeAct)

**Paper:** [arXiv:2402.01030](https://arxiv.org/abs/2402.01030)
**Authors:** Xingyao Wang, Yangyi Chen, Lifan Yuan, Yizhe Zhang, Yunzhu Li, Hao Peng, Heng Ji
**Affiliations:** University of Illinois Urbana-Champaign, Microsoft
**Date:** February 2024 (ICML 2024)

## One-Line Summary

Replace JSON/text tool calls with executable Python code as the universal action space for LLM agents — get composability, self-debugging, and access to all existing software for free.

## Core Idea

ReAct showed that interleaving reasoning and acting works. But what should the **action format** be? Most agent frameworks use either:
- **Text actions** in pre-defined formats ("Search[query]", "Click[element]")
- **JSON actions** (function calling, tool use schemas)

Both suffer from the same fundamental limitations:
1. **Constrained action space** — you can only do what the pre-defined tools allow.
2. **No composability** — you can't combine multiple tools in a single action (e.g., search for X, then filter results by Y, then compute Z).
3. **No control flow** — no if/else, no loops, no variables that persist across actions.

CodeAct proposes: just use **executable Python code** as the action format. The agent writes Python, a sandboxed interpreter executes it, and the agent receives stdout/stderr as its observation.

```python
# Instead of: Action: Search["Apple Remote"]
# CodeAct does:
import wikipedia
result = wikipedia.search("Apple Remote")
page = wikipedia.page(result[0])
print(page.summary[:500])
```

This is a strictly more expressive action space. Everything JSON/text actions can do, code can do — plus composition, control flow, data manipulation, and access to the entire Python package ecosystem.

## Method

### Multi-turn interaction framework

CodeAct defines three roles:
- **Agent**: generates natural language (to user) or Python code (to environment)
- **User**: provides instructions and feedback in natural language
- **Environment**: executes code, returns results/errors

Each turn, the agent can optionally include chain-of-thought reasoning before emitting code. The environment returns execution output (including errors), enabling **self-debugging**: when code fails, the agent sees the traceback and can fix it in the next turn.

### Three research questions

The paper systematically tests:

**RQ1: Does LLMs' code pre-training make CodeAct naturally strong?**
Yes. On API-Bank (atomic tool calls), CodeAct matches or beats JSON/text across 17 LLMs — even for single, simple tool calls where composability isn't a factor. LLMs are already good at generating Python function calls because they've seen billions of lines of code during pre-training.

**RQ2: Does CodeAct benefit from Python's control/data flow on complex tasks?**
Yes, dramatically. On M3ToolEval (multi-tool, multi-step tasks), CodeAct's advantage grows as task complexity increases. Code can loop over results, branch on conditions, and pipe data between tools — things that JSON actions simply cannot express.

**RQ3: Does multi-turn interaction + software access compound the advantage?**
Yes. With a Python interpreter, the agent can install packages, train models, generate visualizations, and self-debug from error messages — all without special tool definitions.

### M3ToolEval benchmark

The authors create a new benchmark specifically designed to test complex, multi-tool scenarios:
- 82 human-curated instances
- Domains: web browsing, finance, travel planning, science, information processing
- Each domain has its own manually crafted tool set
- Zero-shot evaluation (no demonstrations) — tests whether the model can figure out tool use from the tools' docstrings alone

## Results

### Atomic tool calls (API-Bank)

CodeAct matches or beats JSON and text formats for most models. The advantage is especially strong for **open-source** models — they've seen more code than JSON tool-call formats during training.

For closed-source models (GPT-4, etc.), JSON is competitive because these models have been specifically fine-tuned for JSON function calling. But CodeAct still matches them.

### Complex multi-tool tasks (M3ToolEval)

| Model | CodeAct (success %) | JSON (success %) | Text (success %) |
|-------|--------------------|--------------------|-------------------|
| GPT-4 | 53.7 | 29.3 | 24.4 |
| GPT-3.5-turbo | 45.1 | 14.6 | 11.0 |
| Lemur-70b | 12.2 | 7.3 | 8.5 |
| Mistral-7B | 8.5 | 3.7 | 1.2 |

CodeAct's advantage is **massive** on complex tasks — up to 20% absolute improvement. The gap grows with task complexity because code can compose operations that would require multiple separate JSON actions.

### Efficiency (fewer turns)

CodeAct consistently requires **fewer interaction turns** to solve tasks. Where JSON/text agents need multiple rounds of single tool calls, CodeAct can chain operations in one code block.

| Model | CodeAct (avg turns) | JSON (avg turns) | Text (avg turns) |
|-------|--------------------|--------------------|-------------------|
| GPT-4 | 7.2 | 9.7 | 9.9 |
| GPT-3.5-turbo | 6.6 | 9.1 | 9.8 |

### CodeActAgent (fine-tuned)

The authors fine-tune Llama-2 and Mistral-7B on CodeActInstruct (7k multi-turn interaction examples using CodeAct). Key finding: fine-tuning on CodeAct data improves performance on **all** action formats, not just code — suggesting that learning to reason through code transfers to better tool use generally.

The fine-tuned model can:
- Train ML models using scikit-learn/PyTorch
- Generate data visualizations with matplotlib
- Self-debug from error tracebacks across multiple turns
- Use any installed Python package without explicit tool definitions

## Arguments and Key Claims

1. **Code is the natural action language for LLMs.** Models have seen orders of magnitude more Python than JSON tool-call formats during pre-training. Using code as the action format leverages existing capability rather than teaching a new format.

2. **Composability is not optional for real tasks.** Simple tasks can be solved with atomic tool calls. Real-world tasks require combining tools, branching on results, and iterating. Only code provides this naturally.

3. **Self-debugging is emergent.** When the interpreter returns an error traceback, the model naturally attempts to fix the code. This error-correction loop is free — it emerges from the multi-turn interaction format without any special training.

4. **The action space should be open, not pre-defined.** With code execution, the agent isn't limited to a curated tool set. It can `pip install` new packages, write utility functions, and create its own tools on the fly. The action space is as large as the Python ecosystem.

5. **Open-source models benefit most.** Closed-source models have been fine-tuned for JSON; open-source models have been trained on code. CodeAct plays to open-source strengths, democratizing capable agent behavior.

## Concrete Examples from the Paper

### Self-debugging (Figure 3)
The agent tries to load a CSV with `?` values. LinearRegression fails with "could not convert string to float: '?'". The agent sees the error, reasons about it ("The '?' character is present in the data"), and fixes it by adding `df.replace('?', np.nan).dropna()`. Three rounds of self-debugging, no human intervention.

### Multi-tool composition
User asks: "Find the sum of the reciprocals of the roots of x²-13x+4=0."
Agent writes one code block using `sympy.solve()` and arithmetic — a task that would require multiple JSON tool calls or wouldn't be expressible at all in constrained action spaces.

### Interactive data science session (Figure 3)
Agent downloads dataset → trains regression model → reports metrics → plots coefficients → adjusts visualization based on user feedback → reports training metrics — all in a natural multi-turn conversation where each action is executable code.

## Why This Matters for OpenHands / SmolPaws

CodeAct is the direct ancestor of OpenHands' CodeActAgent. The paper provides the theoretical and empirical justification for OpenHands' core design decision: **agents should act through code execution in a sandboxed environment.**

The lineage:
1. **ReAct** (2022): established Thought/Action/Observation loops
2. **CodeAct** (2024): replaced constrained actions with executable code
3. **OpenHands** (2024): built a full platform around CodeAct — persistent sandboxed environments, file system, browser, multi-tool integration

SmolPaws inherits this directly. Every terminal command, every file edit, every browser action is a CodeAct-style code action executed in a persistent environment. The self-debugging behavior the paper documents is what SmolPaws does when a command fails — read the error, reason about it, try again.

The paper's claim that "the action space should be open, not pre-defined" is exactly SmolPaws' philosophy: no tool registry, no JSON schemas — just code that runs.

## Relationship to ReAct

| Aspect | ReAct | CodeAct |
|--------|-------|---------|
| Action format | Constrained text (Search[], Lookup[]) | Executable Python code |
| Action space | Pre-defined, task-specific | Open (entire Python ecosystem) |
| Composability | One action per turn | Arbitrary composition in one turn |
| Error handling | Agent must reason about failures | Interpreter provides tracebacks |
| Self-debugging | Not addressed | Emergent from multi-turn + error feedback |
| Tool extensibility | Must define new action types | `pip install` and use |
| Reasoning | Explicit Thought steps | Optional chain-of-thought before code |

CodeAct preserves ReAct's core insight (interleave reasoning and acting) while removing its main limitation (constrained action space).

## Caveats / Limits

- **Security:** Granting agents arbitrary code execution is a safety risk. The paper acknowledges this: "in the worst scenario, such an agent may potentially break free of the sandbox restriction." OpenHands addresses this with containerized sandboxes.
- **Code quality:** The generated code doesn't need to be production-quality — it just needs to work. But errors in code logic are harder to catch than errors in structured tool calls.
- **Model capability floor:** Weak models generate bad code. The approach works best with capable models (GPT-4 class and above). Smaller models (7B) show smaller CodeAct advantages.
- **M3ToolEval is small:** 82 instances. The benchmark demonstrates the principle but isn't a comprehensive evaluation suite.

## Key Quotes

> "CodeAct can execute code actions and dynamically revise prior actions or emit new actions upon new observations through multi-turn interactions."

> "CodeAct outperforms widely used alternatives (up to 20% higher success rate)."

> "Using CodeAct to call tools is a more natural way to use tools for the models, which typically have extensive exposure to code data during their training."

> "Since CodeAct directly grants access for the agent to freely execute code in a sandbox environment, in the worst scenario, such an agent may potentially break free of the sandbox restriction and cause harm to the world, highlighting the need for future work to design better safety mechanisms."
