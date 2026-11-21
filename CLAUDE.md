## Branch strategy

- `main`: clean mirror of `upstream/main`. Fast-forward only (`git fetch upstream && git merge --ff-only upstream/main`). Never commit here.
- `local-use`: long-lived personal branch holding this file, `docs/agents/`, `GLOSSARY.md`, `docs/adr/`, `.scratch/` and any local-only changes. Pushed to `origin` as backup. Update with `git merge main` (not rebase).
- `fix/<slug>` / `feat/<slug>`: always cut from `main`, never from `local-use` (e.g. `git worktree add ../u1control-<slug> main -b fix/<slug>`). Open upstream PRs from these. Merge into `local-use` for local use.
- Full commands: `docs/agents/branching.md`.
- `.scratch/` and these docs exist only on `local-use`; run the issue-tracker skills from the `local-use` checkout. Never include them in a PR to upstream.

### Agent directives

- Before committing, check `git branch --show-current`. If it is `main`, stop and switch; never commit there.
- To fix a bug or build a feature, create a worktree from `main` (`fix/<slug>` or `feat/<slug>`) rather than editing on `local-use`, unless the change is explicitly local-only.
- Never create a branch from `local-use`.
- Before opening a PR to upstream, run `git diff --stat upstream/main...HEAD` and confirm no `CLAUDE.md`, `docs/agents/`, `GLOSSARY.md`, `docs/adr/` or `.scratch/` files are included.
- Commit issue-tracker, glossary and ADR changes on `local-use` only.

## Agent skills

### Issue tracker

Issues are local markdown files under `.scratch/<feature>/`. See `docs/agents/issue-tracker.md`.

### Triage labels

Default five-role vocabulary, recorded as a `Status:` line. See `docs/agents/triage-labels.md`.

### Domain docs

Single-context: root `GLOSSARY.md` + `docs/adr/` (created lazily). See `docs/agents/domain.md`.
