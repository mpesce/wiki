# WIKI.md — Mark Pesce: LLM Wiki Schema

> This is the schema file for the LLM Wiki. Read it first, every session.
> It defines conventions, directory layout, and the three core workflows
> (INGEST, LINT, QUERY). Keep it in sync with the wiki as it evolves.

---

## 1. What this is

A personal knowledge base built from ~626 audio/video recordings by
**Mark Pesce** — media commentator, technologist, VRML inventor (1994),
and researcher in agentic systems / AI safety. The corpus is a long
running body of talks, interviews, lectures, podcasts, news segments,
Q&As, and raw clips. This wiki compiles that corpus into a persistent,
interlinked, evolving document rather than a flat archive.

The wiki has been ingested from transcripts (see `tools/` in the parent
`nightshift` folder) and summaries of each recording. The goal is to
produce a *living* wiki: entity pages, concept pages, source pages, an
overview/synthesis, an index, a log, and a running lint report.

## 2. Three-layer architecture (after karpathy's "LLM Wiki")

1. **Raw sources** — the immutable recordings/transcripts/summaries in the
   parent `nightshift/` project (the "source of truth"). The wiki never
   modifies these.
2. **The wiki** — this directory. LLM-generated markdown that owns the
   synthesis, cross-references, entity/concept pages, and evolution of
   understanding.
3. **This schema** — the config that makes the wiki a disciplined
   maintainer rather than a flat index.

## 3. Directory layout

```
wiki/
  WIKI.md          <- this file (schema; evolve with the wiki)
  INDEX.md         <- content catalog (one line per page, categorized)
  LOG.md           <- append-only timeline of all actions
  overview.md      <- high-level synthesis: the evolving thesis + big picture
  sources/         <- one page per source (recording)
  entities/        <- people, organizations, technologies, recurring figures
  concepts/        <- themes, ideas, frameworks, topics
  lint/            <- lint reports, contradiction log, cross-reference map
  queries/         <- answers to questions, filed as pages (query-as-a-source)
```

### 3.1 Page kinds and their job

| Kind          | Folder         | What it contains                                                                 |
|---------------|----------------|----------------------------------------------------------------------------------|
| Source        | `sources/`     | Summary of one recording + key points + named entities/concepts. Immutable.       |
| Entity        | `entities/`    | Person / organization / technology / recurring figure. Compiles every source that mentions them. |
| Concept       | `concepts/`    | Theme / idea / framework. Cites sources, notes internal debates and evolution.    |
| Overview      | `overview.md`  | Top-level synthesis. Updated as understanding deepens.                              |
| Query         | `queries/`     | A question asked against the wiki + a synthesized, cited answer.                  |
| Lint          | `lint/`        | Reports: contradictions, orphans, missing cross-refs, stale claims.              |

## 4. Page format

Every wiki page starts with YAML frontmatter, then markdown body.

### 4.1 Common frontmatter

```yaml
---
kind: source            # source | entity | concept | overview | query
slug: vrml-1994-invention
title: The Invention of VRML (1994)
tags: [technology, internet, 3d]
created: 2026-08-24
last_updated: 2026-08-24
source_count: 12        # how many sources mention this page (entities/concepts)
related:
  - concepts/hyperdistribution
  - entities/mark-pesce
  - sources/abc-2019-keynotes
---
```

### 4.2 Source page (`sources/`)

```yaml
---
kind: source
slug: abc-jjj-14mar06-interview
title: ABC-JJJ 14 Mar 2006 Interview
drive_id: <original drive file id>
source_link: https://drive.google.com/...
type: interview          # talk | interview | lecture | podcast | news | clip | panel | workshop
date: 2006-03-14         # when known; else "unknown"
duration_min: ~12
tags: [early-web, social-media]
mentions:
  - entities/mark-pesce
  - concepts/social-networks
created: 2026-08-24
last_updated: 2026-08-24
---
# <title>

## Summary
<2-3 paragraph factual summary of the recording. What it is, main topic,
speakers if named, date. Order of appearance. No fabrication.>

## Key Points
- <a concrete claim / fact / number mentioned>
- <another>

## Named Entities
- <people/orgs/tech explicitly named, with one-line role>

## Related Concepts
- <concepts the source engages with, with why>

## Quotes
- "<a memorable direct quote with timecode if known>"
```

