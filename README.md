# gh-org-backup

Log in to GitHub in the browser, pick an org (or your own account), and get one zip holding every repo you can read there, each with all branches checked out locally and all tags.

Requires `gh`, `git`, `zip` and bash (macOS's built-in 3.2 is fine). Linux, macOS, WSL.

## Install as an agent skill

Clone into your agent's skills directory:

| Agent | Command |
|---|---|
| Claude Code | `git clone https://github.com/Hersy/gh-org-backup ~/.claude/skills/gh-org-backup` |
| Codex | `git clone https://github.com/Hersy/gh-org-backup ~/.codex/skills/gh-org-backup` |
| Gemini CLI | `git clone https://github.com/Hersy/gh-org-backup ~/.gemini/skills/gh-org-backup` |
| Other (Agent Skills standard) | `git clone https://github.com/Hersy/gh-org-backup ~/.agents/skills/gh-org-backup` |

Then ask the agent to "back up my GitHub org".

## Run standalone

```sh
git clone https://github.com/Hersy/gh-org-backup
gh-org-backup/scripts/gh-org-backup            # interactive picker
gh-org-backup/scripts/gh-org-backup --list     # your login + orgs
gh-org-backup/scripts/gh-org-backup --org acme --out ~/backups
```

Flags: `--out DIR`, `--keep` (keep unzipped clones), `--no-archived`, `--no-forks`, `-j N` (parallel clones, default 4).

Output: `<org>-<YYYYMMDD-HHMM>.zip` with `<owner>/<repo>/` inside. Picking your own login includes every repo you can access: owned, collaborator, and org-member repos.

Auth: reuses an existing `gh` login, asks for `repo` and `read:org` scopes in the browser if missing, or runs `gh auth login --web` if you are not logged in. Clones use HTTPS through `gh` credentials, so no SSH key is needed. `GH_TOKEN` is honored.

Not included: wikis, issues/PRs, Git LFS objects (pointer files only).

## License

MIT
