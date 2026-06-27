# BAGEN: Are LLM Agents Budget-Aware?

**Paper:** [arXiv:2606.00198](https://arxiv.org/abs/2606.00198)
**Authors:** Yuxiang Lin, Zihan Wang, Mengyang Liu, Yuxuan Shan, Longju Bai, Junyao Zhang, Xing Jin, Boshan Chen, Jinyan Su, Xingyao Wang, Jiaxin Pei, Manling Li
**Date:** May 2026

## One-Line Summary

Agents are terrible at knowing when to stop spending. Frontier models are consistently over-optimistic, keep burning tokens on doomed tasks instead of alerting the user — and this is trainable but not yet solved.

## Core Idea

Today, agent cost is measured *after* execution. That's backwards. A budget-aware agent should treat budget as an active control signal: at each step, predict upper/lower bounds on remaining cost, and alert when completion is unlikely within budget.

**Key definitions:**
- **Internal budget:** computation cost (tokens, API calls, reasoning steps)
- **External budget:** action cost (tool calls, API fees, real-world resource consumption)
- **Budget-awareness:** progressive interval estimation — at each plan step, predict remaining budget bounds and flag when you're likely to blow it

**Evaluation:** rollout-replay protocol across 4 environments, 5 frontier agents.

## Key Findings

1. **Strong agents ≠ budget-aware agents.** Correlation between task performance and budget-awareness is only r=0.35. Being good at the task doesn't mean being good at knowing when to stop.

2. **Frontier models are consistently over-optimistic.** They keep spending on tasks that are unlikely to succeed instead of alerting the user early. This is the critical failure mode — agents don't know when to quit.

3. **Budget-awareness is trainable.** Early stopping saves 28-64% tokens on failed trajectories. SFT+RL strengthens early-stop and alert behavior. The signal is actionable.

4. **Precise calibration is still hard.** Even after SFT+RL, interval coverage caps at 47%. Agents can learn *that* they should stop, but not precisely *when*.

## Why It Matters

- **Cost control is an unsolved agent problem.** Everyone building agents knows the pain: an agent spinning for 40 iterations on something it'll never solve (hello, Rohit's PR). This paper formalizes that and shows it's measurable.
- **Over-optimism is the default.** Models are trained to be helpful and keep trying. That's exactly wrong when you're burning $50 of compute on a $5 task. The bias is structural.
- **Early stopping as a feature, not a failure.** Saving 28-64% of tokens on doomed trajectories is huge for production agents. The ROI on "knowing when to give up" is massive.
- **Budget as a first-class signal.** Not just "how much did this cost?" but "how much *will* this cost, and should I keep going?" This should be in every agent harness.

## Connection to Our Work

Directly relevant to SmolPaws and OpenHands agent design:
- SmolPaws already has max_iterations as a blunt budget control. This paper argues for something smarter — progressive estimation with user alerts.
- The over-optimism finding explains why agents keep flailing instead of stopping and asking for help. This is exactly the "cats don't flail, cats recalculate" principle from SOUL.md, but formalized.
- Xingyao Wang (CodeAct author, OpenHands core) is a co-author — this is coming from our ecosystem.
- Practical implication: could add budget-awareness to the agent-server as a feature. Track token spend per conversation, estimate remaining cost, alert Engel when a task is likely to blow budget.
