# Complex branch scenario

Open this folder in GitScope to explore a small Git repository with a deliberately non-linear history. All commits use deterministic sample identities and dates.

## Branches and history

- `main` contains two independently developed features merged with `--no-ff`, followed by later work.
- `feature/authentication` and `feature/search` remain as merged branch references.
- `feature/observability` and `feature/notifications` are unfinished branches that have diverged from `main`.
- `release/1.x` branches from the `v1.0.0` release and contains a separate maintenance history.
- `hotfix/1.0.1` branches from the release line and is merged back into it.
- `develop` contains work in progress beyond the current `main` tip.
- `v1.0.0` and `stable-1.0` are two tags on the same merge commit; `v1.0.1` marks the release-line hotfix merge.

The initial graph contains 19 reachable commits, eight local branches, and eight remote-tracking references (plus Git's symbolic `origin/HEAD`). The sibling `complex-branch-scenario-origin.git` bare repository is configured as `origin`. Its `main` has one additional remote-only commit that can be discovered with GitScope's explicit **Fetch** action; opening the repository makes no network requests.

The remote URL is relative to this repository, so keep the sibling bare repository beside this folder if moving the sample.

## Reset the remote-only update

The sample is read-only from GitScope, but using **Fetch** advances `origin/main`. To restore the initial ahead/behind test state without changing the checked-out branch or working files, run these commands from this folder:

```powershell
$baseline = git rev-parse refs/remotes/origin/main^
git --git-dir=..\complex-branch-scenario-origin.git update-ref refs/heads/main $baseline
git update-ref refs/remotes/origin/main $baseline
```

These commands only move the sample's local remote reference and its matching reference in the sibling bare repository. They do not reset the current branch or remove any commits from the working repository.