Source pages are IMMUTABLE once written — they are a faithful record of a
recording. To correct, add a note (see §7.3) rather than editing.

### 4.3 Entity / concept page

```yaml
---
kind: entity              # or concept
slug: mark-pesce
title: Mark Pesce
tags: [person]
source_count: 187
created: 2026-08-24
last_updated: 2026-08-24
related:
  - entities/mozilla
  - concepts/vrml
  - concepts/agentic-systems
---
# Mark Pesce

## TL;DR
<1-2 sentences: who/what + why they matter.>

## Overview
<Tighter narrative of the entity across the corpus. What's consistent,
what changed over time, how they relate to the thesis.>

## Key Facts
- <verifiable fact, cited to sources where relevant>

## In the Corpus
- <how this figure/idea appears over time; debates; evolution>

## Cross References
- see concepts/... , sources/...

## Debates / Open Questions
- <tensions, contradictions, things unresolved>

## Sources
- [[sources/...]]
```

Entity pages are MUTABLE — they compile and evolve as more sources arrive.

> **Note (2026-08-27):** `tools/compile_wiki.py` regenerates entity/concept
> pages on every run, but **preserves hand-written prose**: if a `TL;DR`,
> `Overview`, `In the Corpus`, `Cross References`, or
> `Debates / Open Questions` section no longer contains its `<placeholder>`,
> that text is carried forward into the regenerated page, and the original
> `created:` timestamp is kept. Write synthesis directly into the page; the
> recompile will not clobber it. Only the link lists and `last_updated` are
> regenerated.

### 4.4 Cross-reference syntax

