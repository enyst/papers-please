# Papers Please

Curated research paper notes. Each paper has structured frontmatter (title, authors, arXiv link, mechanism summary, one-line take) and a short analysis.

This is an **LLM-maintained knowledge wiki** (Karpathy's "LLM Wiki" pattern). If you are an
agent working here, read **[`AGENTS.md`](./AGENTS.md)** first — it's the schema: the note
format and the ingest / query / lint workflows. Maintenance history is in
**[`LOG.md`](./LOG.md)**.

## Topics

| Directory | Papers | What |
|-----------|--------|------|
| `notes/memory/` | 79 | Agent memory — architectures, consolidation, benchmarks, security, tools |
| `notes/world-models-agi/` | 31 | World models, understanding, consciousness, concept formation — RSTA 384(2320) theme issue + the foundational classics (Turing, Nagel, Searle, Harnad, Chalmers, Dennett, Block, Bender, Mitchell&Krakauer, Othello-GPT, Lake) |
| `notes/prompt-injection/` | 13 | Prompt injection attacks and defenses — approaches with pros/cons |
| `notes/prompt-enforcement/` | 8 | Deterministic enforcement of agent instructions (Prompt Shield research) |
| `notes/skills/` | 12 | Agent skill discovery, optimization, benchmarking, and context file evaluation |
| `notes/harness/` | 6 | Agent harnesses — *everything between the model weights and the world* (see `notes/harness/README.md`); code-as-harness, state-centric runtimes, and the self-improving-harness line (Darwin Gödel Machine, Meta-Harness, Continual Harness) |
| `notes/agentic-engineering/` | 9 | Engineering *with* coding agents — software factories, immutable-artifact receipts, self-improving SDLC loops (sources from everywhere: tweets, blogs, papers) |
| `notes/prompt/` | 2 | Prompting techniques and adversarial (synthetic languages, Waluigi Effect) |
| `notes/foundational/` | 5 | Foundational agent & AGI-theory papers — ReAct, CodeAct, RLM, weakest-hypothesis, freedom-third-axis |
| `notes/interpretability/` | 3 | Mechanistic interpretability — steering/ablation, safety-entanglement, and the philosophy of not over-reading it |
| `notes/verification/` | 2 | Formal verification of generated code — function-level and repository-level benchmarks (vericoding) |
| `notes/misc/` | 10 | Everything that doesn't fit a category yet (evaluation, capability measurement / task time-horizon, survey simulation, ensembling, context-acquisition/active-inference, multi-agent emergence) |
| `notes/long-context-and-prompting.md` | ~30 | Long-context evaluation, prompting techniques, reasoning |
| `notes/memory-and-rag.md` | ~10 | RAG and memory-retrieval hybrid approaches |
| `blogs/interesting-posts.md` | — | Curated blog posts and articles on AI/agents |

*(Counts drift as notes are added; refresh the row you touch — `ls notes/<topic>/*.md | wc -l`.)*

## The wider atlas — our knowledge lives in four stores

This wiki (external research) is one of four knowledge stores. They stay **federated, not
merged** — each has a different owner and change-rate. Link across them; don't copy
(Letta's "index, don't copy"). The map:

| Store | Location | What | Maintained by |
|-------|----------|------|---------------|
| **Research wiki** *(here)* | `papers-please/` | External papers, blogs, talks, digested for reuse | this repo (`AGENTS.md`) |
| **Identity + system** | `smolpaws/docs/` | SmolPaws identity/soul/ops + architecture (SPEC, agent-server, ingress) | smolpaws repo |
| **OpenHands** | [docs.openhands.dev](https://docs.openhands.dev/) + the SDK | The agent platform SmolPaws is built on | upstream (link, don't snapshot — it moves) |
| **Letta / memory philosophy** | `smolpaws/docs/context-constitution.md`, `letta-constitution-original.md` | Context-management principles; applied in SmolPaws' dreaming/heartbeat | smolpaws repo |
| **Private durable memory** | `~/.smolpaws/memory/` | SmolPaws' own facts/daily memory (not in git) | heartbeat/dreaming |

**Atlas pages** — cross-cutting threads mapped across the stores (links + synthesis, not
copies). Built as *query answers filed back* (see `AGENTS.md` → Query), only when a real
question earns one:
- [`notes/atlas-agent-memory.md`](./notes/atlas-agent-memory.md) — Letta principles ↔ `notes/memory/` ↔ SmolPaws dreaming ↔ concept-formation.
- [`notes/atlas-harness.md`](./notes/atlas-harness.md) — "everything between weights and world"; research corpus ↔ skills ↔ SmolPaws as a live harness.
- [`notes/atlas-grounding-understanding.md`](./notes/atlas-grounding-understanding.md) — does fluent output = understanding? Turing → Searle/Harnad/Bender → Othello-GPT/Lake → Mitchell&Krakauer.

## Writing principle

> "Strive to make my writing unsummarizable, in the sense that it has so little fluff left in it that if you take any words out, as summaries by definition do, you lose a lot of interesting ideas."
> — Paul Graham

This applies to paper notes too. Every sentence should earn its place.

## How notes are structured

Each paper note is a markdown file with YAML frontmatter:
- `title`, `authors`, `arxiv_id`, `arxiv_url`, `published`
- `memory_mechanism` or `mechanism` — what the paper does
- `tags` — for clustering and search
- One-line take, pros/cons, abstract summary

## Work tracking

We use `bd` (Beads) for organizing work. Use `paper-` prefix for individual papers, `task-` prefix for related tasks.
