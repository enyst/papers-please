# Papers Please

Curated research paper notes for Liberty Labs. Each paper has structured frontmatter (title, authors, arXiv link, mechanism summary, one-line take) and a short analysis.

## Topics

| Directory | Papers | What |
|-----------|--------|------|
| `notes/memory/` | 63 | Agent memory — architectures, consolidation, benchmarks, security |
| `notes/prompt-injection/` | 11 | Prompt injection attacks and defenses — 8 approaches with pros/cons |
| `notes/prompt-enforcement/` | 8 | Deterministic enforcement of agent instructions (Prompt Shield research) |
| `notes/skills/` | 7 | Agent skill discovery, optimization, and benchmarking |
| `notes/long-context-and-prompting.md` | ~30 | Long-context evaluation, prompting techniques, reasoning |
| `notes/memory-and-rag.md` | ~10 | RAG and memory-retrieval hybrid approaches |
| `blogs/interesting-posts.md` | — | Curated blog posts and articles on AI/agents |

## How notes are structured

Each paper note is a markdown file with YAML frontmatter:
- `title`, `authors`, `arxiv_id`, `arxiv_url`, `published`
- `memory_mechanism` or `mechanism` — what the paper does
- `tags` — for clustering and search
- One-line take, pros/cons, abstract summary

## Work tracking

We use `bd` (Beads) for organizing work. Use `paper-` prefix for individual papers, `task-` prefix for related tasks.
