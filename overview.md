# LLM Wiki – Overview

## Purpose
This wiki compiles a knowledge base of Mark Pesce's audio/video recordings
(626 transcribed of 628 total in the corpus) into an interlinked,
evolving document: source pages, entity pages, concept pages, query
pages, this overview, and an index — per the schema in WIKI.md.

## Corpus at a glance
- **626** transcribed recordings → **625** distinct source pages
  (one exact re-upload folded as a duplicate; recorded in
  `_ingest_manifest.json` under `duplicates`).
- Two recordings are genuinely untranscribable (DV .mov files with no
  audio stream: `bscast.mov`, `bluestates-capture.mov`).
- All 626 transcribed recordings are documented as native Google Docs
  in the Drive archive (finalize complete 2026-08-26).
- Dates normalized 2026-09-04 (`tools/normalize_dates.py`): 440 of 625
  sources dated (filename-derived where possible), spanning 1993–2026;
  **185 remain unknown** (raw clips and re-uploads with no recoverable
  date). Implausible text-mined dates were reset rather than kept.
- Types: 205 interview, 112 panel, 82 news, 51 keynote, 47 lecture, 46 podcast, 38 clip, 24 workshop, 19 talk, 1 webinar.

## Entities (61 pages)
- **People (17):** alison-page, bernie-hobbs, chris-russell, christine-kininmonth, douglas-rushkoff, erik-davis, fiona-wood, george-greer, ivan-sutherland, james-bradfield-moody, james-ologhlin, mark-pesce, richard-vaughan, sally-deminks, terence-mckenna, tony-parisi, veena-sahajwala.
- **Organizations (25):** abc, anu, apple, battlestar-galactica, bbc, burning-man, esalen, facebook, google, lonely-planet, meta, microsoft, mit, monash, mozilla, npr, radio-national, rmit, stanford, the-new-inventors, the-next-billion-seconds, true-hallucinations, unsw, usc, wired.
- **Technologies (19):** 3d, agentic, ar, bitcoin, blockchain, chatgpt, decentraland, distributed-ledger, ethereum, javascript, libra, metaverse, pokemon-go, python, smart-contracts, vr, vrml, webgl, world-wide-web.

> Extraction is vocabulary-based (`tools/ingest_wiki.py`), including ASR
> misspelling variants ("Mark Pesci", "Venus Sahajwala"). The vocabulary
> was expanded 2026-09-04; entities not yet in the curated list can be added
> the same way.

## Concepts (50 pages)
Most-engaged themes (word-boundary counts): **broadcast (119), the-future (117), networks (79), connectivity (57), artificial-intelligence (54), virtual-reality (54), narrative (49), social-media (48), trust (44), social-networks (37), communication (36), surveillance (36)** —
full list in INDEX.md.

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

## Queries (20 pages)
`queries/` holds cited answers to research questions against the corpus
(WIKI.md §7.3): VR's evolution, hyperdistribution's arc, social media
and democracy, AI predictions, education, broadcasting's decline, the
attention economy, trust, the ABC's role, and the future of work. Each
answer cites specific source pages. Ask new questions the same way and
file the answers there.

## Structure
- `sources/` — 625 recording summaries, each annotated with entities and concepts.
- `entities/` — 61 pages (17 people, 25 orgs, 19 technologies).
- `concepts/` — 50 pages.
- `queries/` — 20 cited research answers.
- `lint/` — dated reports; latest in the directory (clean as of 2026-09-04).

## Status
- **Last built:** 2026-09-04 (vocabulary-expansion rebuild).
- **Quality:** lint clean — 0 broken links, 0 orphans, 0 missing
  cross-refs (see latest `lint/` report).
- **Known gaps:** 185 undated sources; entity vocabulary still
  curated (many one-off names not yet pages); most entity/concept pages
  below the top tier still carry TL;DR/Overview placeholders.
- **Next steps:** keep seeding queries/; synthesize remaining
  entity/concept prose; date-normalize the remainder from summary text.
