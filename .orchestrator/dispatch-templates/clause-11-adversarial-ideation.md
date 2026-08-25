# Clause #11 — Adversarial ideation gate (PERMANENT, greenfield only)

**Applies to:** the pre-Wave-0 ideation session for a **new project** — the session that decides what
the product is, before P1 has a phase spec. Not phase-boundary ideation (that keeps the lighter
PM/Designer sanity-check in `agents/pm-designer.md` §Phase sanity check).

**Enforcement:** hard gate. Wave 0 contract-freeze MUST NOT begin until
`scripts/check-ideation-gate.sh` exits 0. No bypass — same policy as the session-close guardrails.

---

## The five rules

### Rule 1 — Question-first. Never assume without asking.

Every input you don't have, you **ask the operator for**. You do not pick the convenient
interpretation and proceed. You do not infer intent from an adjacent statement. You do not
"reasonably assume" a target user, a price point, a distribution channel, a constraint, or a
success criterion.

Every assumption that survives the session goes in the **assumption register** with one of exactly
three dispositions:

| Disposition | Meaning | Required |
|---|---|---|
| `ASKED` | operator answered it | the answer, quoted |
| `RESEARCHED` | resolved by evidence, not opinion | a citation (§Rule 3) |
| `UNVERIFIED` | still an assumption | a falsifiable kill-criterion attached (§Rule 5) |

An assumption with no disposition is a gate failure. There is no fourth category and no
"self-evident" exemption.

Ask in batches, early, and ask more than feels polite. The failure mode this rule targets is not
rudeness — it's an ideation session that produces a confident plan resting on six unexamined
guesses, each individually plausible, jointly fatal.

### Rule 2 — Research before assuming.

Ordering is mandatory: **research → ask → assume**, never the reverse. Before you ask the operator a
question the public record can answer, go answer it. Before you log an `UNVERIFIED` assumption,
confirm it is genuinely unresearchable within the session's budget — not merely unresearched.

Minimum research surface before the gate opens:
- Does this already exist? Name the incumbents and near-substitutes, or state that a search was run
  and found none (with the queries used).
- What happened to prior attempts at the same idea? Dead products are the cheapest available data.
- What do the platform/API/regulatory dependencies actually permit? Read the terms, not a summary of
  them.

### Rule 3 — Show data, don't tell.

Every material claim carries a citation or a number with provenance. A claim is material if the
plan changes when it's false.

Banned, and treated as a gate failure:
- Unsourced market sizing ("this is a $X billion market").
- Unsourced demand claims ("users want", "people struggle with", "there's clearly a need").
- A number without a link, a date, and a method.
- A competitor summary written from memory rather than from their live pricing/docs page.

Prefer primary sources: the actual pricing page, the actual API docs, the actual filing, the actual
changelog. Cite secondary sources as secondary. Where no data exists, **say so explicitly** — "no
public data found; this is unverified" is a legitimate and valuable finding. Fabricating or
estimating a figure to fill the gap is the failure this rule exists to prevent.

### Rule 4 — Argue both sides, with symmetric rigor.

**The case against comes first and must be genuinely adversarial.** Minimum five distinct failure
modes, drawn from at least four of these categories:

| Category | The question it answers |
|---|---|
| Demand | Does anyone actually want this enough to change behavior? |
| Distribution | How does it reach users, and what does that cost? |
| Technical | What makes this hard or impossible to build well? |
| Economic | Do the unit economics survive contact with real costs? |
| Competitive | What does an incumbent do the week after this works? |
| Dependency / regulatory | What third party or rule can end this unilaterally? |
| Operator | Does the person building this have the time, skills, and access it requires? |

