# Branching convention

Remotes: `origin` = fork (`rp86/u1control`), `upstream` = `bloodf/u1control`.

| Branch | Cut from | Purpose | Goes upstream? |
| --- | --- | --- | --- |
| `main` | n/a | Clean mirror of `upstream/main`. Fast-forward only, never commit here. | n/a |
| `local-use` | `main` | Long-lived personal branch: `CLAUDE.md`, `docs/agents/`, `GLOSSARY.md`, `docs/adr/`, `.scratch/`, local-only changes. Backed up on `origin`. | Never |
| `fix/<slug>` | `main` | Bug fix intended for upstream. | Yes (PR) |
| `feat/<slug>` | `main` | Feature; may be upstreamed, or merged only into `local-use`. | Maybe |

**Rule: never branch from `local-use`.** Anything cut from it carries personal files into the PR.

## Commands

Sync `main` with upstream:

    git checkout main
    git fetch upstream
    git merge --ff-only upstream/main
    git push origin main

Pick up upstream changes in `local-use` (merge, not rebase):

    git checkout local-use
    git merge main
    git push

Start a fix or feature in a worktree (keeps `local-use` checked out in the main directory):

    git worktree add ../u1control-<slug> main -b fix/<slug>     # or feat/<slug>
    cd ../u1control-<slug>
    # ...work, commit...
    git push -u origin fix/<slug>
    gh pr create --repo bloodf/u1control --head rp86:fix/<slug> --fill

Use a feature locally (without or before upstreaming):

    git checkout local-use
    git merge feat/<slug>
    git push

After upstream merges your PR:

    # sync main (see above), then
    git checkout local-use && git merge main && git push
    git worktree remove ../u1control-<slug>
    git branch -d fix/<slug> && git push origin --delete fix/<slug>

## Notes

- Run the issue-tracker skills from the `local-use` checkout: `.scratch/` exists only there.
- From a worktree, read an issue with `git show local-use:.scratch/<feature>/issues/01-<slug>.md`.
- Before opening a PR, check no personal files leaked: `git diff --stat upstream/main...HEAD`.
- Experiments you know will stay local can be committed directly on `local-use`.
