# Capacity log

> **Purpose:** session-by-session ledger. Each session's PM dispatches an entry at session-close summarizing what landed, calibration findings, watchdog outcomes, and S<N+1> forecast.

> **Convention:** newest sessions at the bottom. PM appends; orchestrator reads (along with `velocity.json`) at session-start to compute Bayesian-updated priors.

> **Entry shape:** copy the block from `.orchestrator/templates/capacity-log.md`.

---

## Session 0 — 2026-08-24 (framework setup)

**Stage 2 PM:** not dispatched — no product work in this session.

**Wave executed:** none (pre-P1 setup).

**Build PRs merged:** 0.

**Activities completed:**
- Vendored agentwaves @ `ff074c9` into `.orchestrator/` (see `.orchestrator/VENDOR.md`).
- Patched the three vendored scripts to resolve the project root via git toplevel (upstream assumes root install).
- Seeded `plans/wave-state.md`, `plans/capacity-log.md`, `plans/velocity.json`.
- Wrote root `CLAUDE.md` from `.orchestrator/CLAUDE.md.snippet` with paths rewritten to `.orchestrator/`.

**Issues filed:** 0 (no GitHub remote configured yet).

**Discipline holds:**
- T-A / T-G / T-D: n/a — no dispatches.
- T-M / T-X / T-Y: n/a — no dispatches, no merges.
- HARD CONSTRAINT: n/a — no code verified.

**Calibration findings:**
1. Upstream scripts hardcode `cd "$(dirname "$0")/.."` as the project root, which breaks under the vendoring layout the upstream README itself recommends (`.orchestrator/`). Patched locally; worth an upstream issue.
2. `.orchestrator/templates/wave-state.md` writes its heading as `(session N status)`, but `check-session-close-guardrails.sh` check #2 greps for `post-S<N>`. The template and the guardrail disagree. Seeded file uses `post-S0`; worth an upstream issue.

**Cumulative dispatched:** 0k — no agent dispatches.

**Forecast S1:**
- Slot 1: pre-Wave-0 ideation — decide what dashero is; produce product plan + user flows.
- Slot 2: stack decision + placeholder fill across `.orchestrator/agents/*.md`.
- Slot 3 (stretch): draft `plans/feature-p1-<slug>.md` from the phase-spec template.
- Watchdog triggers: none armed — no anchors exist. Operating mode is forced ACTIVE.
