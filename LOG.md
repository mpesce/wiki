# LOG — Mark Pesce LLM Wiki

Append-only timeline of all wiki actions (schema: WIKI.md §6).
Grep for the last five actions with: `grep '^## [' LOG.md | tail -5`

## [2026-08-24] ingest | initial wiki build: 471 source pages, 33 entities, 49 concepts
## [2026-08-24] lint | run | 0 broken links, 0 orphans, 0 missing cross-refs (stale baseline — corpus incomplete at the time)
## [2026-08-25] ingest | summarize_daemon completed the corpus: 626/626 transcribed recordings now have .sum files (144 new summaries this run, 0 failures)
## [2026-08-26] ingest | 154 new source pages ingested (141 + 4 stragglers) → 625 pages. 626/626 transcribed recordings covered (1 exact re-upload folded as duplicate, see _ingest_manifest.json "duplicates")
## [2026-08-26] tool | ingest_wiki.py: fixed slug-collision bug — same-named re-uploads and different names that slugify to the same base (case/resolution/speaker variants) were silently dropping 14 recordings. Now: first occurrence owns the base slug, Nth gets "<base>-N"; identical-content re-uploads are folded into the owner page. Added --rebuild flag. Fixed datetime.utcnow() deprecation.
## [2026-08-26] tool | ingest_wiki.py: fixed extraction false-positives — bare-substring matching inflated short slugs ("ar" matched "mark"/"argues" → 613 instead of 21; "git" matched "digital" → 160 instead of 0; "meta" matched "metaverse" → 55 instead of 4). All entity/concept matching now uses full word boundaries.
## [2026-08-26] ingest | --rebuild after extraction fix: 625 pages, git/llm/green-tech pages pruned (they were pure false-positives), smart-contracts + distributed-ledger now correctly surface
## [2026-08-26] tool | compile_wiki.py: added stale-page pruning (removes entity/concept pages whose slugs lost all sources); fixed source-slug overwrite bug
## [2026-08-26] compile | 34 entity + 50 concept pages rebuilt from corrected manifest
## [2026-08-26] lint | run | 0 broken links, 0 orphans, 0 missing cross-refs (report-2026-08-26.md). Note: 5 previously reported broken links were all in the hand-written INDEX.md, which referenced pages that never existed (e.g. concepts/ai-safety, entities/github) — those were hallucinated in an earlier session, not real corpus content (verified: 0 of 626 summaries mention ai-safety, hyperpeople, github, or rudy de luc).
## [2026-08-26] tool | build_index.py created: INDEX.md is now regenerated from the manifest instead of hand-written
## [2026-08-26] finalize | finalize_daemon restarted (had been stopped since 2026-08-21): 110 Google Docs created in 17.5 min, 0 failures → 626/626 transcribed recordings now documented in Drive
## [2026-08-26] update | INDEX.md regenerated (3 people, 17 orgs, 14 technologies, 50 concepts, 625 sources); LOG.md restored to proper timeline format; overview.md + WIKI.md §10 updated
## [2026-08-26] git | wiki/ initialised as a git repo (portability per TASK.md); initial commit 8182f97 + rebuild commit
