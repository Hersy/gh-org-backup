# gh-org-backup

An agent skill: log in to GitHub in the browser, pick an org (or your own account), and get one zip holding every repo you can read there, each with all branches checked out locally and all tags.

## Install

Any agent (Claude Code, Codex, Gemini CLI, Cursor, Copilot, opencode, Amp and ~80 more):

```sh
npx skills add Hersy/gh-org-backup --skill gh-org-backup -g
```

(`pnpm dlx skills add …` works the same.)

Then ask your agent to "back up my GitHub org".

<details>
<summary>Other ways</summary>

**Claude Code plugin** (updates through `/plugin`):

```
/plugin marketplace add Hersy/gh-org-backup
/plugin install gh-org-backup@gh-org-backup
```

**Agent-native installers:**

- Gemini CLI: `gemini skills install https://github.com/Hersy/gh-org-backup.git --path skills/gh-org-backup`
- Codex: ask `$skill-installer` to install `Hersy/gh-org-backup` path `skills/gh-org-backup`
- Amp: `amp skill add Hersy/gh-org-backup --global`

**Git only, no Node:**

```sh
git clone --depth 1 https://github.com/Hersy/gh-org-backup ~/.gh-org-backup
mkdir -p ~/.agents/skills ~/.claude/skills
ln -s ~/.gh-org-backup/skills/gh-org-backup ~/.agents/skills/gh-org-backup   # Codex, Gemini, Cursor, Copilot, opencode, Amp
ln -s ~/.gh-org-backup/skills/gh-org-backup ~/.claude/skills/gh-org-backup   # Claude Code
```

Update with `git -C ~/.gh-org-backup pull`.

</details>

## Requirements

`gh`, `git`, `zip`, and bash (macOS's built-in 3.2 is fine). macOS, Linux, WSL. If one is missing, the script says how to install it.

## Run without an agent

```sh
S=skills/gh-org-backup/scripts/gh-org-backup
$S                                  # interactive picker
$S --list                           # your login + orgs
$S --org acme --out ~/backups
```

Flags: `--out DIR`, `--keep` (keep unzipped clones), `--no-archived`, `--no-forks`, `-j N` (parallel clones, default 4).

## What you get

`<org>-<YYYYMMDD-HHMM>.zip` with `<owner>/<repo>/` inside: full clones, a local branch for every remote branch, all tags. Picking your own login includes every repo you can access: owned, collaborator, and org-member repos.

Auth reuses an existing `gh` login, asks for `repo` and `read:org` in the browser if missing, or runs `gh auth login --web` if you are not logged in. Clones use HTTPS through `gh`'s credentials, so no SSH key is needed. `GH_TOKEN` is honored.

Not included: wikis, issues/PRs, Git LFS objects (pointer files only). Orgs with SAML SSO need the token authorized for that org; the error message links to it.

## License

MIT
