# Foundational Agent Papers

The small set of papers the rest of the wiki stands on: the **loop** an agent runs, the
**action space** it runs in, what it means for an induced rule to be *right*, and the scaling
question underneath all of it.

These are here because later notes keep presupposing them — ReAct's thought/action/observation
interleave, CodeAct's code-as-action, RLM's recursive self-call, and the hypothesis-selection
principle behind how we promote lessons out of experience.

## Notes in this folder

| Note | What | Why it's foundational |
|---|---|---|
| [react-synergizing-reasoning-and-acting-in-language-models](react-synergizing-reasoning-and-acting-in-language-models.md) | Interleave reasoning traces with environment actions in one generation loop | The Thought/Action/Observation shape every harness still uses; "reason to act, act to reason" |
| [codeact-executable-code-actions-elicit-better-llm-agents](codeact-executable-code-actions-elicit-better-llm-agents.md) | Replace JSON/text tool calls with executable Python as the universal action space | Composability, self-debugging, and access to existing software for free — the OpenHands/SmolPaws action model |
| [rlm-recursive-language-models](rlm-recursive-language-models.md) | Let the model programmatically examine, decompose, and recursively call itself over prompt snippets in an external REPL | Inputs 100× beyond the context window; the recursion pattern behind context-as-environment |
| [optimal-hypothesis-is-the-weakest-not-the-shortest](optimal-hypothesis-is-the-weakest-not-the-shortest.md) | To generalize, pick the *weakest* hypothesis consistent with the data, not the shortest (MDL) | The rule we use when promoting daily memory into durable learnings (dreaming) |
| [why-the-third-axis-is-freedom](why-the-third-axis-is-freedom.md) | "Generative expressivity" as a third scaling axis actually scales *freedom* — the weakness of the implied constraint | Sequel to the weakest-hypothesis note; the same weakness-maximisation principle at pretraining scale |

## Threads

- **The loop is the unit.** ReAct and CodeAct are both answers to "what does the model get to
  do between observations?" Every harness note downstream is a variation on that question.
- **Recursion buys context.** [RLM](rlm-recursive-language-models.md) is the cleanest statement
  that the window is not the limit — the program is. Compare
  [Context as an Environment (Scroll)](../memory/context-as-an-environment-scroll-programmatic-context-management.md)
  and [Trace as State](../memory/trace-as-state-reasoning-traces-as-conditional-states.md).
- **Induction has a correctness criterion.** The two hypothesis notes give us a principled way to
  choose a lesson from few examples, which matters more for memory/dreaming than for training.

## Related in this repo

- `../harness/` — what sits between these loops and the world.
- `../memory/` — Reflexion, Voyager, MemGPT: the loop plus durable state.
- `.agents/skills/weakest-hypothesis/` (smolpaws repo) — the operational form of the weakest-hypothesis rule.
