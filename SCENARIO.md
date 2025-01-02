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

The initial graph contains 21 reachable commits, eight local branches, and eight remote-tracking references (plus Git's symbolic `origin/HEAD`). The sibling `complex-branch-scenario-origin.git` bare repository is configured as `origin`. Its `main` has a remote-only commit that diverges from the local scenario-guide commits; fetch it with GitScope's explicit **Fetch** action to see both sides. Opening the repository makes no network requests.

The remote URL is relative to this repository, so keep the sibling bare repository beside this folder if moving the sample.

## Reset the remote-only update

The sample is read-only from GitScope, but using **Fetch** advances `origin/main`. To restore the initial ahead/behind test state without changing the checked-out branch, working files, or bare remote, run these commands from this folder:

```powershell
$baseline = git rev-parse refs/remotes/origin/main^
git update-ref refs/remotes/origin/main $baseline
```

This moves only the sample's local `origin/main` tracking reference back to the shared base. It does not reset the current branch or remove commits.
