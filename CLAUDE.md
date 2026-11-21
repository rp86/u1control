## Branch strategy

- `main`: clean mirror of `upstream/main`. Fast-forward only (`git fetch upstream && git merge --ff-only upstream/main`). Never commit here.
- `local_use`: long-lived personal branch holding this file, `docs/agents/`, `GLOSSARY.md`, `docs/adr/`, `.scratch/` and any local-only changes. Pushed to `origin` as backup. Update with `git merge main` (not rebase).
- `fix/<slug>` / `feat/<slug>`: always cut from `main`, never from `local_use` (e.g. `git worktree add ../u1control-<slug> main -b fix/<slug>`). Open upstream PRs from these. Merge into `local_use` for local use.
- `.scratch/` and these docs exist only on `local_use`; run the issue-tracker skills from the `local_use` checkout. Never include them in a PR to upstream.

## Agent skills

### Issue tracker

Issues are local markdown files under `.scratch/<feature>/`. See `docs/agents/issue-tracker.md`.

### Triage labels

Default five-role vocabulary, recorded as a `Status:` line. See `docs/agents/triage-labels.md`.

### Domain docs

Single-context: root `GLOSSARY.md` + `docs/adr/` (created lazily). See `docs/agents/domain.md`.
