# Papers Please

Curated research paper notes. Each paper has structured frontmatter (title, authors, arXiv link, mechanism summary, one-line take) and a short analysis.

## Topics

| Directory | Papers | What |
|-----------|--------|------|
| `notes/memory/` | 70 | Agent memory — architectures, consolidation, benchmarks, security, tools |
| `notes/prompt-injection/` | 13 | Prompt injection attacks and defenses — approaches with pros/cons |
| `notes/prompt-enforcement/` | 9 | Deterministic enforcement of agent instructions (Prompt Shield research) |
| `notes/skills/` | 9 | Agent skill discovery, optimization, benchmarking, and context file evaluation |
| `notes/harness/` | 2 | Agent harnesses — the subsystem that turns a model into an agent; code-as-harness, behavior→code maps |
| `notes/prompt/` | 2 | Prompting techniques and adversarial (synthetic languages, Waluigi Effect) |
| `notes/foundational/` | 5 | Foundational agent & AGI-theory papers — ReAct, CodeAct, RLM, weakest-hypothesis, freedom-third-axis |
| `notes/interpretability/` | 3 | Mechanistic interpretability — steering/ablation, safety-entanglement, and the philosophy of not over-reading it |
| `notes/verification/` | 1 | Formal verification of generated code |
| `notes/misc/` | 4 | Everything that doesn't fit a category yet (evaluation, survey simulation, ensembling) |
| `notes/long-context-and-prompting.md` | ~30 | Long-context evaluation, prompting techniques, reasoning |
| `notes/memory-and-rag.md` | ~10 | RAG and memory-retrieval hybrid approaches |
| `blogs/interesting-posts.md` | — | Curated blog posts and articles on AI/agents |

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
