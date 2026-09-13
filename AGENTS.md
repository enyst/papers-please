# AGENTS.md — how to maintain this wiki

This repo is an **LLM-maintained knowledge wiki** (Karpathy's "LLM Wiki" pattern:
`blogs/interesting-posts.md` → 2026-04-04). You (the agent) write and maintain the notes;
the human does sourcing, exploration, and asks the questions. This file is the **schema**:
the conventions and workflows that make you a disciplined maintainer instead of a generic
chatbot. Read it before ingesting a source, answering a query against the corpus, or
tidying up.

## What this wiki is

Curated, durable notes on external research — papers, blog posts, talks — about AI agents,
LLMs, and the science of intelligence. It is **not** SmolPaws' own memory (that lives in
`~/.smolpaws/memory/`) and **not** system/architecture docs (those live in
`smolpaws/docs/`). Keep those boundaries: this wiki is *external knowledge digested for
reuse*.

The point (per Karpathy): a **persistent, compounding artifact**, not RAG. Cross-references
are already made, contradictions already flagged, syntheses already written. It gets richer
with every source added and every question asked. Prefer **index over embeddings** — a
markdown catalog you read first, then drill into. No RAG infra.

## Three layers

1. **Raw sources** — `pdfs/`, `transcripts/`. Immutable; read, never edit. Source of truth.
2. **The wiki** — `notes/**` + `blogs/interesting-posts.md`. You own this entirely.
3. **The schema** — this file, plus the top-level `README.md` (catalog) and each
   `notes/<topic>/README.md` (per-topic index).

## Layout

```
README.md                     top-level catalog: topic table + conventions
AGENTS.md                     this file (the schema)
LOG.md                        append-only timeline of ingests / queries-filed / lint passes
notes/<topic>/                one directory per topic
  README.md                   the topic index (scope, method, grouped list of notes)
  <slug>.md                   one note per paper/source
notes/<single-file>.md        legacy flat reading lists (long-context-and-prompting.md, ...)
blogs/interesting-posts.md    dated notes on blog posts / tweets / talks (newest first)
pdfs/ transcripts/            raw sources (immutable)
```

## Note format (keep it consistent)

Every paper/source note is markdown with **YAML frontmatter** then bulleted analysis.

Frontmatter — use what applies; don't invent noise:
- `title`, `authors` (list), `published`, `source`
- `arxiv_id` + `arxiv_url` when on arXiv; otherwise `doi` and/or `url`, plus `source_pdf`
  (the copy you actually read) when it differs from the canonical link
- `mechanism` (or `memory_mechanism` in `notes/memory/`) — one sentence: what it does
- `read_depth` — `full` | `abstract-only` | `from knowledge` (be honest)
- `tags` (list, for clustering/search); `categories` optional

Body — lead with a **one-line take**, then bullets. Recommended beats: what it does /
the key idea or mechanism / results or evidence / honest caveats / **why it matters for
us** (SmolPaws / Engel's threads: memory, concept formation, harness, grounding). End with
a **source** line linking where you read it. **Cite, link, and flag uncertainty** — if you
didn't read the full text, say so in `read_depth` and the source line.

Writing bar (from `README.md`, Paul Graham): make it *unsummarizable* — every sentence earns
its place, no filler. Also follow the `writing-for-agents` skill (this file is read by
agents): short imperatives, one idea per sentence, state doubt plainly.

Filenames: lowercase, hyphenated, descriptive `slug.md` (e.g.
`harnad-symbol-grounding-problem.md`).

## The three operations

### Ingest (add a source)
1. Get the source. Prefer the primary source. Publishers behind Cloudflare/paywalls:
   try `curl`, then `https://r.jina.ai/<url>` (jina reader), then the dedicated Chrome
   (see `smolpaws/docs/smolpaws/TOOLS.md`). If you can only reach an abstract, set
   `read_depth: abstract-only` and say which parts you didn't read.
2. Decide the topic dir (or propose a new one — see below). Write the note in the format
   above.
3. **Update the topic `README.md`** — add the note to its grouped list with a one-line
   summary (this is the topic's `index`).
4. **Update the top-level `README.md`** topic table if a count or a topic changed. (Counts
   there drift; refresh the row you touched — `ls notes/<topic>/*.md | wc -l`.)
5. **Append a `LOG.md` entry** (format below).
6. If it changes or contradicts an existing note, update that note too and note the change.

A single ingest may touch several files (the note + topic README + top README + LOG). That
is expected and correct — that's what keeps the wiki coherent.

### Query (answer a question from the corpus)
1. Read the top-level `README.md`, then the relevant topic `README.md`(s), then drill into
   notes. Search with `grep -ri "<term>" notes/` for breadth.
2. Answer **with citations** (link the note files and their sources).
3. **File good answers back.** A synthesis, comparison, or cross-topic connection worth
   keeping should become a note (e.g. a `notes/<topic>/` concept page or a cross-cutting
   atlas page), not vanish into chat. Log it as a `query` entry. This is how exploration
   compounds.

### Lint (periodic health-check)
Ask for or run a lint pass. Look for: contradictions between notes; stale claims a newer
source supersedes; orphan notes missing from their topic README; concepts referenced a lot
but lacking their own page; missing cross-references; stale counts in `README.md`; sources
worth chasing. Fix what's cheap; list the rest. Log a `lint` entry.

## LOG.md

Append-only, newest at top. One line per meaningful action, consistent prefix so it's
greppable (`grep "^## \[" LOG.md | head`):

```
## [YYYY-MM-DD] ingest | <title> → notes/<topic>/<slug>.md
## [YYYY-MM-DD] query  | <question> → filed notes/<topic>/<slug>.md
## [YYYY-MM-DD] lint   | <what was checked / fixed>
```

## Adding a topic

Create `notes/<topic>/` with a `README.md` (scope, what's in/out, how sources were found,
grouped list). Add a row to the top-level `README.md` table. Keep topics few and legible —
prefer an existing topic unless a genuinely new cluster forms.

## Boundaries (do not cross)

- Don't edit files in `pdfs/` or `transcripts/` — raw sources are immutable.
- Don't put SmolPaws private memory, secrets, or machine/ops facts here — those belong in
  `~/.smolpaws/memory/` and `smolpaws/docs/`.
- Don't fabricate. No invented quotes, numbers, authors, or links. If unsure, mark it.

## Related knowledge stores (the wider atlas)

This wiki is one of several stores; the map lives in `README.md` → "The wider atlas". The
others: `smolpaws/docs/` (identity + system), OpenHands docs/SDK (canonical, link don't
copy), Letta `context-constitution.md` (memory philosophy we already apply in dreaming).

## Work tracking

Beads (`bd`) in this repo: `paper-` prefix for individual papers, `task-` prefix for related
work.
