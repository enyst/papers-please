# How to Generate Wiki Articles

Based on Karpathy's [LLM Wiki pattern](karpathy-llm-wiki.md) ([original gist](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)).

## The Core Idea

Instead of RAG (re-derive knowledge every query), the LLM **incrementally builds and maintains a persistent wiki**. The wiki is the compiled artifact — knowledge synthesized once and kept current, not re-derived from raw sources on every question.

## Architecture

```
notes/          Per-paper source notes (the raw layer; source of truth)
wiki/           LLM-generated prose topic articles (the published synthesis)
sources/        This methodology + Karpathy's original instructions
```

- **notes/** holds the per-paper notes across all topics (see `AGENTS.md` for the note schema)
- **wiki/** holds the published prose articles — synthesized across many notes
- When a new paper is added to `notes/`, the LLM updates the relevant wiki article(s)

> History: `wiki/` and `sources/` were folded in from the separate `llm-wiki` prototype on
> 2026-09-13. That repo used `raw/` symlinks into this one; now everything lives here.

## How to Generate an Article

### 1. Read the source papers

For a topic article (e.g. "Memory Security"), read all paper notes tagged with relevant tags. Each note has:
- YAML frontmatter: title, authors, arxiv URL, mechanism, setting, tags
- One-line take
- What it stores / how memory is used
- Why it matters
- Abstract summary

### 2. Synthesize, don't summarize

The article should **synthesize across papers**, not list them sequentially. Key principles:
- Organize by concept, not by paper
- Cross-reference related ideas from different papers
- Note contradictions and open questions
- Include our own implementation perspective where relevant (SmolPaws experience)

### 3. Article structure

Each article follows this pattern:
1. **Opening** — the problem or concept in plain language, no jargon lead
2. **Main sections** — organized by sub-topic, each drawing on multiple papers
3. **Our perspective** — what we learned building SmolPaws (where applicable)
4. **Papers Referenced** — table with paper name, year, and key contribution
5. **See also** — links to related wiki articles

### 4. Citation style

- Inline: `Paper Name ([Author et al., Year](arxiv-url))` on first mention
- Subsequent: just the paper name
- Reference table at the bottom for all cited papers

### 5. Cross-reference other articles

Link liberally to other wiki articles using relative markdown links: `[Memory Security](memory-security.md)`. These links should be meaningful — "see X for a deeper treatment of Y."

### 6. Update, don't append

When new papers arrive, **update existing articles** rather than appending new sections. The wiki should read as a coherent whole, not show the history of when papers were added.

## How to Add New Papers

1. Add the paper note to `notes/memory/` following the existing format (see `AGENTS.md`)
2. Determine which wiki articles the paper is relevant to (check tags)
3. Integrate the paper's key findings into the relevant article sections
4. Add it to `wiki/sources.md` in the appropriate year/category
5. Update paper counts in `wiki/index.md` and the top-level `README.md`
6. Append a `LOG.md` entry and commit

## Karpathy's Original Instructions

The full original pattern description is in [karpathy-llm-wiki.md](karpathy-llm-wiki.md). Key points:

- The wiki is a **persistent, compounding artifact** — it gets richer with every source
- The human curates sources and asks questions; the LLM does the writing
- Cross-references should already be there; contradictions should already be flagged
- The knowledge is compiled once and kept current, not re-derived on every query
