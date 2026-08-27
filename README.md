# Mark Pesce — LLM Wiki

A portable, interlinked knowledge base compiled from 626 transcribed
recordings of **Mark Pesce** — media commentator, VRML inventor (1994),
and researcher in agentic systems / AI safety.

This directory is **self-contained**: plain markdown + YAML frontmatter,
no external dependencies, no binary assets. Clone it and read it.

## Start here

1. **WIKI.md** — the schema: layout, page formats, workflows (INGEST,
   LINT, QUERY), conventions. Read this first.
2. **INDEX.md** — the content catalog: every page, one line each.
3. **overview.md** — the top-level synthesis: corpus shape and key themes.
4. **LOG.md** — append-only timeline of all actions.

## Layout

| Path        | What |
|-------------|------|
| `sources/`  | 625 pages — one per recording (summary + key points + named entities/concepts). Immutable. |
| `entities/` | 61 pages — 17 people, 25 organizations, 19 technologies. |
| `concepts/` | 50 pages — recurring themes (broadcast, the future, networks, AI, VR, …). |
| `queries/`  | 10 pages — cited research answers (workflow: WIKI.md §7.3). |
| `lint/`     | dated health reports; see the latest `report-*.md`. |
| `_ingest_manifest.json` | machine-readable map: slug → entities/concepts/dates/links. The compile + lint + index steps all read from this. |

Links use Obsidian-style `[[wiki-relative/path]]` — open any page and
follow the backlinks.

## Provenance

- Source of truth (recordings, transcripts, summaries) lives in the
  parent `nightshift/` project — this wiki **links** to it, never
  embeds it. Each source page carries the original Drive file id and
  link in its frontmatter.
- Built and maintained by an agent night-shift pipeline
  (`nightshift/tools/`: ingest → compile → lint → index). Rebuilds are
  deterministic and idempotent; hand-written TL;DR/Overview prose
  survives recompiles (see `compile_wiki.py`).
- Corpus status: 628 recordings total, 626 transcribed, 2 untranscribable
  (DV .mov files with no audio stream). 625 distinct source pages (one
  exact re-upload is recorded as a duplicate in the manifest).

## Status

- Last full rebuild: **2026-08-27** (dates normalized; entity vocabulary
  expanded; queries seeded) — lint clean (0 broken links, 0 orphans,
  0 missing cross-refs).
- Known gaps: 336 undated sources; entity vocabulary is curated and can
  be extended; lower-traffic entity/concept pages still carry
  TL;DR/Overview template placeholders.
