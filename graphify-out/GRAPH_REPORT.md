# Graph Report - gh-org-backup  (2026-11-11)

## Corpus Check
- 6 files · ~2,207 words
- Verdict: corpus is large enough that graph structure adds value.
- Unclassified: 6 file(s) not represented in the graph (top: (none) 6)

## Summary
- 34 nodes · 35 edges · 8 communities (3 shown, 5 thin omitted)
- Extraction: 100% EXTRACTED · 0% INFERRED · 0% AMBIGUOUS
- Token cost: 0 input · 0 output

## Graph Freshness
- Built from commit: `11e90f87`
- Run `git rev-parse HEAD` and compare to check if the graph is stale.
- Run `graphify update .` after code changes (no API cost).

## Community Hubs (Navigation)
- Issue tracker: GitHub
- Domain Docs
- gh-org-backup
- triage-labels.md
- SKILL.md

## God Nodes (most connected - your core abstractions)
1. `Issue tracker: GitHub` - 7 edges
2. `Domain Docs` - 5 edges
3. `gh-org-backup` - 4 edges
4. `Conventions` - 1 edges
5. `Language` - 1 edges
6. `Pull requests as a triage surface` - 1 edges
7. `Wayfinding operations` - 1 edges
8. `When a skill says "fetch the relevant ticket"` - 1 edges
9. `When a skill says "publish to the issue tracker"` - 1 edges
10. `Before exploring, read these` - 1 edges

## Surprising Connections (you probably didn't know these)
- `gh-org-backup script` --calls--> `auth()`  [EXTRACTED]
  scripts/gh-org-backup → scripts/gh-org-backup  _Bridges community 4 → community 3_
- `gh-org-backup script` --calls--> `die()`  [EXTRACTED]
  scripts/gh-org-backup → scripts/gh-org-backup  _Bridges community 4 → community 6_

## Import Cycles
- None detected.

## Communities (8 total, 5 thin omitted)

### Community 0 - "Issue tracker: GitHub"
Cohesion: 0.25
Nodes (7): Conventions, Issue tracker: GitHub, Language, Pull requests as a triage surface, Wayfinding operations, When a skill says "fetch the relevant ticket", When a skill says "publish to the issue tracker"

### Community 1 - "Domain Docs"
Cohesion: 0.33
Nodes (5): Before exploring, read these, Domain Docs, File structure, Flag ADR conflicts, Use the glossary's vocabulary

### Community 2 - "gh-org-backup"
Cohesion: 0.40
Nodes (4): gh-org-backup, Install as an agent skill, License, Run standalone

## Knowledge Gaps
- **5 thin communities (<3 nodes) omitted from report** — run `graphify query` to explore isolated nodes.

## Suggested Questions
_Not enough signal to generate questions. This usually means the corpus has no AMBIGUOUS edges, no bridge nodes, no INFERRED relationships, and all communities are tightly cohesive. Add more files or run with --mode deep to extract richer edges._