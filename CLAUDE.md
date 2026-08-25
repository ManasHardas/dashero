# dashero

This project runs under the **agentwaves** protocol, vendored at `.orchestrator/`.
Operating manual: `.orchestrator/agents/orchestrator.md`. Read it at the start of every working session.

Adapted from `.orchestrator/CLAUDE.md.snippet` with paths rewritten for the `.orchestrator/` vendoring layout. Provenance and local patches: `.orchestrator/VENDOR.md`.

---

## Session operating modes

**Read `plans/next-session.md` FIRST** at any session-start (Session Handoff Document — pre-rendered playbook by PM at prior session-close). Contains pre-rendered slot 1 dispatch brief, compressed priors digest, watchdog framing. If missing OR stale (older than the latest merged PR), fall back to `plans/wave-state.md` (authoritative state) + legacy session-start ritual (PM dispatch). SHD protocol saves 65-95k per session-start. See `.orchestrator/agents/pm.md` §Session Handoff Document protocol for the format.

**Two operating modes — ACTIVE (full PM discipline) vs DEGRADED (PM-skip):**

DEGRADED mode is allowed ONLY when ALL of:
- All planned slots are narrow-fix or sibling-shape (no first-of-class)
- All issues filed before session start (no orchestrator scope synthesis)
- No new contract artifacts (no new endpoints, tables, OpenAPI changes, migrations)
- Last session closed cleanly (no unresolved fix-cycle)

ACTIVE mode is REQUIRED if ANY of the above conditions fails. ACTIVE mode requires:
- Stage-2 PM dispatched at session-start + session-close (per `.orchestrator/agents/pm.md`)
- Wave 0.5 issue planning before any Wave 1 build dispatch (per `.orchestrator/agents/orchestrator.md` §Wave sequence)
- Dispatch briefs derived from FILED ISSUE BODIES, not orchestrator-synthesized memory

**Source:** retrospective from a real project where PM-skip mode was wrongly applied to a session introducing new pages with new state machines. The orchestrator-synthesized dispatch brief conflated already-shipped endpoints as "future-phase, disable with tooltip"; review agent fired 4 Blockers; ~68k fix-cycle tax incurred. **This rule is now permanent.**

**Current project status:** ACTIVE is forced and DEGRADED is unreachable until at least one phase has shipped. See `plans/wave-state.md`.

## Session-close guardrails

**`.orchestrator/scripts/check-session-close-guardrails.sh` MUST run before the chore-close commit.** Exit 1 = BLOCKER, stop and fix; exit 2 = WARN, acknowledge each warn-line in the chore-close commit body; exit 0 = clean, proceed. Enforces 17 invariants: velocity.json rollup completeness (one `pr_merge` row per build PR), wave-state.md currency, SHD presence for S<N+1>, capacity-log.md entry, clean working tree, clean worktrees, cc_session_id presence (when your harness exposes one), stale-branch cleanup, operating-mode + watchdog declarations in close commit, etc. Cost ~5s + ~200-300 tokens per session; +5-10k with GitHub API checks for issue/branch verification.

Catches the silent execution drift from non-negotiable spec invariants that is invisible during normal development — agents follow stale memory; the spec keeps living in the doc unaltered until someone runs a retrospective and notices the gap. **No bypass** — file an issue against the script if a check is wrong; do not skip the gate. See `.orchestrator/agents/orchestrator.md` §Session-close ritual + `.orchestrator/agents/pm.md` §Session close step 5.

**Local note:** `plans/wave-state.md` must carry a `(post-S<N>)` marker in its `## Current state` heading — check #2 auto-detects the session number from it. The upstream template writes `(session N status)`, which the guardrail does not match.

## Wave -1 — adversarial ideation gate (PERMANENT, greenfield only)

dashero has not run this yet, and **Wave 0 cannot begin until it has.**

The ideation session that decides what dashero is runs under Clause #11 (`.orchestrator/dispatch-templates/clause-11-adversarial-ideation.md`) and is **extremely critical by default**. Five rules:

