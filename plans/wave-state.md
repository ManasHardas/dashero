# Wave State

> **Purpose:** authoritative current state of the project. Updated by PM at session-close; read by Orchestrator at session-start. Eliminates session-amnesia about phase / wave / required activities.

> **Convention:** if you're starting a session, read THIS FILE FIRST (after fetch+reset), then `.orchestrator/agents/orchestrator.md` §Session-start ritual.

> **Heading convention:** the `## Current state` heading MUST carry a `(post-S<N>)` marker — `.orchestrator/scripts/check-session-close-guardrails.sh` auto-detects the session number from it (check #2).

---

## Current state — 2026-08-26 (post-S1)

**Phase:** none yet — pre-P1. No phase spec written. **Wave 0 is deliberately not started.**

**Wave:** Wave -1 (adversarial ideation) is **complete**. `check-ideation-gate.sh` exits 0 — 9 ok / 0 warn / 0 fail against `plans/ideation-dashero.md`.

**Verdict:** `RESHAPE`, product-level. dashero as originally specified scored **last of eight** candidate product shapes on a rubric that double-weighted reachable-buyer and revenue arithmetic. The recommended shape is narrower — spreadsheet-native per-recipient reporting for agencies and freelancers — and is **itself gated on a market test, not on a build decision.**

**Wave 0 is blocked by KC-14, not by the gate script.** The gate is open; the operator has not confirmed a buyer. No product code is authorised until ≥5 of ~50 contacted producers-for-hire commit to paying, by **2026-09-12**. A one-hour competitive check (KC-15) runs first and can falsify the recommendation outright.

**Last session:** S1 — Wave -1 ideation. Eight agents dispatched (Research, Red-team A/B/C, Steel-man per Clause #11 §Dispatch shape; then Demand Archaeologist, Gap Scout, Pivot Architect under a generative extension the operator requested). Artifacts: `plans/ideation-dashero.md` (gate artifact), `plans/design-canon-notes.md`, `plans/brainstorm-summary.md` (plain-language writeup), `plans/outreach-draft.md` (the KC-14 test). `CLAUDE.md` gained a permanent plain-language rule after operator feedback.

**Carry-over slots:** none. No build slots were dispatched this session.

**Open blockers (must resolve before Wave 0):**
- **No confirmed buyer.** KC-14 is the binding gate. Q-26 ("how do the first 40 customers find you") was answered "I don't know yet" and remains unanswered.
- **KC-15 unrun** — whether DashThis or AgencyAnalytics already deliver flat-rate per-client fan-out with branding. AgencyAnalytics is confirmed to support Google Sheets as a source, which already narrows the wedge from ~16x to ~4x.
- **The name must change.** `DASHERO` is a registered EUIPO word mark (018457439, Dashero S.L.) in class 42 across 29 territories; `dashero.com` is owned and parked for sale. KC-12.
- **KC-1 and KC-9 unresolved** — whether a `drive.file` grant survives unattended server-side re-reads, and whether snapshot persistence is permitted under Google APIs ToS §5.e. Both were deleted by the add-on shape and reintroduced by the fan-out shape.
- Stack placeholders in `.orchestrator/agents/*.md` remain unfilled. A stack decision is recorded in the brief's §Handoff but is contingent on KC-14 clearing.

**Next required activities (in order):**
1. ⏳ **KC-15** — one hour. Falsifies the recommendation if an incumbent under $100/mo already sells branded per-recipient fan-out.
2. ⏳ **KC-14** — the outreach test in `plans/outreach-draft.md`. ~50 contacts, ≥5 committing to pay by 2026-09-12. **No code before this clears.**
3. ⏳ **KC-12** — settle the name and domain before any branding spend.
4. ⏳ **KC-1** — one-day `drive.file` persistence spike (only if KC-14 clears).
5. ⏳ If KC-14 clears: write `plans/feature-p1-<slug>.md` from `.orchestrator/templates/phase-spec.md`, fill the agent placeholders, then Wave 0 contract freeze.
6. ⏳ If KC-14 fails: record NO-GO in the brief's verdict section with the operator's reasoning, per Clause #11 §Doesn't apply to.

**Operating mode:** **ACTIVE** — required. New phase boundary, new contract surfaces, first-of-class everything, and no filed issues exist. DEGRADED is unreachable on this project until at least one phase has shipped.

**Throughput mode:** **serial** — `plans/velocity.json` has zero entries, so no class anchor has n≥3. Clause #10 parallel-by-default does not apply yet.

---

## Recent session history (rolling window of last 5 sessions)

| Session | Phase / Wave | Mode | PRs | Notes |
|---|---|---|---|---|
| S0 | — / setup | n/a | 0 | Vendored agentwaves @ `ff074c9` as `.orchestrator/`; seeded `plans/`; wrote `CLAUDE.md`. No product work. |
| S1 | — / Wave -1 | ACTIVE | 0 | Adversarial ideation under Clause #11. 8 agents. Gate exit 0. Verdict RESHAPE (product-level); original spec ranked last of 8. Wave 0 held behind KC-14 market test. Clause #11 §Dispatch shape found to lack a generative lens — amendment pending operator decision. |

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
