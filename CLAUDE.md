## Agent skills

### Issue tracker

GitHub Issues on `Hersy/gh-org-backup`, via `gh -R Hersy/gh-org-backup`. See `docs/agents/issue-tracker.md`.

### Triage labels

Default five-role vocabulary (`needs-triage`, `needs-info`, `ready-for-agent`, `ready-for-human`, `wontfix`). See `docs/agents/triage-labels.md`.

### Domain docs

Single-context: root `GLOSSARY.md` + `docs/adr/`. See `docs/agents/domain.md`.

## graphify

This project has a knowledge graph at graphify-out/ with god nodes, community structure, and cross-file relationships.

Rules:
- When graphify-out/graph.json exists, run `graphify query "<question>"` before your first grep, search or source-file read for a codebase question, and put this rule in every subagent prompt that explores code. Read raw files only for lines the graph or an earlier read already located. Use `graphify path "<A>" "<B>"` for relationships and `graphify explain "<concept>"` for focused concepts. These return a scoped subgraph, usually much smaller than GRAPH_REPORT.md or raw grep output.
- If graphify-out/wiki/index.md exists, use it for broad navigation instead of raw source browsing.
- Read graphify-out/GRAPH_REPORT.md only for broad architecture review or when query/path/explain do not surface enough context.
- A committed graphify-out/graph.json is rewritten whole on every build, so a large diff to it in a pull request is expected. Do not flag it as churn or suggest skipping the graph rebuild or its hooks.

## Project

Agent skill at `skills/gh-org-backup/` (`SKILL.md` + one Bash script, `scripts/gh-org-backup`), that backs up every readable repo of a GitHub org or account into one zip. Public. Installed via `npx skills add` (vercel-labs/skills), the Claude plugin marketplace in `.claude-plugin/`, or git clone + symlink; see README.

- Keep the skill folder self-contained: installers copy only `skills/gh-org-backup/`. Nothing else may ship a `SKILL.md` (that is why gfy runs in local mode here, not shared).

- Must run on macOS `/bin/bash` 3.2: no `mapfile`, no associative arrays, no `${var,,}`. Check with `/bin/bash -n` and `mise exec aqua:koalaman/shellcheck -- shellcheck skills/gh-org-backup/scripts/gh-org-backup`.
- Runtime deps are only `gh`, `git`, `zip`. Auth is `gh`'s browser device flow; clones go over HTTPS via `gh auth git-credential` so no SSH key is needed.
- Picking the user's own login means `user/repos?affiliation=owner,collaborator,organization_member` (everything accessible), not owned repos only. Deliberate.
- No test harness. Verify with a real run: `skills/gh-org-backup/scripts/gh-org-backup --org <small-org> --out <tmp> --keep`, then compare `git branch` vs `git branch -r` counts in a clone.

## Project graph notes

Graph: TBD (not built yet; run `gfy build`).
Graph is local (not committed).
Indexed: `skills/`, `README.md`
Excluded via .graphifyignore: defaults
If a symbol is missing from the graph, check the ignore file before concluding
it does not exist.

Deep-pass paths (`GFY_DEEP_PATHS`): none.

Known graph weaknesses in this repo:
- Single Bash script; Bash function calls resolve poorly in AST extraction.

Entry points to query first: `clone_one`, `list_repos`, `auth`
