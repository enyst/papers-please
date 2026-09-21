# Verification — Formally Verified Code Generation

Generating code that *provably* satisfies a specification, rather than code that passes a test
suite. Two benchmarks, at two granularities: function-level and repository-level.

## Notes in this folder

| Note | What | Granularity |
|---|---|---|
| [algoveri-verified-code-generation](algoveri-verified-code-generation.md) | Aligned benchmark for verified code generation on classical algorithms — Dafny, Verus, and Lean; correctness is machine-checked, not test-checked | function-level |
| [vero-can-ai-agents-build-formally-verified-software-repositories](vero-can-ai-agents-build-formally-verified-software-repositories.md) | First repository-level benchmark for verified code generation: a multi-module implementation **and** a machine-checked Lean 4 proof, across real codebases | repository-level |

## Threads

- **What is measured flips.** Test-pass rate rewards code that happens to satisfy the cases you
  thought of; proof-checking rewards code that satisfies the spec. The two can disagree, and the
  gap is where most "the agent's tests passed" claims live.
- **Granularity is the hard part.** Getting a single function proved is a different problem from
  proving a multi-module repository with real dependencies
  ([Vero](vero-can-ai-agents-build-formally-verified-software-repositories.md) is explicitly the
  first to try the latter, and reports how much of it agents still fail to complete).
- **This is the strong form of the verification thread.** `../agentic-engineering/` argues
  verification is the bottleneck for autonomy; these papers show what the deterministic,
  non-LLM end of the verification ladder looks like.

## Related in this repo

- `../agentic-engineering/` — "verification is the bottleneck"; the guardrail tier (architecture > static analysis > tests > LLM checks); and the **two-gap framework** ([reality-is-the-final-verifier-two-gap-framework](../agentic-engineering/reality-is-the-final-verifier-two-gap-framework.md)) — a sound proof closes the *evaluation* gap inside the loop, but the requirement and model gaps outside it are what these benchmarks cannot touch.
- `../prompt-enforcement/` — runtime enforcement of constraints, a lighter-weight cousin.
- `../misc/` — evaluation methodology, including [METR time-horizon](../misc/measuring-ai-ability-to-complete-long-software-tasks.md).