1. **Never assume without asking.** Every input you lack, ask for. Every surviving assumption is labelled `ASKED` (quote the answer), `RESEARCHED` (cite the source), or `UNVERIFIED` (attach a falsifiable kill-criterion). No fourth category, no "self-evident" exemption. Ask in batches, and ask more than feels polite.
2. **Research before assuming.** Ordering is mandatory: research → ask → assume. Read primary sources — the actual pricing page, API docs, terms, filing — not a summary of them.
3. **Show data, don't tell.** Every material claim carries a citation or a number with a link, a date, and a method. Unsourced market sizing and unsourced demand claims are rejected outright. "No public data found" is a legitimate and valuable finding; an invented estimate to fill the gap is the failure this rule exists to prevent.
4. **Be extremely critical first, then argue the other side with equal rigor.** Minimum five *specific* failure modes across at least four categories (demand / distribution / technical / economic / competitive / dependency-regulatory / operator), each with a concrete mechanism and a leading indicator — generic risk-listing does not count. Then minimum three evidenced reasons it works, written after the critique and engaging with it.
5. **Falsifiable kill criteria, then a verdict.** Observable thresholds named in advance, while stopping is cheap. Close with `GO` / `NO-GO` / `RESHAPE` and the strongest argument against your own verdict.

Findings go in `plans/ideation-<slug>.md`, seeded from `.orchestrator/templates/ideation-brief.md`. Red-team and research agents are dispatched in parallel per the clause's §Dispatch shape, with the clause body pasted verbatim into each brief. **`.orchestrator/scripts/check-ideation-gate.sh` must exit 0 before Wave 0.** No bypass.

**What the gate does not do:** every check is structural. It confirms the reasoning was done, not that it was good — a brief can satisfy all nine checks and contain no genuine thought. A green gate is not validation, and treating it as such is the misuse it is most vulnerable to.

## Dispatch system — agentwaves only (PERMANENT)

**All subagent dispatch in this repo goes through the agentwaves wave protocol. No exceptions.**

Specifically forbidden: `superpowers:subagent-driven-development`, `superpowers:dispatching-parallel-agents`, and any ad-hoc "decompose this and fan out agents" improvisation. This is not an instruction to avoid subagents — subagents remain the execution model. What is forbidden is dispatching them outside the wave structure.

**Why.** Both systems dispatch subagents, but they constrain different things, and the harness's version silently voids the guarantees this protocol exists to provide. Superpowers decomposes in-context and dispatches from that decomposition; agentwaves requires every Wave 1 dispatch to reference a **filed GitHub issue** produced by Wave 0.5 planning — the orchestrator never synthesizes a dispatch brief from memory. Harness-native dispatch also bypasses the permanent dispatch-template clauses (#3, #6, HARD CONSTRAINT, close-keyword), the T-X file-lock disjointness gate, and the velocity/capacity accounting PM needs at session-close.

Parallelism comes from **Clause #10** — a single orchestrator message with multiple `Agent` tool_use blocks on disjoint T-X file-lock units — not from a parallel-dispatch skill.

Harness skills stay usable *inside* a wave where they don't displace protocol structure: `superpowers:brainstorming` for pre-Wave-0 ideation, TDD skills within a Wave 1 build slot. Per `.orchestrator/agents/orchestrator.md` §Meta-skill conflict carve-out: **in any conflict, the Wave protocol wins** — skip the skill for that session, never the protocol. If a skill auto-activates and begins decomposing or fanning out on its own schedule, stop and surface the conflict to the user.

## Direct-to-main policy

The orchestrator is the only agent that touches `main`, and only for the artifacts listed in `.orchestrator/agents/orchestrator.md` §Your authority (API specs, migrations, `plans/**`, `.github/**`, codegen output). **`scripts/`, `package.json`, and dev tooling are NOT on that list** — they are build-agent territory and go through branch + PR + reviewer dispatch like anything else, including mid-dogfood, including one-line fixes. See §Wave 3.5 Dogfood discipline.

## Project-tunable knobs (env vars)

Two env-var prefixes are recognized:

- **`AW_*`** — protocol-wide knobs that change orchestration behavior (e.g. `AW_CI_QUOTA_CONSTRAINED=1` activates the CI-quota-constrained operating sub-mode).
- **`GUARDRAIL_*`** — knobs specific to `.orchestrator/scripts/check-session-close-guardrails.sh`:
  - `GUARDRAIL_CC_SESSION_GATE=<N>` enables the cc_session_id invariant (check #7) from session N.
  - `GUARDRAIL_MAIN_CI_GATE=<N>` escalates check #18 (main CI green at session-close) from WARN to BLOCKER starting at session N. Default: WARN-only; sub-10s failures auto-classified as INFO (likely billing-block, not a real red).

See `.orchestrator/README.md` §Environment variables for the full table.
