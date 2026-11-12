---
name: gh-org-backup
description: Back up every GitHub repo the user can read in one organization (or their whole account) into a single zip, with every branch checked out locally. Use when the user wants to download, back up, archive, export, mirror or zip all repos of a GitHub org or account.
---

# gh-org-backup

`scripts/gh-org-backup` (next to this file) does the whole job. Needs `gh`, `git`, `zip`. If one is missing the script stops and prints the install command; offer to run it for the user, never install without asking.

1. Run `scripts/gh-org-backup --list`. It prints the user's login first, then their orgs, one per line.
   - If the user is not logged in, it starts GitHub's browser login and prints a one-time code and `https://github.com/login/device`. Show both to the user and tell them to approve in the browser; the command continues by itself once they do.
2. Show the list and ask which one to back up. Picking their own login backs up every repo they can access (owned, collaborator, and repos of every org they belong to).
3. Ask where to save the zip (default: current directory) and whether to skip archived repos or forks. Skip this if the user already said.
4. Run `scripts/gh-org-backup --org <name> [--out <dir>] [--no-archived] [--no-forks]`. Large orgs take a while; use a long timeout or run it in the background.
5. Report the zip path from the `Done:` line. Exit code 3 means some repos failed; relay the `Failed:` lines.

Other flags: `--keep` keeps the unzipped clones beside the zip, `-j N` sets parallel clones (default 4).
