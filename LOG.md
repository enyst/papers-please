# LOG

Append-only timeline of wiki maintenance. Newest first. One line per action; keep the
`## [date] op |` prefix so it stays greppable (`grep "^## \[" LOG.md | head`).
Ops: `ingest` (added a source), `query` (filed an answer/synthesis back), `lint`
(health-check), `meta` (schema/structure change).

## [2026-09-13] meta | Folded the separate `llm-wiki` prototype in: added `sources/` (karpathy-llm-wiki.md verbatim + METHODOLOGY.md) and `wiki/` (3 prose syntheses: what-is-agent-memory, memory-consolidation, memory-security, + index/sources). Fixed dead links to never-written articles; wired README/AGENTS "two layers". llm-wiki repo retired to a tombstone.
## [2026-09-13] ingest | Prompt-injection arXiv sweep (2607–2609) → 8 notes in notes/prompt-injection/ (CapScope, test-time-search, ECLIPSE, AgentDrift, DriftNet, No-Box/MCP, Semantic Overlays, CoRL, MMPIBench multimodal) + Simon Willison tag tracker in README
## [2026-09-13] query  | atlas: grounding & understanding → filed notes/atlas-grounding-understanding.md
## [2026-09-13] query  | atlas: agent harness → filed notes/atlas-harness.md
## [2026-09-13] query  | "make our knowledge a wiki" → filed notes/atlas-agent-memory.md (first cross-store atlas page)
## [2026-09-13] meta | Adopted Karpathy LLM-Wiki schema: added AGENTS.md + this LOG.md; README "wider atlas" section
## [2026-09-12] ingest | Karpathy "LLM Wiki" pattern → blogs/interesting-posts.md
## [2026-09-12] ingest | Classics batch (11) → notes/world-models-agi/ (Turing 1950, Nagel 1974, Searle 1980, Harnad 1990, Dennett 1991, Block 1995, Chalmers 1995, Bender&Koller 2020, Stochastic Parrots 2021, Mitchell&Krakauer 2023, Othello-GPT 2023, Lake 2015/2017)
## [2026-09-12] ingest | RSTA 384(2320) "World models in natural & artificial intelligence" theme issue (18 papers) → notes/world-models-agi/
