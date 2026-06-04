# TextGrad: Automatic "Differentiation" via Text

**Paper:** [arXiv:2406.07496](https://arxiv.org/abs/2406.07496)
**Authors:** Mert Yuksekgonul, Federico Bianchi, Joseph Boen, Sheng Liu, Zhi Huang, Carlos Guestrin, James Zou
**Date:** June 2024
**Code:** [https://github.com/zou-group/textgrad](https://github.com/zou-group/textgrad)

## One-Line Summary

Turn arbitrary text artifacts into optimization variables: have LLMs produce natural-language "gradients" and update prompts, code, solutions, molecules, or planning parameters through textual gradient descent.

## Core Idea

TextGrad generalizes the backpropagation metaphor from neural networks to compound AI systems. A system is represented as a computation graph whose variables can be natural-language text, code, prompts, molecular strings, or other structured artifacts. During a backward pass, LLMs provide feedback describing how each variable should change to improve the downstream objective.

The key move is not literal differentiability. It is using LLM criticism as an interpretable direction of improvement:

| Neural optimization | TextGrad |
|---|---|
| Tensor variable | Text/code/prompt/SMILES/planning parameter |
| Loss function | Evaluation, verifier, objective prompt, simulator output |
| Gradient | Natural-language criticism |
| Optimizer step | LLM rewrite incorporating the criticism |
| Autograd graph | Compound AI computation graph |

## Method

### Pipeline

1. **Define variables:** Mark the artifacts to optimize, such as a prompt, code solution, answer, or molecule string.
2. **Run a forward pass:** Execute the system and compute an objective or evaluation.
3. **Backpropagate textual feedback:** Ask an LLM to explain how outputs and upstream variables should change.
4. **Apply Textual Gradient Descent (TGD):** Rewrite variables by incorporating their accumulated criticisms.
5. **Repeat:** Iterate until the objective improves or the budget is exhausted.

### Optimization Modes

- **Instance optimization:** Improve one artifact for one problem instance, such as a code solution or scientific answer.
- **Prompt optimization:** Improve a prompt so it generalizes across a batch of task instances.
- **Constrained optimization:** Express constraints in natural language and ask the optimizer to preserve them during updates.
- **Batch optimization:** Aggregate feedback across multiple examples before a prompt update.

## Results

The paper demonstrates TextGrad across a deliberately broad range of domains:

- **Question answering / problem solving:** Improves GPT-4o zero-shot accuracy on GPQA from **51% to 55%** by refining solutions at test time.
- **Coding:** Reports about a **20% relative performance gain** on difficult LeetCode-Hard solution optimization.
- **Prompt optimization:** Pushes GPT-3.5 performance closer to GPT-4 on reasoning tasks; on Object Counting, it beats a DSPy baseline by about **7%**.
- **Molecule optimization:** Uses SMILES strings and Vina/QED objectives to generate druglike candidate molecules with improved binding and druglikeness.
- **Radiotherapy planning:** Optimizes treatment-planning hyperparameters to improve target dosing while reducing organ-at-risk exposure.

## Why This Matters for SmolPaws

TextGrad is useful as a vocabulary and engineering pattern for skill improvement:

1. **Skills can be variables.** A `SKILL.md` file is exactly the kind of text artifact TextGrad would treat as mutable state.
2. **Feedback should be attached to components.** A bad task outcome should be traced to a specific instruction, script, example, or omission in the skill.
3. **Natural-language gradients are inspectable.** Unlike numeric gradients, a reviewer can read the proposed reason for an edit.
4. **Batching matters.** Skill updates should aggregate multiple failures rather than overreact to one trajectory.

## Relationship to SkillOpt

SkillOpt inherits the TextGrad intuition but narrows and hardens it for agent skills. TextGrad says arbitrary text artifacts can be optimized by textual gradients; SkillOpt says a persistent skill document should be optimized with deep-learning-style controls: bounded edit budgets, held-out validation, rejected-edit buffers, and slow/meta updates.

TextGrad is the broad framework. SkillOpt is the skill-specific training recipe.

## Caveats / Limits

- Textual gradients depend on the optimizer model's ability to diagnose causality.
- Rewrites can drift, overfit, or silently violate constraints without strong validation.
- Instance optimization is powerful but can blur into solving one case rather than learning reusable procedure.
- The framework is general, so production use still requires task-specific evaluation design.

## Key Quotes

> "TextGrad backpropagates textual feedback provided by LLMs to improve individual components of a compound AI system."

> "TextGrad follows PyTorch's syntax and abstraction and is flexible and easy-to-use."
