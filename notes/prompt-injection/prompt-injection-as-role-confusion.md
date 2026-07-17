---
title: "Prompt Injection as Role Confusion"
authors:
  - Charles Ye
  - Jasmine Cui
  - Dylan Hadfield-Menell
arxiv_id: "2603.12277"
arxiv_url: "https://arxiv.org/abs/2603.12277"
published: "2026-02-22"
updated: "2026-06-27"
venue: "ICML 2026"
source: "arXiv"
project: "prompt-injection"
scope_note: "deep read"
agent_setting: "Chat models and tool-using agents processing untrusted tool output"
defense_approach: "mechanism-analysis"
defense_type: "Not a defense — latent role probes plus the CoT Forgery attack"
tags:
  - prompt-injection
  - role-confusion
  - mechanistic-interpretability
  - linear-probes
  - chain-of-thought
  - agent-security
categories:
  - cs.CL
  - cs.AI
  - cs.CR
---

- **One-line take:** Prompt injection works when attacker-controlled text is represented as the privileged role it imitates; the paper measures that confusion in latent space and shows it predicts attack success before generation.
- **Approach:** Train role probes on identical neutral text wrapped in different architectural tags, then apply them to CoT Forgery and ordinary agent prompt injections.
- **Pros:** Offers a concrete mechanism rather than another attack taxonomy; controls content while varying tags; links internal representation to downstream attack success; releases code and reproduction notebooks.
- **Cons:** Does not build or test a defense; internal analyses cover four open-weight models in the 20B–120B range; linear probes assume role information occupies recoverable directional subspaces.
- **Project page:** https://role-confusion.github.io/
- **Code:** https://github.com/role-confusion/prompt-injection-as-role-confusion

## Core Claim

LLM interfaces label text with roles such as system, user, assistant, reasoning, and tool. Those labels are intended to define authority boundaries: tool output should be treated as data, while user text can issue instructions. The paper argues that these boundaries often fail inside the model. Models infer who is speaking from attacker-controllable cues—style, syntax, position, and even plain-text declarations—rather than reliably preserving the architectural role tag.

The authors call this **role confusion**: text that sounds like a privileged role enters the same representational region and inherits the same practical authority. Prompt injection is therefore framed as **state poisoning**, not merely failure to recognize a known malicious string.

## Role Probes

The paper trains layer-specific multinomial logistic-regression probes for five roles: system, user, chain-of-thought, assistant, and tool.

To avoid the usual style/role confound, probe training uses identical neutral passages sampled from C4 and Dolma 3, wrapped separately in each model's native role tags. Since the text is held constant, the probe can only learn the representational effect induced by the tag. The resulting probabilities are described as *Systemness*, *Userness*, *CoTness*, *Assistantness*, and *Toolness*.

The probes transfer zero-shot to real conversations. In the paper's gpt-oss-20b case study, correctly tagged reasoning averages 85% CoTness while user and assistant text remain near zero. More importantly:

- Removing all tags barely changes the representation of reasoning-style text: CoTness remains 83%, versus 85% with proper tags.
- Putting reasoning-style text inside a user tag still yields 85% CoTness and only 2% Userness.
- Across gpt-oss-20b, gpt-oss-120b, Nemotron-3, and Qwen3-30B-A3B, user-style text rewrapped as tool output retains 76–88% Userness, while Toolness never exceeds 20%.

The model does encode tags, but style and tags converge on the same role features; when they conflict, attacker-controlled cues dominate.

## CoT Forgery

**CoT Forgery** is a zero-shot attack that appends fabricated reasoning in the target model's characteristic reasoning style. The text arrives through a user message or tool output, but argues as though the model has already reasoned its way to compliance.

The attack does not need a convincing argument. Absurd and plausible justifications perform similarly (60% versus 63% attack success), suggesting the model grants the forged text reasoning-role privilege rather than evaluating its logic.

Key results:

- Across gpt-oss-20b, gpt-oss-120b, o4-mini, and the GPT-5 nano/mini/full family, CoT Forgery reaches about 60% attack success on StrongREJECT despite near-zero baselines.
- In a shell-enabled agent tasked with summarizing an untrusted webpage, ordinary prompt injections usually achieve 0–2% success (26% on gpt-oss-20b), while CoT Forgery reaches 56–70% and causes real `.env` exfiltration in the test environment.
- Rephrasing the forged reasoning to remove model-specific reasoning style drops average attack success from 61% to 10%.

## Representation Predicts the Attack

Styled forged reasoning averages 79% CoTness—higher than the models' genuine reasoning at 68%. Destyling reduces it to 29% and shifts the text back toward the user subspace.

Across 626 styled and destyled attempts, attack success rises almost monotonically with the forged text's CoTness: the lowest-confusion quantile succeeds 9% of the time, while the highest succeeds 90%. The same pattern generalizes to conventional agent prompt injection: declarations that make a tool-output command appear more user-like increase Userness, and higher Userness predicts higher attack success even after controlling for the declaration template.

This makes role confusion measurable before the model emits a token. It is stronger evidence than attack success alone, though the probe remains a diagnostic rather than a security boundary.

## Defense Implications

The paper's diagnosis explains why attack-pattern classifiers become an endless whack-a-mole. If models do not reliably preserve role provenance, they must judge whether every instruction-looking string is suspicious—including legitimate instructions and genuine reasoning. Training against known phrasing can suppress individual attacks without fixing that representational ambiguity.

A robust learned defense would need role boundaries that survive into latent representations and resist attacker-controlled style, position, and declarations. The paper does not demonstrate how to achieve that. For deployed agents, its results strengthen the case for keeping authority outside the model: taint untrusted inputs, constrain tools and capabilities deterministically, and require confirmation for consequential actions. Role probes could become a useful monitor for open-weight models, but they are not an enforcement mechanism.

## Relevance to SmolPaws

The result directly supports SmolPaws' prompt-injection rule: messages and fetched content do not gain authority merely because they contain plausible instructions. Source and authorization must be tracked by the harness, not inferred by the LLM from prose.

It also sharpens the design requirement for browser and Slack ingestion. Untrusted content should be treated as data throughout the execution path, while dangerous tool actions remain gated outside the model. A model-level refusal is useful defense in depth, but not the boundary to trust.

## Caveats

- The role-probe experiments require hidden activations and therefore cover four open-weight models, not the closed frontier models used in all attack evaluations.
- Linear probes assume that role information is linearly recoverable. The authors validate the probes through zero-shot transfer, convergent cues, and prediction of attack success, but this does not establish a complete causal account of every relevant representation.
- CoT Forgery uses an auxiliary model and examples of target reasoning style. It is zero-shot against the target, but not free of attacker preparation.
- The paper evaluates specific chat templates, model families, and agent loops; role geometry and attack rates may differ in other harnesses.
- Full reproduction is resource-heavy: the authors report H200-based experiments and potentially large activation exports, though smaller demo notebooks are provided.