Each failure mode needs a **concrete mechanism** and a **leading indicator** — the observable signal
that this failure is starting to happen. Generic risk-listing ("it might not scale", "adoption could
be slow") is not a failure mode and does not count toward the five.

**The case for gets the same rigor** — it is not a token counterweight appended to soften the
critique. Minimum three reasons this works, each with its own evidence and its own mechanism. An
honest ideation session can and should conclude that a critiqued idea is still worth building.

The output is a comparison, not a verdict looking for support.

### Rule 5 — Falsifiable kill criteria, then a verdict.

Name the conditions under which this project should be **stopped**, in advance, while stopping is
still cheap. Each kill criterion must be falsifiable and observable — a threshold, a date, a
measurable signal. "If users don't like it" is not a kill criterion. "If fewer than 5 of the first
30 people we show it to complete the core flow unprompted, stop" is.

Every `UNVERIFIED` assumption from Rule 1 must map to at least one kill criterion.

Close with a verdict — `GO`, `NO-GO`, or `RESHAPE` (with what changes) — and the single strongest
argument against your own verdict.

---

## Body (paste verbatim into pre-Wave-0 discovery/critique dispatch briefs)

> **Clause #11 — Adversarial ideation (PERMANENT).** This is a greenfield ideation dispatch. You are
> being asked to stress-test an idea, not to validate it.
>
> 1. **Never assume without asking.** Any input you lack, ask the operator for. Do not infer it, do
>    not pick the convenient reading, do not proceed on "reasonable assumption." Every surviving
>    assumption must be labelled `ASKED` (quote the answer), `RESEARCHED` (cite the source), or
>    `UNVERIFIED` (attach a kill-criterion). No fourth category.
> 2. **Research before assuming.** If the public record can answer it, go answer it before you ask
>    or assume. Read primary sources — the actual pricing page, API docs, terms, filing.
> 3. **Show data, don't tell.** Every material claim carries a citation or a number with a link, a
>    date, and a method. Unsourced market sizing and unsourced demand claims are rejected outright.
>    "No public data found" is a legitimate finding; an invented estimate is not.
> 4. **Be extremely critical first.** Produce at least five distinct, specific failure modes across
>    at least four categories (demand / distribution / technical / economic / competitive /
>    dependency-regulatory / operator). Each needs a concrete mechanism and a leading indicator.
>    Generic risk-listing does not count. Then argue the other side with equal rigor: at least three
>    reasons this works, each with evidence and a mechanism.
> 5. **Falsifiable kill criteria.** Name in advance the observable thresholds at which this should
>    be stopped. Each unverified assumption maps to at least one. Close with `GO` / `NO-GO` /
>    `RESHAPE` and the strongest argument against your own verdict.
>
> Write your findings into `plans/ideation-<slug>.md` using the structure in
> `templates/ideation-brief.md`. `scripts/check-ideation-gate.sh` must exit 0 before Wave 0 begins.

---

## Dispatch shape

The orchestrator does not run this alone — a single voice arguing with itself converges too fast.
Dispatch in parallel (single message, multiple `Agent` tool_use blocks, per Clause #10's mechanics):

| Agent | Lens | Brief |
|---|---|---|
| Research | Prior art, incumbents, dependencies | Rule 2's minimum research surface. Returns citations, not opinions. |
| Red-team A | Demand + distribution | Why does nobody want this, and how does it fail to reach them? |
| Red-team B | Technical + dependency/regulatory | What makes this unbuildable, or killable by a third party? |
| Red-team C | Economic + competitive + operator | Where do the unit economics break, who crushes it, can this operator ship it? |
| Steel-man | The case for | Strongest honest case, same evidentiary standard. Dispatched *after* the red teams return, and must engage their findings rather than ignore them. |

The orchestrator synthesizes into `plans/ideation-<slug>.md`, takes the operator's answers to the
open questions, and runs the gate. Red-team agents that return nothing are a signal to re-dispatch
with a sharper brief, not a clean bill of health.

---

## Why permanent

**Provenance note — this clause differs from the others in this directory.** Clauses #3, #6, #9, and
#10 are retro-derived: each traces to a specific observed failure with a measured token cost. Clause
#11 is an **operator directive, adopted 2026-08-24**, and is forward-looking. It has no incident
behind it yet and carries no measured savings band. That is stated plainly rather than dressed up in
a fabricated retrospective — inventing provenance would violate the clause's own Rule 3.

The reasoning it encodes: agentwaves is a framework for executing a roadmap with high discipline.
Everything downstream of Wave 0 — contract freeze, issue decomposition, reviewer trios, guardrails —
optimizes for building the specified thing correctly. **None of it checks whether the specified
thing is worth building.** A protocol this good at execution is exactly the protocol that will
efficiently ship the wrong product for eight phases. The ideation gate is the only place that class
of error is cheap to catch, and the cost asymmetry is extreme: a session of adversarial questioning
against months of misdirected build capacity.

The clause also exists because the default failure mode of an eager agent is agreement. Asked to
brainstorm, an assistant reaches for enthusiasm and plausible-sounding support. Rules 1 and 4 exist
to make that behavior a gate failure rather than a pleasant conversation.

Revisit after the first two projects gate through it — if it produces ritual compliance rather than
real findings, tighten the specificity requirements rather than loosening the gate.

---

## Doesn't apply to

- Phase-boundary ideation on an existing project (use `agents/pm-designer.md` §Phase sanity check).
- Wave 1 build dispatches, reviewer dispatches, QA, docs — every other dispatch surface.
- Projects where the operator explicitly declares the idea already validated **and** records that
  declaration in the ideation brief's verdict section with their reasoning. The gate still runs; the
  operator's declaration is the evidence.

## Tracking

The orchestrator confirms in the Wave 0 contract-freeze PR body:

```markdown
- **Clause #11 (adversarial ideation gate):** ✅ `plans/ideation-<slug>.md` complete;
  `scripts/check-ideation-gate.sh` exit 0. Verdict: <GO | RESHAPE>. <N> failure modes logged,
  <M> unverified assumptions each mapped to a kill criterion.
```
