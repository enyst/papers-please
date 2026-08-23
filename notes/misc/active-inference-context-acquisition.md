---
title: "Active Inference as Context Acquisition for AI Agents"
authors:
  - Sanchayan Dutta
  - Sai Niranjan Ramachandran
  - Suvrit Sra
venue: arXiv
date: 2026-06-08
arxiv: "2608.19202"
url: https://arxiv.org/abs/2608.19202
tags: [agents, context-acquisition, active-inference, clarifying-questions, information-gain, prompt-optimization, decision-theory]
source: "flagged by Engel via @omarsar0 — https://x.com/omarsar0/status/2091199978014458081"
---

# Active Inference as Context Acquisition for AI Agents

**Paper:** [arXiv:2608.19202](https://arxiv.org/abs/2608.19202)
**Authors:** Sanchayan Dutta, Sai Niranjan Ramachandran, Suvrit Sra
**Date:** June 2026

## One-Line Summary

Treats an agent's decision to *ask vs. assume vs. retrieve vs. act* as **active inference over a latent task state**: keep a belief about what the user actually wants, and at each step pick the action that most reduces uncertainty per token spent (minimize expected free energy under cost). Instantiated as **Optimal Question Asking (OQA)** with exact posteriors and a dynamic-programming oracle, so you can measure how far a frontier model is from optimal context-gathering.

## The problem it names

Context acquisition is usually an afterthought. When a user omits a constraint, preference, file, or task variable, the agent must either:

- proceed on a **default assumption** (risking a wrong guess → hallucination, wasted work), or
- **spend tokens** on a clarifying question, a retrieval call, a tool call, or a prompt trial.

The paper argues many current agent failures (bad assumptions, cost blowups, unreliable tool calls) are really *this* tradeoff handled badly, and gives it an objective function instead of leaving it to vibes.

## The formulation

- **Inner step (inference):** update beliefs over a latent task state as new context arrives.
- **Outer step (decision):** choose the next action — a *context* action (ask / retrieve / probe), a *task* action, or *stop* — to minimize **expected free energy under cost**.
- **Deterministic case:** the epistemic term collapses to **expected information gain**, optionally **normalized by token cost**. That is a concrete, implementable scoring rule today — score each candidate question/tool-call by expected bits-per-token and pick the best.
- **Model-agnostic:** framed as a *design principle for the context-acquisition layer*, not a new model.

## OQA benchmark

- Exact posteriors + a **dynamic-programming oracle** for the optimal question sequence.
- Frontier LLMs benchmarked on binary and multiway categorical tasks, candidate sets from **25 to 300**.
- Also studies **clarification-before-generation** and **automated prompt optimization under token budgets**.
- The oracle gives a measurable *gap* between an agent's questioning strategy and the true optimum.

## Why it's in here (relevance to our work)

- **Memory / context management:** directly about *what to pull into context and when* — the same economy the dreaming/consolidation and retrieval work cares about, but on the acquisition side. "Ask a clarifying question" vs "retrieve" vs "assume" is a retrieval-policy decision with a cost model.
- **Clarifying-question policy:** an implementable scoring rule (expected info gain / token cost) for when an agent should stop and ask the user instead of guessing — relevant to how SmolPaws decides to ask Engel vs. proceed.
- **Concept-formation angle:** belief updating over a latent task state is a clean, decision-theoretic take on "figuring out what the human means," adjacent to Engel's concept-formation interest.

## Open questions / caveats

- Exact posteriors + DP oracle are tractable on small categorical candidate sets (25–300); real tasks have unbounded latent state, so the oracle is a *yardstick*, not a drop-in planner.
- Expected-information-gain scoring needs a usable belief/likelihood model over candidate task states — the hard part in practice is estimating those beliefs, not the argmax.
