# Wiki — synthesized articles

Prose syntheses of the agent-**memory** thread, built on the raw notes in [`../notes/`](../notes/).
This is the *published-article* layer of Papers Please: full-prose topic articles as opposed to
the per-paper notes and the index-style [`atlas-*.md`](../notes/atlas-agent-memory.md) pages.

Follows the [LLM Wiki pattern](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)
(source saved at [`../sources/karpathy-llm-wiki.md`](../sources/karpathy-llm-wiki.md); how-to at
[`../sources/METHODOLOGY.md`](../sources/METHODOLOGY.md)): knowledge synthesized across sources
into topic articles, not listed paper-by-paper. Cross-references are pre-built; the synthesis
compounds as new research is added.

---

## Articles

Written (prose syntheses):

- [What Is Agent Memory?](what-is-agent-memory.md) — Why agents need memory, what kinds exist, and how the field is structured.
- [Memory Consolidation & Lifecycle](memory-consolidation.md) — How agents compress, prune, and maintain memory over time.
- [Memory Security](memory-security.md) — Poisoning attacks, injection vectors, and defenses for persistent memory.

For every other memory topic, read the raw notes and the cross-cutting atlas page:

- [`../notes/memory/`](../notes/memory/) — the per-paper notes (source of truth).
- [`../notes/atlas-agent-memory.md`](../notes/atlas-agent-memory.md) — the index-style cross-store synthesis of this whole thread.

---

## Source Corpus

This wiki synthesizes 63 papers from arXiv (2023–2026), focusing on deployed/inference-time memory in AI agents. The full source index is in [Sources](sources.md).

**Scope:** ICL-style and prompt-time memory — retrieved experiences, workflows, summaries, skills. Also: episodic, semantic, hierarchical, and personalization memory. Benchmarks, surveys, and security papers included where they inform the synthesis.

**What's excluded:** Papers centered on pretraining, fine-tuning, or memory architectures without a deployed-agent angle.

---

*Maintained by [Liberty Labs](https://liberty-labs.org). Prose articles seeded 2026-06-07; folded into Papers Please 2026-09-13.*