Use double-bracket `[[wiki-relative-path]]` links (Obsidian-style).
Examples: `[[concepts/hyperdistribution]]`,
`[[entities/mark-pesce]]`, `[[sources/abc-jjj-14mar06-interview]]`.
The LINT pass (§7.2) flags **broken** links (targets that don't exist).

## 5. INDEX.md

Content catalog. One entry per page, categorized, each on its own line.

Format (one line per page, sorted by slug within category):

```markdown
## People
- [[entities/mark-pesce]] — media commentator, VRML inventor (1994), agentic-systems researcher. 187 sources.

## Technologies
- [[entities/vrml]] — Virtual Reality Modeling Language, 1994. 12 sources.

## Concepts
- [[concepts/hyperdistribution]] — the long tail of online distribution. 23 sources.

## Sources (626 total; N ingested)
- [[sources/abc-jjj-14mar06-interview]] — ABC interview, 2006-03-14.
```

Keep `## Sources` updated on every ingest with the ingested count
(`N ingested` of the queue total). Update `last_updated` in the header.

## 6. LOG.md

Append-only timeline. Every action adds one entry with a parseable
prefix so it can be grepped (`grep '^## [' LOG.md | tail -5`).

Format:

```markdown
## [2026-08-24] ingest | 30 source pages (total ingested: 30/626)
## [2026-08-24] ingest | +1 source page (total: 31/626)
## [2026-08-24] lint | run | 2 contradictions, 3 broken links, 5 orphans
## [2026-08-24] entity | created entities/mark-pesce (187 sources)
## [2026-08-24] concept | created concepts/hyperdistribution (23 sources)
## [2026-08-24] query | "how did Pesce's AI view change over time?" -> queries/ai-evolution
## [2026-08-24] update | overview.md revised; INDEX.md updated
```

## 7. Core workflows

### 7.1 INGEST (add one or many sources)

1. Read `tools/queue.json` + `tools/state.json` (source of truth).
2. For each not-yet-ingested recording with a `.sum` summary:
   - Load the summary + metadata (drive id, name, link, date, type).
   - Write `sources/<slug>.md` (§4.2). Slug = lowercase, dash-joined
     title with non-alphanumerics collapsed.
   - Extract candidate `mentions` (entities/concepts) from the summary
     via the shared extraction rules (see `tools/ingest_wiki.py`).
3. Append to `LOG.md`. Do NOT edit entity/concept pages during ingest —
   do that in the LINT/compile pass so cross-references are consistent.

Ingest is idempotent: skip any slug already present in `sources/`.

### 7.2 LINT (compile + health-check) — run after ingesting

1. **Compile entity/concept pages** from ingested sources: for each
   entity/concept, gather every source page that mentions it, aggregate
   their key points/quotes/mentions, and (re)write the page. Update
   `source_count`, `related`, `Sources` list.
2. **Broken links:** scan `[[...]]` links in every page; flag any target
   file that does not exist. See `lint/broken_links.md`.
3. **Orphans:** entity/concept/source pages with zero inbound `[[...]]`
   links (mentioned by nothing). See `lint/orphans.md`.
4. **Contradictions:** detect claims that conflict across sources
   (e.g. "VRML invented 1994" vs a source claiming another year; opposing
   views on the same concept). See `lint/contradictions.md`.
5. **Missing cross-refs:** concepts mentioned in sources but with no
   dedicated concept page. Flag for creation.
6. **Stale claims:** verify/tech claims superseded by later sources.
7. Write findings to `lint/report-<date>.md` and summarize in `LOG.md`.

### 7.3 QUERY (question-as-a-source)

1. Read `INDEX.md` + `LOG.md` to find relevant pages.
2. Read and synthesize the relevant entity/concept/source pages.
3. Write the answer to `queries/<slug>.md` with citations
   (`[[...]]` + source page refs). The answer is itself a source.

### 7.4 Correction / note convention

Do not rewrite source-page content. To record a correction or nuance,
append a dated note at the bottom:

```markdown
---
## Note (2026-08-24)
Clarification: source X says Y, but source Z corrects it to Z. See lint/contradictions.md.
---
```

## 8. Portability rules

- Markdown + YAML frontmatter only. No binary assets, no external DB.
- Keep the `wiki/` directory self-contained: it must be cloneable and
  fully readable on its own.
- Media (recordings/audio) stays in the parent `nightshift/` project —
  the wiki links, never embeds.
- Ingest tool `tools/ingest_wiki.py` uses only the Python standard library.

## 9. Conventions

- Write in plain, factual prose. No fabrication. If the source doesn't
  say it, don't imply it.
- Prefer present-tense synthesis over transcription.
- Cite with `[[...]]` links generously; the lint pass keeps them honest.
- Date format ISO `YYYY-MM-DD`. Unknown date = "unknown".
- Keep `INDEX.md` and `LOG.md` updated on every action.

## 10. Current status

- Total recordings in corpus: 628 (626 transcribed; 2 untranscribable —
  DV .mov files with no audio stream).
- Source pages ingested: 625 / 626 transcribed (626 recordings covered;
  1 exact re-upload folded as a duplicate — see `_ingest_manifest.json`).
- Dates normalized 2026-08-27 (`tools/normalize_dates.py`): 176 sources
  re-dated from filenames, 48 implausible text-mined dates reset, 148
  previously-unknown dates recovered. Plausibility window 1988-2026.
- Entity pages: 34 (3 people, 17 orgs, 14 technologies).
- Concept pages: 50. Query pages: 10 (seeded 2026-08-27).
- Last lint run: 2026-08-26 — 0 broken links, 0 orphans, 0 missing
  cross-refs (`lint/report-2026-08-26.md`).
- INDEX.md is regenerated by `tools/build_index.py` (do not hand-edit).
- See LOG.md for the live timeline.
