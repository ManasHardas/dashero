# Vendoring record — agentwaves

| | |
|---|---|
| **Upstream** | `git@github.com-personal:manashardas/agentwaves.git` |
| **Vendored at commit** | `ff074c955d25d87a6a83e21c5f7ff5dfc8eafeef` (`feat(protocol): clause #10 — throughput maximization`) |
| **Vendored on** | 2026-08-24 |
| **Method** | file copy (not a submodule) |
| **Local path** | `.orchestrator/` |

## Why a copy and not a submodule

Adoption step 2 in the upstream README requires editing `agents/*.md` in place to fill
stack placeholders (`<api-routes-dir>`, `<services-dir>`, …). Those edits are
project-specific and belong in this repo's history, not in a fork of the framework.
A submodule would either lose them or force a fork just to hold them.

Trade-off accepted: upstream changes do not arrive automatically. To pull them, see
§Updating below.

## Excluded from the copy

| Path | Why |
|---|---|
| `.git/` | vendoring, not nesting a repo |
| `.github/` | upstream's own CI (notifies a skill repo on protocol changes) — meaningless here, and GitHub only reads the root `.github/` anyway |
| `.gitignore` | upstream's root ignore file; its entries were folded into this repo's root `.gitignore` |
| `.DS_Store` | noise |

Everything else is byte-identical to upstream except the local patch below.

## Local patches

### 1. Project-root resolution in `scripts/*.sh` (all three)

**Problem.** All three scripts open with `cd "$(dirname "$0")/.."` and then reference
`plans/**` — and, in the guardrails script, run git invariant checks — relative to
that directory. This assumes the framework lives at the repo root. Under the
`.orchestrator/` layout the upstream README itself recommends, `dirname $0/..`
resolves to `.orchestrator/`, so every `plans/**` path misses and the git checks run
against the wrong tree.

**Fix.** Resolve the git toplevel from the script's own location, falling back to
upstream behaviour outside a git repo:

```bash
_SCRIPT_DIR="$(cd "$(dirname "$0")" && pwd)"
_ROOT="$(git -C "$_SCRIPT_DIR" rev-parse --show-toplevel 2>/dev/null || true)"
[[ -n "$_ROOT" ]] || _ROOT="$(cd "$_SCRIPT_DIR/.." && pwd)"
cd "$_ROOT"
```

Correct in both layouts: at the repo root the toplevel equals `dirname $0/..`.
Each patch is fenced with `--- LOCAL PATCH ---` / `--- END LOCAL PATCH ---` comments.

Applied to `scripts/session-start.sh`, `scripts/session-close.sh`,
`scripts/check-session-close-guardrails.sh`.

**Worth upstreaming.** This is an upstream bug, not a local preference.

## Known upstream inconsistency (not patched)

`templates/wave-state.md` writes its state heading as
`## Current state — YYYY-MM-DD (session N status)`, but
`check-session-close-guardrails.sh` check #2 greps for `post-S<N>` and check-session
auto-detection greps the same pattern. A file seeded verbatim from the template fails
check #2 and cannot auto-detect its session number.

Not patched in the vendored template — instead `plans/wave-state.md` uses the
`(post-S<N>)` form the script expects, and the convention is documented at the top of
that file and in the root `CLAUDE.md`. Also worth upstreaming.

## Placeholder customization — OUTSTANDING

Upstream adoption step 2 is **not done**: dashero has no stack yet, so the role docs
still carry unfilled placeholders. Build-agent scope fences are not enforceable until
these are filled. Current inventory:

| Placeholder | Appears in |
|---|---|
| `<api-routes-dir>` | `agents/backend.md`, `agents/infra.md`, `agents/orchestrator.md` |
| `<services-dir>` | `agents/backend.md`, `agents/infra.md`, `dispatch-templates/clause-3-*.md` |
| `<workers-dir>` | `agents/backend.md`, `agents/infra.md` |
| `<models-file>` | `agents/backend.md`, `agents/infra.md` |
| `<config-file>` | `agents/backend.md`, `agents/infra.md` |
| `<tests-dir>` | `agents/backend.md`, `dispatch-templates/clause-3-*.md` |
| `<backend-tests-dir>`, `<frontend-tests-dir>`, `<test-fixtures-dir>` | `agents/qa.md`, `agents/frontend.md` |
| `<frontend-app-dir>`, `<frontend-components-dir>`, `<frontend-lib-dir>` | `agents/frontend.md`, `agents/infra.md` |
| `<migrations-versions-dir>` | `agents/backend.md`, `agents/infra.md`, `agents/orchestrator.md`, `templates/phase-spec.md` |
| `<api-spec-path>`, `<api-codegen-output>` | `agents/orchestrator.md`, `agents/frontend.md`, `templates/phase-spec.md` |
| `<full-stack-up-command>` | `agents/infra.md` |

Run `grep -rn '<[a-z-]*-\(dir\|file\|path\|output\|command\)>' .orchestrator/` to
re-derive this list after any upstream update.

**Find/replace gotcha:** upstream is inconsistent about one name —
`<migrations-versions-dir>` (6 occurrences) vs `<migration-versions-dir>`
(1 occurrence, `agents/orchestrator.md`) vs `<migration-version-file>`
(1 occurrence, same file). A naive replace on the plural form silently leaves the
other two behind. Same for `<data-flow-doc-path>` and `<test-path>`, which appear
once each and are easy to miss.

## Updating from upstream

```bash
cd ~/Projects/agentwaves && git fetch origin && git log --oneline ff074c9..origin/main
# Review the diff, then re-copy and re-apply the local patch:
rsync -a --exclude='.git/' --exclude='.DS_Store' --exclude='.github/' \
      ~/Projects/agentwaves/ .orchestrator/
```

After re-copying: re-apply §Local patches (the `--- LOCAL PATCH ---` fences are gone
after an overwrite), re-fill placeholders, and bump the commit recorded at the top of
this file.
