# LLM Wiki – Overview

## Purpose
This wiki compiles a knowledge base of Mark Pesce's audio/video recordings
(626 transcribed of 628 total in the corpus) into an interlinked,
evolving document: source pages, entity pages, concept pages, this
overview, and an index — per the schema in WIKI.md.

## Corpus at a glance
- **626** transcribed recordings → **625** distinct source pages
  (one exact re-upload folded as a duplicate; recorded in
  `_ingest_manifest.json` under `duplicates`).
- Two recordings are genuinely untranscribable (DV .mov files with no
  audio stream: `bscast.mov`, `bluestates-capture.mov`).
- Dated sources span 1909–2050; **376 of 625 are undated** (raw clips
  and re-uploads without a date in filename or summary).
- Types: 205 interviews, 112 panels, 82 news, 47 lectures, 46 podcasts,
  38 clips, 51 keynotes, 24 workshops, 19 talks, 1 webinar.

## Entities (34 pages)
- **People (3):** Mark Pesce (388 sources), Douglas Rushkoff (16),
  Dr. George Greer (1).
- **Organizations (17):** Apple, Mozilla, Google, Microsoft, Facebook,
  Meta, MIT, Stanford, UNSW, ANU, Monash, RMIT, USC, NPR, ABC, BBC,
  Wired.
- **Technologies (14):** VRML, VR, AR, 3D, metaverse, Git, JavaScript,
  Python, LLM, ChatGPT, agentic, blockchain, Bitcoin, Ethereum.

> Extraction is vocabulary-based (`tools/ingest_wiki.py`): entities not
> in the curated list are not yet pages. Expanding the vocabulary and
> re-running ingest + compile is the way to grow this layer.

## Concepts (51 pages)
Most-engaged themes: **broadcast** (155), **the future** (117),
**networks** (79), **narrative** (58), **connectivity** (57),
**artificial intelligence** (54), **virtual reality** (54), **trust**
(48), **social media** (48), **communication** (42), **podcasting**
(41), **education** (41), **social networks** (37), **innovation** (37),
**surveillance** (36) — full list in INDEX.md.

## Key themes
- **Distribution & the creator economy** — hyperdistribution, digital
  distribution, crowdfunding, content creation: the long tail of who
  gets heard, and on what terms.
- **Networked society** — social networks, peer-to-peer, the swarm,
  attention economy, surveillance: how mediation reshapes power.
- **The 3D / immersive web** — VRML (1994) through virtual reality and
  the metaverse: the recurring claim that 3D on the web was early, not
  wrong.
- **AI & agency** — artificial intelligence, agentic systems,
  verification design, trust: how machines that act change the design
  burden.
- **Broadcast & media history** — the corpus' densest theme, tracing
  the migration from broadcast to participatory media.

## Structure
- `sources/` — 625 recording summaries, each annotated with entities and concepts.
- `entities/` — 34 pages (3 people, 17 orgs, 14 technologies).
- `concepts/` — 51 pages.
- `queries/` — empty; the QUERY workflow (WIKI.md §7.3) is the next major feature.
- `lint/` — dated reports; latest: report-2026-08-26.md (clean).

## Status
- **Last built:** 2026-08-26 (full-corpus rebuild).
- **Quality:** clean — 0 broken links, 0 orphans, 0 missing cross-refs.
- **Known gaps:** undated sources (376); entity vocabulary coverage;
  entity/concept pages carry template placeholders (TL;DR / Overview)
  awaiting LLM synthesis; contradiction lint (§7.2.4) not yet run.
- **Next steps:** seed queries/; synthesize TL;DR/Overview for the
  highest-traffic pages; expand entity vocabulary; git history.
