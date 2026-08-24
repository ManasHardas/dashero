# Wave State

> **Purpose:** authoritative current state of the project. Updated by PM at session-close; read by Orchestrator at session-start. Eliminates session-amnesia about phase / wave / required activities.

> **Convention:** if you're starting a session, read THIS FILE FIRST (after fetch+reset), then `.orchestrator/agents/orchestrator.md` §Session-start ritual.

> **Heading convention:** the `## Current state` heading MUST carry a `(post-S<N>)` marker — `.orchestrator/scripts/check-session-close-guardrails.sh` auto-detects the session number from it (check #2).

---

## Current state — 2026-08-24 (post-S0)

**Phase:** none yet — pre-P1. No phase spec written.

**Wave:** none. Next wave to run is **Wave 0** of P1, which cannot start until a phase spec exists.

**Last session:** S0 was framework setup only (vendored agentwaves at `.orchestrator/`, seeded `plans/`, wrote `CLAUDE.md`). No commits on `main` yet at file-write time.

**Carry-over slots:** none.

**Open blockers (must resolve before next required activity):**
- No stack decided. `.orchestrator/agents/*.md` still carry unfilled placeholders (`<api-routes-dir>`, `<services-dir>`, `<frontend-app-dir>`, `<migrations-versions-dir>`, `<models-file>`, `<config-file>`, `<tests-dir>`, `<full-stack-up-command>`, …). Build-agent scope fences are not enforceable until these are filled. See `.orchestrator/VENDOR.md` §Placeholder customization.
- No product plan / user-flows doc, so PM-Designer has nothing to sanity-check a phase spec against (per `.orchestrator/agents/pm-designer.md` §Phase sanity check).
- No `plans/feature-p1-<slug>.md` phase spec.

**Next required activities (in order):**
1. ⏳ Decide what dashero is and what P1 ships — product plan + user flows. (Pre-Wave-0 ideation; `superpowers:brainstorming` is the sanctioned tool here per `.orchestrator/agents/orchestrator.md` §Meta-skill conflict carve-out.)
2. ⏳ Decide the stack, then fill the placeholders in `.orchestrator/agents/*.md`.
3. ⏳ Write `plans/feature-p1-<slug>.md` from `.orchestrator/templates/phase-spec.md`.
4. ⏳ Wave 0 — contract freeze (orchestrator alone) + PM-Designer phase-sanity-check + `[P1] Phase tracking` issue.
5. ⏳ Wave 0.5 — parallel Backend + Frontend + Infra issue decomposition.

**Operating mode:** **ACTIVE** — required. New phase boundary, new contract surfaces, first-of-class everything, and no filed issues exist. DEGRADED is unreachable on this project until at least one phase has shipped.

**Throughput mode:** **serial** — `plans/velocity.json` has zero entries, so no class anchor has n≥3. Clause #10 parallel-by-default does not apply yet.

---

## Recent session history (rolling window of last 5 sessions)

| Session | Phase / Wave | Mode | PRs | Notes |
|---|---|---|---|---|
| S0 | — / setup | n/a | 0 | Vendored agentwaves @ `ff074c9` as `.orchestrator/`; seeded `plans/`; wrote `CLAUDE.md`. No product work. |

---

## Maintenance protocol

**At session-close (PM responsibility):**
1. Update `## Current state` block to reflect post-session reality — including the `(post-S<N>)` marker in the heading.
2. Move the just-closed session into `## Recent session history` (drop oldest if window > 5).
3. Update `**Carry-over slots**` if any slots were T-A/T-D/T-G dropped.
4. Update `**Next required activities**` for the next session (read `.orchestrator/agents/orchestrator.md` §Wave sequence + current phase tracking issue).
5. Commit alongside `velocity.json` + `capacity-log.md` + `next-session.md` updates in the session-close chore PR.

**At session-start (orchestrator responsibility):**
1. Read `plans/next-session.md` FIRST if it exists; fall back to this file (authoritative) when it's missing or stale.
2. Cross-reference with `.orchestrator/agents/orchestrator.md` §Session-start ritual.
3. Decide operating mode (ACTIVE vs DEGRADED) per the encoded rules.
4. If carry-over slots exist, dispatch them as first slots of the new session.
