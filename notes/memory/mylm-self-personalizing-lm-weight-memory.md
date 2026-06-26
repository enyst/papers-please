---
title: "mylm: Self-Personalizing LM (weight-based memory via sleep-time LoRA)"
authors:
  - Awni Hannun
source: "GitHub (experimental repo)"
url: "https://github.com/awni/mylm"
created: "2026-03-05"
project: "memory"
scope_note: "context include — practitioner experiment, useful contrast"
agent_setting: "local personal chat assistant on MLX (Apple silicon)"
memory_mechanism: "Stores user facts in model weights: a 'sleep' step generates Q&A pairs from chat history and LoRA-fine-tunes the model on the accumulated pile."
icl_relevance: "high"
tags:
  - agent-memory
  - weight-memory
  - sleep-time-compute
  - lora
  - catastrophic-forgetting
  - eviction
categories:
  - consolidation
  - personalization
---

# mylm — memory in the weights, and the eviction wall

**What it is.** A small experimental repo by Awni Hannun (co-creator of MLX at
Apple; the project predates / coincides with his move away from Apple). "A
self-personalizing LM." ~76★ as of mid-2026, code-only (no README), built on
`mlx-lm`.

**Mechanism (`mylm/sleep.py`).** Memory lives in **adapter weights**, not in a
store or context:

1. **Chat** with a local MLX model (`chat.py`), system prompt (`SYSTEM.md`) tells
   the AI to get to know the user — name, where they live, preferences, even to
   adopt a user-chosen personality. Same "AI friend that knows you" framing as
   personal-agent products.
2. **Sleep** (`sleep.py`): prompt the model to generate **Q&A pairs** about the
   user's messages from the conversation history → append to a growing
   `memory/qa.jsonl` → **LoRA-fine-tune** (rank 16, 16 layers) on the *entire*
   accumulated set → save `adapters.safetensors`.
3. Next session loads the adapter; the model "remembers" the user because it was
   trained on them. No retrieval, no context budget, no database.

## Why it matters: it isolates the eviction problem

This is the cleanest practitioner illustration that **forgetting/eviction is the
hard part** of agent memory, and it comes from a credible ML engineer:

- Every sleep cycle **appends and retrains on the whole pile**. Knowledge is
  smeared across adapter weights.
- When a fact **changes** (user moves Stockholm → Sveg), there is **no clean way
  to delete** the old value. It coexists in the weights with the new one;
  retraining on the ever-growing Q&A set keeps baking the stale fact back in.
- Selective deletion in weight-space is ~intractable without retraining from
  scratch — i.e. the thing you actually want (timely forgetting) is exactly what
  weights-as-memory makes hardest.

## Contrast with external/context memory (e.g. dreamem, A-MEM, Letta)

| Axis | mylm (weights) | external store (dreamem / A-MEM / Letta) |
|---|---|---|
| Memory locus | LoRA adapter weights | text + metadata in a store |
| Consolidation | retrain on accumulated Q&A | promote / prune / restructure / index |
| Eviction | ~impossible (baked in) | first-class (flag/delete) |
| Contradiction update | new pairs fight old weights | evict old, keep new |
| Auditable / measurable | hard | recall@budget benchmarks, provenance |

**Takeaway for our work.** Validates the Liberty Labs / dreamem thesis: keep
memory **external and editable** so eviction is an operation, not a training
problem. mylm is the strongest "the other path hits the forgetting wall" data
point we have — good to cite in the dreamem write-up and the memory wiki.

**Related local notes:** `auto-dreamer-learning-offline-memory-consolidation-for-language-agents.md`
(consolidation framing), A-MEM (structured editable notes). Sleep-time compute
lineage connects to Letta's Context Constitution.
