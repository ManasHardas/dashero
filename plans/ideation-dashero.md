# Ideation brief — dashero

> **Gate artifact for Clause #11.** Wave 0 contract freeze cannot begin until
> `.orchestrator/scripts/check-ideation-gate.sh` exits 0 against this file.
>
> **Status: IN PROGRESS.** Sections below the question register are populated during synthesis,
> after the Wave -1 dispatch returns (Research, Design-canon, Red-team A/B/C, Steel-man).
> The gate is expected to fail until synthesis completes. That is correct behaviour, not a defect.

**Session:** S1 · **Date:** 2026-08-25 · **Operator:** Manas Hardas

**One-line thesis:** Connect one Google Sheet and get back a dashboard of automatically-inferred,
genuinely well-designed charts at a shareable URL in under a minute — where the creator refines the
charts by conversation and the recipient can ask questions of what the charts show.

---

## Open questions

Every question put to the operator, with their answer quoted. Clause #11 Rule 1 — ask more than
feels polite. 26 asked across three batches, all answered.

### Batch 1 — operator, demand, product shape, business model

- **Q-1:** Hours per week available, and over what horizon before you'd call it dead? Solo, or is
  anyone else building?
  **A:** "solo, i would give it 3-4 months until I see some revenue from it"
- **Q-2:** What is this for — a business, a portfolio/learning project, or a tool you personally want?
  **A:** "strictly to make money from it right now"
- **Q-3:** Monthly out-of-pocket ceiling for infra plus LLM calls before "permanently free for
  individuals" has to change?
  **A:** "I want to reframe the 'permanently free' claim. it will be free to connect 1 sheets and
  generate dashboards from it but after that everyone will have to pay."
- **Q-4:** Who is user #1 — someone specific with this problem today, or hypothetical?
  **A:** "hypothetical user. i think the demand exists but you will need to verify and confirm. at a
  previous company we were using a similar free tool which you could directly connect the database
  to."
- **Q-5:** What do they do right now instead, and what specifically is bad about it?
  **A:** "dashboards are created by every team in an org but there is a huge discrepancy in how. many
  mid to large orgs have big data teams that have set up data warehouses or data lakes in which data
  is organized for olap. Some enterprises are well organized enough to data marts for marketing,
  finance, hr, and other departments within the data warehouse itself. These orgs typically use large
  tools like microstrategy, tableau, etc. to generate dashboards. In smaller orgs data is scattered
  and not warehoused properly. More over finance, sales, marketing and other teams still need to
  create dashboards and what they default to is excel or google sheets both of which are really
  terrible to create interactive charts."
- **Q-6:** Which existing tools have you personally tried and rejected?
  **A:** "I've only tried Looker and Grafana."
- **Q-7:** Live-connected sheet (OAuth, re-reads on load) or one-time upload snapshot?
  **A:** "don't know yet"
- **Q-8:** Is the dashboard URL public by default?
  **A:** "not public by default. it is only visible to you and people in your orgs that the dashboard
  has been shared with."
- **Q-9:** What data scale — 500 rows or 5M rows?
  **A:** "More like 100M rows! it has to be insanely fast too"
- **Q-10:** Screenshot-quality static output, or live interactive dashboards people return to?
  **A:** "The live dashboards must have very beautiful charts."
- **Q-11:** Do you have a real enterprise contact who would pay, or is that segment hypothetical?
  **A:** "this segment is currently hypothetical."
- **Q-12:** What stops an enterprise from having ten employees each use ten free individual accounts?
  **A:** "nothing stops but each of the ten employees only get 1 sheet each and a different
  namespacae alltogehter."
- **Q-13:** Do you own `dashero.com`? Have you checked trademark conflicts?
  **A:** "no"
- **Q-14:** Any hard stack constraints — languages, hosting, existing accounts?
  **A:** "keep the stack as simple and local as possible. sqlite works perfectly fine"

### Batch 2 — resolving the contradictions surfaced by Batch 1

Batch 1 produced four contradictions: 100M rows is unreachable through a spreadsheet (Google Sheets
caps at 10M cells; Excel at 1,048,576 rows per worksheet); 100M-row OLAP contradicts the SQLite
preference; the org-sharing model contradicted both the per-person namespace model and the
frictionless-share pitch; and total scope exceeded a 3-4 month solo horizon.

- **Q-15:** Sheet-first (Product A) or warehouse-first (Product B)? "Both" is the answer that kills
  this.
  **A:** "lets go with A first just a google sheet connector"
- **Q-16:** Where do the 100M rows actually live — name the source system.
  **A:** "the 100M rows argument was for when we have db connectors"
- **Q-17:** "Insanely fast" as a number — p95 time to a rendered dashboard.
  **A:** "not sure" — resolved at Q-22.
- **Q-18:** Does v1 have a team/org concept, or single-user with unlisted share links?
  **A:** "lets begin with single user with unlisted share links. but there has to be a hook for people
  with whom the link has been shared to signup. like in built virality" — and later, "For the sharing
  model, make it such that in the future teams would share a namespace but I do agree immediately
  shareable is magical and should be preserved."
- **Q-19:** What do you charge for sheet #2? A dollar number.
  **A:** "I am thinking sheets 2-20 go for $25/m and 20+ sheets go for $50/m. if there is a better way
  to price this then let me know."
- **Q-20:** What revenue number in 3-4 months makes you continue rather than stop?
  **A:** "$1000 is my limit,I want to see at least 40 signups at $25 or 20 signups at $50."
- **Q-21:** Do you remember the name of the free DB-connected tool from your previous company?
  **A:** "I don't remember. You should regenerate scope from these clarifications."

### Batch 3 — architecture forks, cost ceiling, and the aesthetic bar

- **Q-22:** Latency target — proposed p95 under 1.5s to first rendered dashboard on a 50k-row sheet.
  **A:** "latency target is appropriate"
- **Q-23:** Does the viewer's AI see the whole sheet, or only the columns the creator charted?
  **A:** "the viewer only sees the charts not the actual data. we will sacrifice some capability to
  avoid leaks for now"
- **Q-24:** Who pays for viewer AI queries, and what is the hard cap on a free account?
  **A:** "for now I pay, hard cap $20"
- **Q-25:** Name 2-3 charts or dashboards in the wild that hit your "beautiful" bar.
  **A:** The operator answered with a canon rather than examples: "I will give you a list of books
  that are considered as the last word on infographics. Research them thoroughly. ... These set of
  premises will be your commandments to draw a map. I want you to know that there is a difference
  between what data is show versus how it is shown. Generate opinions on both of these from the
  books." Books named: *The Visual Display of Quantitative Information* (Tufte), *Designing with
  Data* (Suda), *Beautiful Evidence* (Tufte), *Visual Explanations* (Tufte), *Envisioning
  Information* (Tufte), *Design for Information* (Meirelles), *How to Draw Charts & Diagrams*
  (Robertson), *The Secret Language of Maps* (Carter), *Information Graphics* (Rendgen). Bar stated
  as: "We want visually stunning graphs and charts that tell a story. Just some bars or scatter plot
  on the x-y axis with colors and annotations just won't do. They need to tell a story."
- **Q-26:** How do the first 40 paying customers find out dashero exists?
  **A:** "I don't know yet."

### Additional operator directives captured outside the Q-numbering

- Two-sided AI is a requirement, not a nice-to-have: "I want a tool that is two sided i.e. the creator
  of the dashboard that can converse with the AI to improve charts and the end-user that can converse
  with the AI to ask questions off the data."
- The insight-extraction prompt is a first-class versioned artifact: "We will need to build it so that
  the prompt that is used to extract insights from a table is editable in the code base."

---

## Scope as regenerated from the Batch 2 and Batch 3 answers

Recorded here because it is what the Wave -1 dispatch was briefed against. It is a working scope,
not a committed one — the verdict below may reshape or reject it.

**In P1:** Google Sheets connector (single sheet). Column profiling and type inference. Chart
inference from inferred types. Dashboard rendered at a per-user namespaced URL. Unlisted share link.
Creator-side conversational chart refinement. Viewer-side conversational questioning restricted to
charted aggregates. A signup hook on the viewer path. A workspace record with exactly one member, so
that shared team namespaces are a later migration rather than a rewrite. The insight-extraction
prompt as a versioned file in the repository.

**Deliberately out of P1:** database connectors, warehouse sources, 100M-row scale, organisations,
roles and invitations, a public gallery, embedding, scheduled refresh, alerting.

**Risk ranking used to brief the red teams**, highest first: viewer-side AI usefulness and leak
surface; achieving the aesthetic bar solo with no designer; chart inference producing dashboards
that are not garbage on real-world messy sheets; distribution.

---

## Assumption register

Every assumption the plan rests on. Exactly one disposition each. Every `UNVERIFIED` row references
a kill criterion.

| # | Assumption | Disposition | Evidence / answer | Kill criterion |
|---|---|---|---|---|
| A-1 | The operator is solo with a 3-4 month horizon to first revenue | ASKED | Q-1 | — |
| A-2 | The goal is revenue, not learning or portfolio | ASKED | Q-2 | — |
| A-3 | P1 connects Google Sheets only; database connectors are deferred | ASKED | Q-15, Q-16 | — |
| A-4 | v1 is single-user with unlisted share links; teams deferred but not precluded | ASKED | Q-18 | — |
| A-5 | The viewer AI sees charted aggregates only, never raw rows | ASKED | Q-23 | — |
| A-6 | Total LLM spend is capped at $20/month, paid personally | ASKED | Q-24 | — |
| A-7 | Below $1000 MRR by roughly 2026-12-25 the project stops | ASKED | Q-20 | — |
| A-8 | Metabase X-ray already ships the auto-inferred-charts mechanic, free, under AGPL | RESEARCHED | E-1, 2026-08-25 | — |
| A-9 | Metabase's Google Sheets path is not free — it needs paid Cloud plus a storage add-on | RESEARCHED | E-2, 2026-08-25 | — |
| A-10 | Google shipped Sheets canvas (prompt to interactive dashboard, live sync) on 2026-08-10 | RESEARCHED | E-3, E-4, 2026-08-25 | — |
| A-11 | Sheets canvas excludes free gmail.com accounts, leaving that population addressable | RESEARCHED | E-3, 2026-08-25 | KC-3 |
| A-12 | The exact product ships today from at least two vendors, one at $0.99 per dashboard | RESEARCHED | E-5, E-6, 2026-08-25 | — |
| A-13 | Medium built and silently archived this literal spec (Charted, 2014-2018) | RESEARCHED | E-7, 2026-08-25 | — |
| A-14 | `drive.file` is non-sensitive: no CASA assessment, no sensitive-scope review | RESEARCHED | E-8, E-9, 2026-08-25 | — |
| A-15 | A `drive.file` grant persists for unattended server-side re-reads days later | UNVERIFIED | not confirmed from any primary source; the entire snapshot architecture rests on it | KC-1 |
| A-16 | The 100-user cap does not bind non-sensitive-scope apps in Published status | UNVERIFIED | Google's own two support pages contradict each other; queries logged in the Research return | KC-2 |
| A-17 | Sheets API allows 300 reads/min per project and 60/min per user, making read-on-load unviable | RESEARCHED | E-10, 2026-08-25 | — |
| A-18 | Storing parsed snapshots server-side is permitted despite Google APIs ToS section 5.e on caching | UNVERIFIED | Limited Use permits storage for user-facing features; the two clauses point in different directions and this is a question for counsel | KC-9 |
| A-19 | `DASHERO` is a registered EUIPO word mark in class 42 (software), owned by Dashero S.L. | RESEARCHED | E-11, 2026-08-25 | — |
| A-20 | Automatic table detection tops out near 79% F1 even with a fine-tuned frontier model | RESEARCHED | E-12, E-13, 2026-08-25 | KC-4 |
| A-21 | A confirm-the-shape step converts that 79% from a failure rate into a pre-fill rate | UNVERIFIED | reasoned; every serious data tool asks users to confirm shape, but not measured for this product | KC-4 |
| A-22 | Metric polarity cannot be inferred reliably from column names and fails silently | UNVERIFIED | Design-canon estimates a lexicon catches roughly 60%; this is a working assumption, not a measurement | KC-5 |
| A-23 | Vega-Lite is the only major chart library shipping a live JSON Schema for pre-render validation | RESEARCHED | E-14, 2026-08-25 | — |
| A-24 | LaTeX, matplotlib and ggplot2 are unviable as the interactive renderer; pgfplots suits paid PDF export | RESEARCHED | E-15, 2026-08-25 | — |
| A-25 | Paid LLM tiers are legally required; the Gemini free tier violates Google's own Workspace API policy | RESEARCHED | E-16, E-17, 2026-08-25 | — |
| A-26 | At Gemini Flash-Lite rates a viewer turn costs about $0.001, giving roughly 18,600 turns per $20 | RESEARCHED | E-18, 2026-08-25; token counts per turn are the analyst's estimates, not measurements | KC-6 |
| A-27 | Free-tier viewer AI is insolvent well below the user count needed for 40 payers | RESEARCHED | E-19, 2026-08-25 | KC-6 |
| A-28 | Paid-user gross margin at $25 is roughly 83% after Stripe fees and inference | RESEARCHED | E-20, 2026-08-25 | — |
| A-29 | Demand for a paid fix to chart aesthetics exists | UNVERIFIED | Q-4 answered "hypothetical"; two agents independently found no public data in either direction | KC-3 |
| A-30 | Dashboard creation is frequent enough for a second-sheet paywall to have a population | UNVERIFIED | no public data found on per-person dashboard creation frequency | KC-7 |
| A-31 | Some channel reaches 40 paying customers within the window | UNVERIFIED | Q-26 answered "I don't know yet"; channel-by-channel expected value modelled at roughly 4 | KC-8 |
| A-32 | The enterprise or team segment converts | UNVERIFIED | Q-11 answered "hypothetical"; no operator contact exists | KC-8 |
| A-33 | Embellished charts do not reduce comprehension and improve recall at 2-3 weeks | RESEARCHED | E-21, 2026-08-25 | — |
| A-34 | The scope as specified is roughly 2.5-3x the available time | UNVERIFIED | reasoned from a 13-item build inventory against a solo 3-4 month window | KC-10 |
| A-35 | No incumbent under $100/month already delivers flat-rate per-client fan-out with per-recipient branding | UNVERIFIED | AgencyAnalytics meters per client at $20 and Whatagraph starts near €699, but DashThis and Swydo were not tested for fan-out specifically | KC-15 |
| A-36 | Recurring money in this category is priced per client rather than per dashboard | RESEARCHED | E-53, E-54, E-55, 2026-08-25 | — |
| A-37 | One-off spreadsheet-dashboard build work clears at $10-125 against roughly 150 suppliers per live buyer | RESEARCHED | E-56, 2026-08-25 | — |
| A-38 | Parameterized fan-out is a recurring unmet need across unrelated verticals | RESEARCHED | E-57, six independent threads 2019-2026, 2026-08-25 | — |
| A-39 | Producers-for-hire will pay a subscription rather than continue building the workaround themselves | UNVERIFIED | the anchor thread shows an operator moving 80 clients from paid tooling onto free Looker Studio, which demonstrates price sensitivity rather than willingness to pay | KC-14 |
| A-40 | Fan-out can be scoped to a 6-7 week solo build by cutting the spec-builder UI, scheduled refresh, and auth beyond signed URLs | UNVERIFIED | an inventory estimate, not a measurement; the unscoped version was independently sized at 8-12 weeks | KC-14 |
| A-41 | N recipients cost one Sheets read because all slices render from a single snapshot, making the 300-reads-per-minute pool a non-issue | RESEARCHED | E-10 combined with the snapshot architecture; arithmetic is direct | — |

---

## Evidence

Primary sources first. Every row carries a link or an explicit negative result, with the date
accessed and what it establishes.

| # | Claim it supports | Source | Date | Type |
|---|---|---|---|---|
| E-1 | Metabase X-ray auto-generates dashboards with chart types inferred from field data types; free under AGPL | https://www.metabase.com/docs/latest/exploration-and-organization/x-rays | 2026-08-25 | primary |
| E-2 | Metabase's Google Sheets connector requires paid Cloud plus a storage add-on | https://www.metabase.com/product/google-sheets | 2026-08-25 | primary |
| E-3 | Google Sheets canvas turns a sheet into an interactive dashboard from a prompt; excludes free gmail.com accounts | https://workspaceupdates.googleblog.com/2026/08/use-google-sheets-canvas-to-visualize-data.html | 2026-08-25 | primary |
| E-4 | Sheets canvas shares like a regular sheet and syncs live | https://blog.google/products-and-platforms/products/workspace/sheets-canvas-for-google-sheets-spreadsheets/ | 2026-08-25 | primary |
| E-5 | VibeFactory ships sheet-to-AI-dashboard in about 60 seconds with a public share URL, from $0.99 | https://vibefactory.ai/google-sheets-dashboard-ai | 2026-08-25 | primary |
| E-6 | Queryless ships spreadsheet-to-dashboard in under 60 seconds with a live shareable URL | https://www.querylessai.com/ | 2026-08-25 | primary |
| E-7 | Medium's Charted did exactly this in 2014 and was archived 2018-11-14 with no announcement | https://github.com/charted-co/charted | 2026-08-25 | primary |
| E-8 | `drive.file` is non-sensitive; `drive.readonly` and `drive` are restricted | https://developers.google.com/workspace/drive/api/guides/api-specific-auth | 2026-08-25 | primary |
| E-9 | Restricted scopes require an annual third-party CASA security assessment | https://developers.google.com/identity/protocols/oauth2/production-readiness/restricted-scope-verification | 2026-08-25 | primary |
| E-10 | Sheets API allows 300 read requests per minute per project and 60 per minute per user; overage becomes billable later in 2026 | https://developers.google.com/workspace/sheets/api/limits | 2026-08-25 | primary |
| E-11 | DASHERO is a registered EUIPO word mark, number 018457439, classes 35/36/42, owner Dashero S.L. | https://euipo.europa.eu/trademark/data/EM500000018457439 | 2026-08-25 | primary |
| E-12 | TableSense reaches 91.3% recall at a 2-cell boundary tolerance, from 22,176 tables across 10,220 sheets | https://www.microsoft.com/en-us/research/wp-content/uploads/2019/01/TableSense_AAAI19.pdf | 2026-08-25 | primary |
| E-13 | At exact-boundary match, TableSense scores 66.6% F1 and a fine-tuned GPT-4 reaches 78.9% | https://arxiv.org/html/2407.09025v1 | 2026-08-25 | primary |
| E-14 | Vega-Lite ships a live draft-07 JSON Schema with 458 definitions, enabling pre-render validation | https://vega.github.io/schema/vega-lite/v6.json | 2026-08-25 | primary |
| E-15 | pgfplots' own documentation recommends externalizing figures because graphical LaTeX processing takes non-negligible time | https://tikz.dev/pgfplots/ | 2026-08-25 | primary |
| E-16 | Google's Workspace API policy prohibits using user data to create, train or improve an AI model, and prohibits human reading | https://developers.google.com/workspace/workspace-api-user-data-developer-policy | 2026-08-25 | primary |
| E-17 | The unpaid Gemini tier trains on submitted content and permits human review; paid tiers do not | https://ai.google.dev/gemini-api/terms | 2026-08-25 | primary |
| E-18 | Gemini 3.1 Flash-Lite is priced at $0.25 per MTok input and $1.50 output | https://ai.google.dev/gemini-api/docs/pricing | 2026-08-25 | primary |
| E-19 | Anthropic per-token pricing used for the higher-cost sensitivity case | https://platform.claude.com/docs/en/about-claude/pricing | 2026-08-25 | primary |
| E-20 | Stripe charges 2.9% plus $0.30 per successful domestic card transaction | https://stripe.com/pricing | 2026-08-25 | primary |
| E-21 | Bateman et al. (CHI 2010) found embellished charts caused no comprehension loss and significantly better recall at 2-3 weeks | https://dl.acm.org/doi/10.1145/1753326.1753716 | 2026-08-25 | primary |
| E-22 | Freemium converts at roughly 5 paying customers per 1,000 visitors across 200 B2B products | https://chartmogul.com/reports/saas-conversion-report/ | 2026-08-25 | primary |
| E-23 | Product Hunt features roughly 10% of launches; non-featured launches yield 100-500 visitors and 1-15 signups | https://www.shno.co/marketing-statistics/product-hunt-launch-statistics | 2026-08-25 | secondary |
| E-24 | SMB and prosumer SaaS logo churn runs 3-5% monthly across a 939-company dataset | https://optif.ai/learn/questions/b2b-saas-churn-rate-benchmark/ | 2026-08-25 | secondary |
| E-25 | Spreadsheet.com shut down with over 1,000 paying organizations, citing inability to achieve venture-scale growth | https://techstartups.com/2024/02/24/spreadsheet-com-is-shutting-down-after-burning-through-5-5-millions-of-investors-money/ | 2026-08-25 | secondary |
| E-26 | Google announced Fusion Tables' shutdown in December 2018 and terminated it on 2019-12-03 | https://workspaceupdates.googleblog.com/2018/12/google-fusion-tables-to-be-shut-down-on.html | 2026-08-25 | primary |
| E-27 | Chartio had 280,000 users and 10.5 million charts, was acquired by Atlassian in 2021 and killed in 2022 | https://www.atlassian.com/blog/announcements/atlassian-acquires-chartio | 2026-08-25 | primary |
| E-28 | Infogram gates privacy controls and live data connections behind $19-67/month while giving charts away free | https://infogram.com/pricing | 2026-08-25 | primary |
| E-29 | Datawrapper's free tier places no limit on chart views or reader access | https://www.datawrapper.de/pricing | 2026-08-25 | primary |
| E-30 | Bricks charges $25 per seat per month for AI dashboards, AI visualization and AI chat over data | https://www.thebricks.com/pricing | 2026-08-25 | primary |
| E-31 | Geckoboard charges $79/month for 2 dashboards and 1 editor with unlimited viewers | https://www.geckoboard.com/pricing/ | 2026-08-25 | primary |
| E-32 | Indirect prompt injection ranks first in the OWASP Top 10 for LLM Applications 2025 | https://www.microsoft.com/en-us/msrc/blog/2025/07/how-microsoft-defends-against-indirect-prompt-injection-attacks | 2026-08-25 | secondary |
| E-33 | Disclosure control requires secondary suppression, not just small-cell suppression, to defeat differencing attacks | https://docs.opensafely.org/outputs/sdc/ | 2026-08-25 | secondary |
| E-34 | GDPR Article 28 makes a written DPA mandatory and holds the processor fully liable for its sub-processors | https://sprinto.com/gdpr/article-28/ | 2026-08-25 | secondary |
| E-35 | Anthropic's commercial terms state that Anthropic may not train models on Customer Content | https://www.anthropic.com/legal/commercial-terms | 2026-08-25 | primary |
| E-36 | No public data found on how often an individual creates a new dashboard. Queries run: "how often" create new dashboard frequency knowledge workers survey; dashboard creation frequency per user per year business intelligence | searched 2026-08-25 — no public data found in either direction | 2026-08-25 | negative |
| E-37 | No credible public demand data found for the Google Sheets dashboard category. Queries run: "google sheets dashboard" search volume keyword demand data SEO; indie hacker solo SaaS dashboard tool revenue MRR google sheets analytics microsaas | searched 2026-08-25 — no public data found; all results were listicles citing uncited figures | 2026-08-25 | negative |
| E-38 | Trademark status of DASHERO in the United States could not be established directly. USPTO TESS returned S3 errors and a JavaScript-only interface; TMview's federated USPTO feed shows no live US mark | searched 2026-08-25 — no public data found via direct USPTO query | 2026-08-25 | negative |
| E-39 | The asking price for dashero.com could not be retrieved; the Atom marketplace listing returns HTTP 403 to automated fetch | searched 2026-08-25 — no public data found | 2026-08-25 | negative |
| E-40 | Robertson's *How to Draw Charts and Diagrams* has essentially no online full text. Six query formulations returned catalogue metadata and bare citations only; not in Internet Archive or Open Library full-text | searched 2026-08-25 — no public data found | 2026-08-25 | negative |
| E-41 | ChartExpo, a Google Sheets add-on selling only better chart types and storytelling presentation, charges $10 per user per month | https://chartexpo.com/pricing | 2026-08-25 | primary |
| E-42 | ChartExpo positions explicitly on storytelling and claims over 700,000 users — an unaudited vendor self-claim counting users, not payers | https://chartexpo.com/tools/google-sheets | 2026-08-25 | primary page, vendor self-claim |
| E-43 | Canva acquired Flourish in February 2022; roughly 800,000 users on about $1M raised, with all 44 employees retained | https://techcrunch.com/2022/02/02/canva-acquires-flourish-in-mission-to-tell-better-stories-with-data/ | 2026-08-25 | secondary |
| E-44 | Datawrapper is bootstrapped, founded 2011, at roughly $3.2M ARR with about 29 employees — aggregator-sourced, indicative only | https://getlatka.com/companies/datawrapper.de | 2026-08-25 | secondary, low confidence |
| E-45 | MicroConf's 2024 State of Independent SaaS (about 700 usable responses) puts 38% of products under $10k annual revenue and 28% between $10k and $50k | https://www.startupsfortherestofus.com/episodes/episode-721-7-key-takeaways-from-the-2024-state-of-independent-saas-report | 2026-08-25 | secondary, primary report gated |
| E-46 | Datawrapper requires chart titles to be written by hand in the Annotate tab, while its own guidance calls the title one of the two most important elements | https://academy.datawrapper.de/article/336-annotate-tab | 2026-08-25 | primary |
| E-47 | Datawrapper's own writing states the title is the first or second thing readers see and is very important to comprehension | https://www.datawrapper.de/blog/text-in-data-visualizations | 2026-08-25 | primary |
| E-48 | Power BI's Smart Narrative produces a separate summary text visual, not an auto-generated chart headline | https://learn.microsoft.com/en-us/power-bi/visuals/power-bi-visualization-smart-narrative | 2026-08-25 | primary |
| E-49 | Tableau Data Stories, the closest prior art to auto-generated narrative, was retired in January 2025 (2025.1) | https://help.tableau.com/current/pro/desktop/en-us/data_stories.htm | 2026-08-25 | primary, negative for FOR-4 |
| E-50 | Google Workspace Marketplace add-ons reach real scale — Sheetgo lists 5M+ installs, GPT for Sheets and Docs 7M+ — but both run inside Sheets, which a hosted external app does not | https://workspace.google.com/marketplace/app/gpt_for_sheets_and_docs/677318054654 | 2026-08-25 | primary |
| E-51 | No public data found on the share of Google Workspace paying organisations on Business Starter versus Standard or Plus. Queries run: google workspace business starter vs standard share of customers; workspace tier distribution paying seats | searched 2026-08-25 — no public data found | 2026-08-25 | negative |
| E-52 | Whether the 100-new-user cap binds Published apps using only non-sensitive scopes could not be resolved; two Google pages were fetched and neither settles it | https://support.google.com/cloud/answer/13463073 | 2026-08-25 | negative |
| E-53 | AgencyAnalytics prices client reporting at $20 per client per month, billed annually, with unlimited dashboards — revealing a per-client rather than per-dashboard meter | https://agencyanalytics.com/pricing | 2026-08-25 | primary |
| E-54 | DashThis charges $44/month annual or $54 monthly for 3 dashboards and 15 sources | https://dashthis.com/pricing/ | 2026-08-25 | primary |
| E-55 | Swydo charges €69/month including 10 sources, then €4.50 per additional source, working out near €12.15 per client per month | https://www.swydo.com/pricing/ | 2026-08-25 | primary |
| E-56 | PeoplePerHour lists 300+ freelancers across 16 pages for Google Sheets dashboard work against roughly two live buyer projects; one $150-200 project drew 39 proposals and a $34/hr posting drew 50; fixed-price offers cluster $10-125 | https://www.peopleperhour.com/hire-freelancers/google+sheets+dashboard | 2026-08-25 | primary |
| E-57 | Parameterized fan-out is described as an unmet need across unrelated verticals — a PPC agency with roughly 100 clients whose templates are unmanageable, and a sole analyst with 50+ production lines sharing one KPI layout | https://www.reddit.com/r/BusinessIntelligence/comments/1u5bgdc/best_way_to_manage_50_production_line_dashboards/ | 2026-08-25 | primary |
| E-58 | Metabase's Google Sheets integration requires Metabase Cloud plus the Cloud Storage add-on, and self-hosted instances cannot use it — a structurally protected gap, with the OSS request open since 2018-07-06 | https://www.metabase.com/docs/latest/cloud/google-sheets | 2026-08-25 | primary |
| E-59 | Datawrapper's pricing page names dashboards, live data connections and scheduled refresh on no tier, and paywalls PDF and SVG export behind Pro | https://www.datawrapper.de/pricing | 2026-08-25 | primary |
| E-60 | Metabase's public roadmap lists dashboard invites for external sharing and PDF attachments in subscriptions as currently in build, closing two gaps that otherwise looked open | https://www.metabase.com/roadmap | 2026-08-25 | primary |
| E-61 | Operators reverse-proxy Metabase behind nginx basic-auth to fake per-client passwords, a workaround recommended by maintainers on the seven-year-old external-sharing issue | https://github.com/metabase/metabase/issues/9978 | 2026-08-25 | primary |
| E-62 | No venue was found where twenty SMB operators with one recurring report are reachable in a week, and targeted searches for nonprofit, church, club and league buyers returned nothing. Queries logged in the Demand Archaeologist return | searched 2026-08-25 — no public data found | 2026-08-25 | negative |
| E-63 | Google Workspace Marketplace shows Awesome Table, which turns a Sheet into a shareable view, at 13M+ installs — the largest figure found and the least trustworthy, since counts are cumulative installs with undocumented methodology | https://workspace.google.com/marketplace/app/awesome_table/56088344336 | 2026-08-25 | primary, low confidence |
| E-64 | An add-on shipping approximately the auto-insight product concept, "AI Insights for Google Sheets", shows 24 installs — a marketplace listing is not distribution | https://workspace.google.com/marketplace/search/AI%20insights | 2026-08-25 | negative |
| E-65 | All fourteen software-review platforms approached (G2, Capterra, TrustRadius, GetApp, Gartner Peer Insights, Trustpilot and others) returned HTTP 403 to automated access, so the session holds no paying-reviewer sentiment data at all | attempted 2026-08-25 — no public data found, every platform blocked automated access | 2026-08-25 | negative |

### Prior art / incumbents

| Product | What it does | Pricing | Still alive? | Source |
|---|---|---|---|---|
| Metabase X-ray | Point at a table, get auto-generated charts inferred from field types | Free (AGPL); Sheets path needs paid Cloud from $90/mo | Yes | https://www.metabase.com/pricing |
| Google Sheets canvas | Prompt to interactive dashboard, live sync, shares like a sheet | Bundled in Workspace Business/Enterprise and AI Pro/Ultra; not free gmail | Yes, since 2026-08-10 | https://workspaceupdates.googleblog.com/2026/08/use-google-sheets-canvas-to-visualize-data.html |
| Google Looker Studio | Free BI with a native Sheets connector and public sharing | Free; Pro $9/user/mo | Yes | https://coefficient.io/is-looker-studio-free |
| VibeFactory | Sheet to AI dashboard in about 60 seconds, public URL, no viewer login | From $0.99 per dashboard | Yes | https://vibefactory.ai/google-sheets-dashboard-ai |
| Queryless | Spreadsheets to auto-wrangled dashboard in under 60 seconds, live URL | Not published | Yes | https://www.querylessai.com/ |
| Bricks | AI spreadsheet with AI dashboards, visualization and chat over data | Free (20 AI msgs); $25/seat; $100/seat | Yes | https://www.thebricks.com/pricing |
| Datawrapper | Beauty-first charts, live Sheets link, suggests chart type | Free with attribution; $21/user; $39 | Yes | https://www.datawrapper.de/pricing |
| Flourish | Story-driven visualization, live Sheets updates on paid tiers | Free with attribution; paid via Canva | Yes, owned by Canva | https://flourish.studio/pricing/ |
| Infogram | Charts and dashboards; privacy and live data are paid | Free; $19; $67; $149 | Yes, Prezi subsidiary | https://infogram.com/pricing |
| Geckoboard | Dashboards with Sheets on all plans, unlimited viewers | $79; $319 | Yes | https://www.geckoboard.com/pricing/ |
| Charted (Medium) | Paste a Sheets or CSV URL, get an auto-generated shareable chart, refetched every 30 min | Free | **Archived 2018-11-14, no announcement** | https://github.com/charted-co/charted |
| Google Fusion Tables | Upload data, get auto maps, charts and tables, embeddable | Free | **Dead 2019-12-03** | https://workspaceupdates.googleblog.com/2018/12/google-fusion-tables-to-be-shut-down-on.html |
| Chartio | Cloud BI, 280k users, 10.5M charts | Paid | **Dead 2022-03-01** after Atlassian acqui-hire | https://www.atlassian.com/blog/announcements/atlassian-acquires-chartio |
| Plotly Chart Studio | Hosted charts with public URLs | Free and paid | **Closed 2025-10-31** | https://plotly.com/chart-studio-updates/ |
| Spreadsheet.com | Spreadsheet to no-code apps; $5.5M seed, 170k users | Paid | **Dead 2024-05-31** with 1,000+ paying orgs | https://techstartups.com/2024/02/24/spreadsheet-com-is-shutting-down-after-burning-through-5-5-millions-of-investors-money/ |
| Silk | Spreadsheet to an auto interactive site of charts | Free | **Dead**, Palantir acqui-hire 2016 | https://techcrunch.com/2016/08/10/palantir-acquires-data-visualization-startup-silk/ |

**The pattern across the graveyard, and it is not what one would expect:** no dead product in this
list died of ugly charts. Four mechanisms recur — the category behaves as a feature rather than a
company (every exit is an acqui-hire and the acquirer kills the product); even the platform owners
abandon it (Google built and killed both Fusion Tables and Tables; Medium built and archived
Charted; Plotly ran Chart Studio for a decade and closed it); platform dependency is a fired risk
rather than a theoretical one (the Sheets API v3 turndown broke every tool built on it); and
willingness-to-pay concentrates in privacy, live refresh and connectors rather than aesthetics
(E-28). One asymmetry runs in the operator's favour: venture-scale growth is not the bar here.
Spreadsheet.com's 1,000 paying organisations killed a company that had raised $5.5M and would be an
extraordinary outcome for one person.

### Dependency + regulatory surface

- **Google OAuth scopes** — `drive.file` is non-sensitive and Google-recommended, requiring no
  verification, no CASA assessment and no annual recertification. `spreadsheets.readonly` is
  sensitive (verification plus a permanent 100-new-user cap). `drive.readonly` and `drive` are
  restricted (CASA, priced by third-party assessors between roughly $540 and $8,000 per year
  depending on tier and assessor, with sources disagreeing). Architecture consequence: Google Picker
  plus `drive.file` only, decided in Wave 0, never retrofitted. Cost of that path: dashero can never
  list a user's spreadsheets, never auto-discover, never build a file browser. Every connection is a
  Picker flow, permanently. (E-8, E-9, accessed 2026-08-25)
- **Sheets API quota** — 300 reads/min per project across all customers combined, 60/min per user.
  Read-on-load is unviable at any real share volume. Overage is planned to become billable to the
  Cloud account later in 2026 with at least 90 days' notice, at prices not yet published. (E-10,
  accessed 2026-08-25)
- **Google APIs ToS section 5.e** forbids keeping cached copies longer than the cache header permits,
  while the Workspace Limited Use policy permits storing data to provide user-facing features. These
  point in different directions and the snapshot architecture sits between them. (A-18, KC-9)
- **Workspace API user data policy** — prohibits using Workspace data to create, train or improve an
  AI model, and prohibits human reading of user data absent documented explicit consent. Two
  consequences: the unpaid Gemini tier is legally unusable because it trains and human-reviews, and
  **the operator may not read a customer's sheet to debug it** — while data-shape bugs are precisely
  the ones only diagnosable by looking at the data. (E-16, E-17, accessed 2026-08-25)
- **Anthropic commercial terms** state that Anthropic may not train models on Customer Content,
  satisfying the Workspace constraint on the sub-processor side. (E-35, accessed 2026-08-25)
- **GDPR Article 28** — dashero is a processor and its users are controllers. A written DPA is
  mandatory, the LLM provider becomes a disclosed sub-processor requiring back-to-back terms, and the
  processor carries full liability for the sub-processor's failures. Sole-trader scale confers no
  exemption. The aggregates-only viewer design genuinely reduces this surface. (E-34, accessed
  2026-08-25)
- **Trademark** — `DASHERO` is a registered EUIPO word mark in class 42 (software and SaaS) across 29
  territories, owned by Dashero S.L. A US mark could not be confirmed either way by direct query.
  (E-11, E-38, accessed 2026-08-25)

---

## The case against

Twelve failure modes across seven categories. Each carries a concrete mechanism and an observable
leading indicator.

### FM-1 — Google shipped the core mechanic natively, twelve days before this session · *competitive*
**Mechanism:** Sheets canvas turns a spreadsheet into an interactive dashboard from one plain-English prompt, syncs live with the source data, and shares like any sheet. It sits inside the tool the user already has open, requires no OAuth grant, no new account, no new URL and no procurement. dashero's differentiator collapses to "but mine are prettier" — a claim the user cannot evaluate before signing up, competing against zero switching cost. Google iterates monthly and the differentiator narrows on their schedule, not the operator's.
**Leading indicator:** In user interviews, the response to a description of dashero is "isn't that what canvas does?" Or any Google Workspace release note extending canvas to free and Individual tiers.
**Evidence:** E-3, E-4. Partly defused: canvas is tier-gated away from free gmail.com accounts, which is exactly the under-resourced small-org population the operator's Q-5 hypothesis names.

### FM-2 — The paywall fires on frequency, but the need is episodic · *demand*
**Mechanism:** The claimed value is aesthetic, but the free-to-paid trigger is the second connected sheet, which is a frequency event. A small-org finance or marketing person builds a dashboard when a reporting need is created, then maintains it by adding rows to the same sheet — that is the free tier, forever. The user who genuinely needs sheets 2 through 20 is doing multi-source reporting, and that person is not the "my charts are ugly" persona at all. A recurring price is attached to an episodic job, and the aesthetic value is consumed once, at creation.
**Leading indicator:** Median days to second dashboard among signups exceeding 45 days; or fewer than 25% of activated free users ever creating a second artifact; or month-2 login rate below 30%.
**Evidence:** E-36 — no public data found in either direction on dashboard creation frequency. This failure mode is a reasoned argument resting on an unmeasured assumption, and it is stated as such.

### FM-3 — The funnel does not close arithmetically under any sourced channel combination · *distribution*
**Mechanism:** 40 payers requires roughly 8,000 visitors at established-product benchmark rates and closer to 16,000 at realistic new-product rates. Working channel by channel at sourced yields — Product Hunt at a 10% feature rate, Show HN at a roughly 90% failure rate, SEO taking 6-12 months to compound against a window of 4, no identified community watering hole, and a Marketplace that ranks new listings last — expected value is approximately 4 paying customers, with an optimistic case of about 16 that requires winning two separate 10% lotteries. The $1,000 budget buys 8-13 customers at benchmark CPA while exhausting the entire runway.
**Leading indicator:** Week-4 traffic under 200 unique visitors per week, meaning launch-spike channels have exhausted and no compounding channel has started.
**Evidence:** E-22, E-23. The arithmetic is sound; its weakness is that benchmark rates are averages over undifferentiated products with a documented 10x spread between top and bottom quintile.

### FM-4 — The viral loop is structurally impossible for this content type · *distribution*
**Mechanism:** Products with working viral loops are inherently multi-player, and their viewers hold a symmetric latent need — a Loom viewer also wants to send videos. A dashboard viewer is a boss or a client looking at someone else's numbers; their reaction concerns the numbers, not a desire for a chart tool. The content is private business data, so the creator throttles the loop deliberately. And a converted viral signup lands on a 1-sheet free tier that covers their entire need, so the loop acquires users who structurally cannot become customers while burning inference cost on them.
**Leading indicator:** Referral-attributed signups below 1% of unique shared-link viewers after 500 viewers; or mean unique viewers per shared link below 3.
**Evidence:** Reasoned argument. Supporting comparables exist for products where the loop does work, but no data was found for dashboard-shaped content specifically.

### FM-5 — Table detection and type inference fail silently on real spreadsheets · *technical*
**Mechanism:** Real sheets carry headers below row 1, multiple independent tables per tab, blank spacer rows, merged cells, totals rows interleaved with data, string dates in mixed formats, numbers stored as text with currency symbols, and mixed types within a column. The inference layer picks an answer with no confidence signal and renders a polished chart. A wrong inference and a right one produce identical logs. The user cannot distinguish them without re-reading their own data, which is the exact work the product promised to remove — and by then the link is already shared.
**Leading indicator:** Above 25% of generated dashboards having a chart deleted, regenerated, or a column type manually overridden in the first session.
**Evidence:** E-12, E-13. Substantially defused by the confirm-the-shape reframe (A-21): those benchmarks measure fully automatic detection, and 79% is an excellent pre-fill rate for a step the user confirms.

### FM-6 — Free-tier viewer AI is insolvent, and success accelerates the failure · *economic*
**Mechanism:** The viewer AI endpoint is reachable by unauthenticated strangers holding an unlisted link. Cost scales with reach, and reach is precisely what the virality goal maximises. One dashboard reaching 500 viewers who ask 3 questions each costs $11.25 on a mid-priced model and $22.50 on a premium one — more than half or all of the monthly cap, from a single free user. On the cheapest viable model a mildly viral dashboard at 10,000 views and one question each still costs $10.75. The growth mechanism and the cost structure are the same mechanism pointed in opposite directions, so the AI goes dark on the dashboard receiving the most attention, in front of the largest audience the product has ever had. Unlisted is not secret: URLs leak through referrers, Slack unfurls and scraping, making this also a free LLM proxy for any scripted actor.
**Leading indicator:** Any single share link generating more than 200 AI turns in 24 hours; or any day's spend exceeding $1.50; or cost per active dashboard exceeding $0.30/month.
**Evidence:** E-18, E-19. Arithmetic shown in the agent returns; token counts per turn are estimates pending measurement (KC-6).

### FM-7 — The pricing axis is orthogonal to both cost and value · *economic*
**Mechanism:** Sheets are not the cost driver; AI turns and viewer traffic are. A customer with 1 sheet and 10,000 viewers costs real money and pays nothing; a customer with 19 idle sheets costs nothing and pays $25. The meter is decoupled from COGS and from willingness-to-pay in the same design. Worse, $25 spanning sheets 2 through 20 is a 20x usage range at one price, so the best and marginal accounts pay identically and expansion revenue is structurally zero. Every comparable product meters the thing that costs money.
**Leading indicator:** LLM cost per paying account varying by more than 5x across the paid base; top-decile accounts by sheet count showing the same ARPU as median accounts.
**Evidence:** E-28, E-29, E-30, E-31 — comparable products meter AI credits, dashboards, editors or monthly active users, and give viewers away.

### FM-8 — Sheets API project-wide quota caps total product scale from outside · *dependency/regulatory*
**Mechanism:** 300 reads per minute applies to the entire product across every customer, not per user. Read-on-load dies immediately: 500 people opening one shared dashboard in a minute is 500 reads against a 300 ceiling, and because reads execute under the creator's identity it also breaches the 60/min per-user cap at viewer 61. A background-sync architecture survives but is still bounded by sync interval. Quota increases can be requested but approval is not guaranteed, and overage is planned to become billable later in 2026 at prices not yet published — an unbudgeted cost line landing inside the runway.
**Leading indicator:** HTTP 429 responses above 0.5% of sync attempts; or publication of Google's 2026 quota billing schedule.
**Evidence:** E-10.

### FM-9 — Polarity cannot be inferred, and fails silently in the direction that destroys trust · *technical*
**Mechanism:** Whether "up" is good is not a property of the data; it is a property of the domain. Churn up is bad, revenue up is good, headcount is ambiguous. A column-name lexicon catches roughly 60% of real cases and fails without signalling. A green up-arrow on a churn spike is not a cosmetic defect — it is a confident wrong claim, rendered beautifully, arriving at a stranger by link. Carter's formulation names the mechanism exactly: viewers cannot distinguish intention from default, so an auto-generated dashboard looks like something somebody meant. Polish raises the cost of being wrong, because an ugly chart gets fixed and a beautiful wrong one gets forwarded.
**Leading indicator:** Polarity guessed incorrectly on more than 10% of measure columns across a 30-sheet corpus; or any shipped annotation the underlying data does not support.
**Evidence:** Reasoned argument from the design canon. The 60% figure is Design-canon's working estimate, not a measurement — hence KC-5.

### FM-10 — The name is a registered EU trademark in the software class · *dependency/regulatory*
**Mechanism:** DASHERO is a live registered EUIPO word mark in classes 35, 36 and 42 across 29 territories, owned by Dashero S.L. Class 42 covers software and SaaS, which is a direct conflict for any EU-facing launch. dashero.com is registered since 2015 and parked for sale at an undisclosed price. Dasheroo — a business-intelligence dashboard product — is confusingly close in both name and category. The cost is not a lawsuit on day one; it is that branding, domain, and any EU go-to-market are built on ground that has to be rebuilt later, at exactly the moment traction would make rebranding most expensive.
**Leading indicator:** Any correspondence from Dashero S.L.; or a domain quote above the operator's total budget; or a trademark attorney advising against US filing.
**Evidence:** E-11, E-38, E-39.

### FM-11 — Scope is roughly 2.5-3x the time budget, and distribution is what gets cut · *operator*
**Mechanism:** The build inventory runs to thirteen production subsystems before any design iteration or marketing — OAuth and consent, sheet ingest and change detection, table and type inference, chart inference, a custom-quality render layer, an LLM edit loop with spec validation and repair, viewer AI with injection defence, auth and namespaces and link tokens, billing, abuse controls, landing page, a design system, and support. That totals roughly 15-17 weeks of focused solo engineering. A 3-4 month window to revenue requires the build to land in 6-8 weeks to leave any selling time. Under compression, work with a compiler error beats work without one: build has a compiler, design has a screenshot, support has an angry email, and marketing has none of these. It slips every week, silently, until the window closes.
**Leading indicator:** Week 6 arriving with zero landing-page traffic and zero conversations with prospective users; or any week where "make the charts nicer" wins over "talk to five people."
**Evidence:** Reasoned argument from the stated constraints and the build inventory.

### FM-12 — The differentiator is the one component with no library, no shortcut and no available skill · *operator*
**Mechanism:** The stated bar rejects "bars and scatter plots with colors and annotations," which means annotation and emphasis that turn a chart into an argument. Decomposed, that requires knowing which fact in the data is the point, choosing the encoding that makes it legible, writing a headline stating the finding, annotating the specific anomaly, and getting typography, spacing and palette coherent in both themes. The first four require domain knowledge the system does not have; the last requires a designer the operator does not have. The realistic output of chart inference plus a good library is a competent generic dashboard, which is what the platform owner already gives away. Meanwhile the reference standard for this aesthetic has pursued it since 2012 and gives it away free with unlimited views.
**Leading indicator:** Showing five generated dashboards cold to five strangers and fewer than three stating the main finding within 10 seconds without reading axis labels.
**Evidence:** E-29. Partly defused by Design-canon's finding that declarative data-derived titles are cheap and automatable, and that repositioning from "most beautiful" to "the dashboard you do not have to fix" trades an uncompoundable asset for a compounding one.

## The case for

Written after the case against, by an agent dispatched last and required to engage the red-team
findings rather than talk past them. Same evidentiary standard.

### FOR-1 — The Sheets canvas gap is a tier gap, not an account-type gap, and it is roughly an order of magnitude wider than first measured
**Mechanism:** Google's own availability notice limits canvas to Business Standard and Plus, Enterprise Standard and Plus, and consumer AI Pro and Ultra. The excluded set is therefore not merely free gmail.com accounts — it is free consumer accounts **plus Business Starter, plus Enterprise Starter and Essentials, plus Frontline**. Business Starter is Google's cheapest paid tier and the default landing spot for freelancers, solo professionals and micro-teams, which is precisely dashero's plausible buyer. The cheapest route in for an unaffiliated individual is a paid consumer AI subscription in which spreadsheet dashboards are one bundled feature among dozens. dashero is not competing against free; it is competing against a bundle priced at or above its own proposed Starter tier.
**Evidence:** E-3, accessed 2026-08-25 — the availability list is verbatim from Google's rollout post.
**Which failure mode it survives:** FM-1. The incumbent is not free for the segment in question and is not available even on Google's own entry-level paid tier. It binds anyway to this extent: Google's historical pattern is to push AI features down-tier over time, so this is a wedge with an expiry date, which is why it is written into KC-11 as a continuously-checked external trigger.

### FOR-2 — Willingness-to-pay for presentation-quality charting inside the Sheets workflow is directly evidenced, not inferred
**Mechanism:** The claim that willingness-to-pay concentrates in privacy, live refresh and connectors rather than aesthetics rests on a single artifact — Infogram's tier structure — which is evidence about how one company packages, not a measurement of buyer preference. A direct counter-instance exists in dashero's exact adjacency. ChartExpo is a paid Google Sheets add-on selling nothing but better chart types and storytelling presentation: no connectors, no joining, no warehousing, no live refresh. It charges $10 per user per month and claims over 700,000 users, positioning on "convey ideas" and "tell your data story effectively." That is dashero's positioning, already monetised, on the axis said not to monetise.
**Evidence:** E-41, E-42, accessed 2026-08-25. The price is from the vendor's own pricing page and is solid; **the 700,000 figure is an unaudited vendor self-claim counting users rather than payers, and must not be treated as demand sizing.**
**Which failure mode it survives:** Partially FM-2 and the willingness-to-pay claim underlying FM-7 — ChartExpo's paywall fires on aesthetics and has done so long enough to accumulate a base. It binds anyway: ChartExpo runs *inside* Sheets and rides Marketplace distribution, which dashero as a hosted external app does not get. This establishes that the axis monetises; it does not establish that dashero can reach the people paying on it.

### FOR-3 — The graveyard is selected on positioning, and the survivors in this category are the presentation-positioned ones
**Mechanism:** Every product on the death list — Chartio, Silk, Actiondesk, Blockspring, Fusion Tables, Google Tables, Chart Studio, Spreadsheet.com — was positioned as analysis, BI, or data management. That is the category that behaves as a feature. Two products positioned instead on publication and presentation quality did not die: Datawrapper (bootstrapped, founded 2011, roughly $3.2M ARR at about 29 employees) and Flourish (roughly 800,000 users on about $1M of venture capital total, acquired by Canva in February 2022 with all 44 employees retained). Both exist on top of free Google Charts and free Looker Studio. The extracted condition — flagged as inference rather than sourced finding — is that **taste survives against free when the output is shown to a third party.** Notion, Linear and Superhuman are weaker analogies because those are private-use tools where taste buys retention rather than conversion. Datawrapper and Flourish share dashero's defining property: the artifact is published and read by someone other than its author, which is exactly the share-by-link shape.
**Evidence:** E-43, E-44, E-45, accessed 2026-08-25. The Datawrapper ARR figure comes from a self-reporting aggregator and is indicative, not established.
**Which failure mode it survives:** The dead-product pattern behind FM-13-class reasoning, and the modal-outcome framing that treats $75-200 MRR as failure. There is a frame correction underneath: Spreadsheet.com died at 1,000+ paying organisations because it had taken $5.5M and could not reach venture scale. For a solo operator with no investors, 1,000 customers at $25 is $25,000 MRR. Against the MicroConf 2024 independent-SaaS distribution — 38% of products under $10k in *annual* revenue, 28% between $10k and $50k — the operator's $1,000 MRR threshold sits near the median of the population he is actually joining. It binds anyway: Datawrapper took fifteen years and serves a findable vertical (newsrooms) that dashero does not have, and Flourish's outcome was acquisition-shaped.

### FOR-4 — "Charts that state their finding" is an unoccupied position, and it is the cheap half of "tells a story"
**Mechanism:** Declarative titles generated from the data are one template plus one statistic, and they convert a chart from a lookup surface into a claim. Checking whether anyone ships it: Datawrapper — whose own guidance calls the title "the first or second thing your readers will see and therefore very important" — makes the user write it **by hand** in the Annotate tab. Power BI's Smart Narrative generates a separate summary text visual beside the chart, not a headline asserted as the chart's own claim. Tableau Data Stories was the closest thing and is gone. The position is currently vacant across the competitive set. This also decomposes the objection that killed the differentiator: "tells a story" is not one problem but a *taste* problem (beautiful marks, where the no-designer objection binds hard) plus a *statistics* problem (state the finding), and the second is a computation rather than a sensibility.
**Evidence:** E-46, E-47, E-48, accessed 2026-08-25.
**Which failure mode it survives:** FM-12, the objection judged to have no defusing architectural move. The defusing move is decomposition. It binds anyway, and this is stated at full strength: **Tableau built automatic narrative and retired it in January 2025.** That is direct negative evidence (E-49). Two readings are live — the feature had no value, or it was folded into Tableau Pulse — and the retirement notice favours the second, but the first is not excluded and is the single best argument against this reason. Separately, FOR-4 is **strictly conditional on shipping the confirmation screen**: without elicited polarity, an auto-generated declarative title is confidently wrong on a meaningful share of metrics, and this argument inverts into FM-9.

### FOR-5 — Nearly every fatal objection attaches to a removable feature decision, and the residue has no known fatal objection
**Mechanism:** Enumerating what each blocker actually attaches to: free-tier insolvency attaches to free-tier viewer AI (a config change); the wrong pricing axis attaches to sheet-count pricing (config); structural non-virality attaches to virality as the growth plan (an assumption, not a feature); the frequency paywall attaches to the second-sheet gate (same config change); silent wrong charts attach to fully automatic inference (the 15-second confirm screen); aggregate re-identification attaches to unsuppressed aggregates (n≥5 suppression at build time). Six objections, six configuration-level changes, none architectural. Two points sharpen this. The insolvency arithmetic was computed on premium model pricing; a viewer turn at Gemini Flash-Lite rates is roughly 10x cheaper, so the free tier was not structurally insolvent but priced against the wrong model. And the technical and design agents **independently converged on the same confirmation screen** from unrelated premises — one from table-boundary detection, one from polarity elicitation. Independent convergence from different starting points is the strongest signal in the session, and it points at a fix costing fifteen seconds of user time. What remains after the six changes: connect a sheet, confirm shape and polarity in about 15 seconds, receive a themed dashboard whose charts state their findings, share by link. **No report in this session raises a fatal objection to that product.**
**Evidence:** Reasoned argument over the session's own findings; the Flash-Lite pricing is E-18. No new external evidence.
**Which failure mode it survives:** FM-2, FM-4, FM-5, FM-6, FM-7. It binds anyway, decisively: **none of these changes shrink the build inventory or solve distribution.** FM-3 and FM-11 survive the reshape entirely, and the reshape adds work to a schedule already over budget.

---

## Addendum — generative dispatch

**Why this section exists.** The Clause #11 dispatch table contains four adversarial lenses, one
research lens, and a steel-man constrained to *defending the specification*. No lens was pointed at
the market. Every agent above answered "is dashero a good idea"; none answered "what is the best
product in this space for this operator." The operator identified this gap and three further agents
were dispatched under the same evidentiary rules but with generative briefs: a Demand Archaeologist
(revealed preference), a Gap Scout (unserved need), and a Pivot Architect (candidate product shapes,
with the incumbent plan scored on equal terms).

**Methodological limitation, stated first because it bounds everything below.** All three ran after
the session's web-search budget was exhausted. Between them they executed **zero keyword searches**
and reached every source by hand-constructing URLs. Consequently: every "not crowded" claim in this
addendum is weaker than it appears — competitors already known were verified, competitors unknown
could not be discovered. The Gap Scout was additionally blocked by fourteen software-review
platforms returning HTTP 403, so it holds **no review data at all**, and its complaint ledger is
biased toward products with public issue trackers. Its own words: Metabase is over-represented
because it is open, not because it is worse.

### What the generative lens found that the adversarial lens could not

**Revealed preference exists, and it is priced per client rather than per dashboard.**
AgencyAnalytics charges $20 per client per month; DashThis $44-54; Swydo about €12.15 per client;
SyncWith $24.99-149.99. The Demand Archaeologist's formulation: the buyer is not paying for a
dashboard, they are paying for not having to redo a report every month for a client who will look at
it. (E-53, E-54, E-55)

**The bespoke-build market has collapsed in price.** PeoplePerHour lists 300+ freelancers across 16
pages for this work against roughly two live dashboard-shaped buyer projects; a $150-200 project drew
39 proposals and a $34/hr posting drew 50; fixed-price offers cluster between $10 and $125. Any
product positioned as cheaper than hiring a freelancer competes with a price already collapsing
without it. (E-56)

**The best-evidenced unserved need is parameterized fan-out** — one report definition, N recipients,
each seeing only their own slice, each branded as theirs. Six independent threads spanning 2019-2026
across *unrelated* verticals: a PPC agency with "around 100ish clients [where] the templates are just
BS"; a sole analyst at a manufacturer with "50+ production lines... the KPIs and layout are the same
across all lines"; a thread titled "Moving 80 Clients from AgencyAnalytics to Looker Studio."
Recurrence across unrelated verticals was the strongest demand signal produced in the entire session.
(E-57)

**The most structurally protected gap is Google Sheets as a live source below the BI price floor.**
Metabase issue 7985 carries 205 reactions and has been open since 2018-07-06; Metabase's own
documentation states that Sheets sync requires paid Cloud plus the Cloud Storage add-on and that
self-hosted instances cannot use the integration at all; its published roadmap does not mention
Sheets. The incumbent is commercially prevented from closing this. Separately, Datawrapper's pricing
page mentions dashboards, live data connections and scheduled refresh exactly zero times on any tier
— a deliberate product boundary rather than a backlog item. (E-58, E-59)

**Two apparently strong gaps are closing this month**, reported by the Gap Scout against its own
thesis: Metabase's public roadmap now lists both "Dashboard invites — share dashboards with people
outside Metabase with one click" and "attach a dashboard as a PDF to your subscriptions." Gated
external sharing and board-ready PDF export should therefore be scored as weak, not as openings.
(E-60)

**Observed workarounds — each one a job someone does by hand:** screenshotting a dashboard with the
Windows Snipping Tool to share it; pasting screenshots into client PDFs manually; routing Sheets
through BigQuery to reach a BI tool; reverse-proxying Metabase behind nginx basic-auth to fake
per-client passwords; running headless Chrome to render a PDF the vendor declines to build; Apps
Script cron jobs; a literal monthly copy-paste ritual between tabs. (E-61)

**The persona in the original thesis is now an evidenced negative.** The Demand Archaeologist rated
SMB operators with one recurring report the least findable of four segments: "one-off posts years
apart, not a congregating population. I could not locate a venue where twenty of them are reachable
this week." It searched specifically for nonprofit, church, club and league buyers and found nothing.
The reachable-buyer score for the specified product moves from absence of evidence to evidence of
absence. (E-62)

### The candidate ranking

Seven candidate product shapes were scored on seven criteria — buildable solo in under 8 weeks,
reachable buyer, revenue arithmetic to $1,000 MRR by late December, resistance to the obvious
incumbent response, fits a $20/month inference budget, reuses the banked assets, requires no designer
— with buyer and revenue double-weighted because distribution was established as the binding
constraint and the operator's stop-rule is a revenue number.

| Candidate | Weighted | Verdict |
|---|---|---|
| Parameterized fan-out over a Sheet, scoped to 6-7 weeks | **22** | Recommended. The only candidate clearing the revenue gate. |
| Service-funded add-on | 20 | Fails its own gate once the labour anchor is applied. Fallback only. |
| Pure done-for-you report service | 19 | Fails gate. Bridge if the pre-sale fails. |
| Open-source commandments library | 19 | Scores well, earns nothing. Included as a calibration check on the rubric. |
| Single-chart Sheets add-on | 17 | Best 18-month asset in the table; loses only on the clock. |
| Bookkeeper client-report product | 16 | Right buyer, build size reproduces the original failure. |
| Print-quality board-pack PDF | 14 | Dead — Metabase is closing it this month. |
| **dashero exactly as reshaped** | **8** | **Last. Fails all three weighted criteria outright.** |

**The argument that decided it, and it is an asymmetry in what each candidate is priced against.**
The service candidate competes with an anchor *below* its proposed price — $1,000 MRR at $25 per
client report is roughly 30 hours of work, or about $33/hour, which is the exact rate that attracted
50 competing proposals. The fan-out product competes with an anchor roughly *16x above* its proposed
price: AgencyAnalytics costs about $800/month for a 40-client agency, against $99 flat. That is the
difference between selling into a price war and selling into a price umbrella.

**What the Pivot Architect refused to concede**, and this matters for calibration: it rejected the
Gap Scout's "under 3 months" sizing as missing the window, scoping the build to 6-7 weeks by deleting
the spec-builder UI (the report is defined in a config tab inside the Sheet), scheduled refresh (a
publish-all button, since operators tolerate manual today), and any auth beyond unguessable signed
URLs (strictly better than the nginx workaround observed in the wild). It also rejected the Gap
Scout's "structurally protected" reading as one notch too confident, on the grounds that
AgencyAnalytics and DashThis already sell this shape — so the protection is *pricing*, which can
change in an afternoon, not architecture.

**Two structural facts about fan-out worth recording.** In its favour: it is quota-efficient by
construction, because N recipients render from one snapshot and therefore cost **one** Sheets read —
the 300-reads-per-minute project pool that made read-on-load unviable is a non-issue, and the
100-user OAuth cap binds paying customers rather than anonymous recipients. Against it: fan-out
requires a snapshot, so it **reintroduces KC-1 and KC-9**, both of which the add-on shape had
deleted.

**Asset reuse is higher here than in any other candidate**, including the incumbent: all 18
commandments apply, the dashboard grammar returns, and declarative titles are worth more in this
shape than anywhere else — one template across N slices produces N different findings, which is
literally the one-template-plus-one-statistic mechanism fanned out.

---

## Kill criteria

Consolidated from all five agent returns, deduplicated, each falsifiable and dated. Today is
2026-08-25; the operator's window closes approximately 2026-12-25.

### KC-1 — The `drive.file` persistence spike
**Stop if:** a throwaway spike proves a `drive.file` grant does NOT survive an unattended server-side re-read 48 hours after the user last authenticated, with no session present. Failure forces a sensitive scope carrying a permanent 100-user cap, and the snapshot architecture must be re-planned before any Wave 1 build.
**Covers:** A-15, FM-8
**Check by:** 2026-09-08

### KC-2 — The 100-user cap ambiguity
**Stop if:** an empirical test shows the 100-new-user cap DOES bind a Published app using only non-sensitive scopes. Google's own two support pages contradict on this, and the product cannot exceed 100 lifetime users without weeks of verification if the pessimistic reading holds.
**Covers:** A-16
**Check by:** 2026-09-15

### KC-3 — The wedge is real
**Stop if:** across 20 recorded interviews with people matching the target profile, fewer than 6 name chart quality or appearance unprompted as a top-3 pain; or, when shown Sheets canvas output beside a dashero mock, fewer than 8 of 20 say they would pay for the dashero version. Cost to run: about two weeks and $0. This is the highest-value action available and should precede any product code.
**Covers:** A-11, A-29, FM-1, FM-2
**Check by:** 2026-09-22

### KC-4 — Inference accuracy on real sheets
**Stop if:** across 30 real spreadsheets not authored by the operator, fewer than 24 (80%) have their table region, header row, column types and totals-row exclusion pre-filled correctly enough that a user confirms with at most one correction. Below 18 of 30 (60%), the inference premise is falsified outright.
**Covers:** A-20, A-21, FM-5
**Check by:** 2026-10-01

### KC-5 — Polarity guessing accuracy
**Stop if:** on the same 30-sheet corpus, the model guesses metric polarity incorrectly on more than 10% of measure columns. Above that threshold, declarative titles and directional colour must stay gated behind explicit elicitation, and any design assuming inferred polarity is unsafe.
**Covers:** A-22, FM-9
**Check by:** 2026-10-01

### KC-6 — Measured inference cost
**Stop if:** instrumented against real prompts and a real spreadsheet, one dashboard generation exceeds $0.05 or one viewer turn exceeds $0.01 on the cheapest acceptable model. Separately, switch the viewer AI off within 24 hours if any single share link generates more than 200 AI turns in a day, or any day's total spend exceeds $1.50.
**Covers:** A-26, A-27, FM-6
**Check by:** 2026-09-15, then continuously

### KC-7 — Frequency, and therefore the paywall's population
**Stop if:** fewer than 8 of the same 20 interviewees report creating 3 or more distinct dashboards in the last 12 months. Below that, the second-artifact paywall has no population and the pricing model must be rebuilt before building.
**Covers:** A-30, FM-2, FM-7
**Check by:** 2026-09-22

### KC-8 — Distribution has any channel at all
**Stop if:** one named channel is not identified by 2026-09-22 and one test run by 2026-10-06 producing at least 50 email signups for at most $100. Then: stop if unique visitors across all channels total under 2,000 by 2026-10-31, or fewer than 8 paying customers exist 60 days after launch.
**Covers:** A-31, A-32, FM-3, FM-4
**Check by:** 2026-10-06, then 2026-10-31

### KC-9 — The caching question
**Stop if:** legal review concludes that persisting parsed snapshots server-side beyond the cache-header duration is not permitted under Google APIs ToS section 5.e. The snapshot architecture is load-bearing for both the latency target and the quota ceiling, so an adverse reading invalidates both.
**Covers:** A-18
**Check by:** 2026-09-29

### KC-10 — The operator's own threshold, enforced
**Stop if:** fewer than 40 paying customers at $25 (or the revenue equivalent at a revised price) by 2026-12-25, or total spend exceeds $1,000, whichever comes first. The entire value of this criterion lies in refusing to move it once written.
**Covers:** A-7, A-34, FM-11
**Check by:** 2026-12-25

### KC-11 — External trigger, checked continuously
**Stop if:** Google publishes any of: Sheets canvas extended to free gmail.com accounts, a native publish-this-analysis-as-a-shareable-page feature in Sheets or Looker Studio, a reclassification of the `drive.file` scope, or 2026 quota pricing material at the target scale. Any one of these requires a GO/NO-GO re-evaluation within one week.
**Covers:** A-11, FM-1, FM-8
**Check by:** continuously from 2026-08-25

### KC-12 — The name
**Stop if:** a trademark attorney advises that the EUIPO DASHERO registration in class 42 blocks the intended launch territories, or the dashero.com asking price exceeds $1,000. Rename before any branding, domain purchase, or public launch — not after.
**Covers:** A-19, FM-10
**Check by:** 2026-09-08

### KC-13 — The named buyer, and the concierge test
**Stop if:** the operator cannot name a specific, reachable, countable first buyer by 2026-09-08; or if, having hand-built 5 dashboards from real spreadsheets he did not author and delivered them as static links, fewer than 1 of the 5 recipients pays $25. This is the gating criterion for the entire verdict below. It costs one weekend and $0, it requires no product code, and it converts every argument in this brief — including all five reasons in the case for — into an observable.
**Covers:** A-29, A-30, A-31, A-32, FM-2, FM-3, FM-12
**Check by:** 2026-09-08

### KC-14 — The pre-sale gate, which supersedes KC-13 as the binding test
**Stop if:** fewer than **5** of roughly 50 contacted producers-for-hire — the top decile of named, publicly messageable PeoplePerHour profiles by completed-project count, plus identifiable AgencyAnalytics defectors — return a paid pre-order or a written letter of intent at $99/month by **2026-09-12**, having been shown one page describing the artifact and nothing else. No build begins before this clears. This test costs one week and roughly $0, and it directly falsifies the load-bearing risk that this audience admires the product and does not buy it, having already chosen unpaid labour over a subscription.
**Covers:** A-29, A-31, A-32, FM-2, FM-3
**Check by:** 2026-09-12

### KC-15 — The one-hour competitive check that could falsify the recommendation outright
**Stop if:** DashThis at $44-54/month, or any comparable at under $100/month, already delivers flat-rate per-client fan-out with per-recipient branding. The recommended candidate rests on a price wedge of roughly 16x against AgencyAnalytics; if a flat-rate incumbent already occupies that position, the wedge narrows to roughly 1x and the candidate falls below the fallback. Run this **before** the outreach in KC-14, not after.
**Covers:** A-35, FM-1
**Check by:** 2026-09-01

---

## Alternatives considered

Clause #11 Rule 6, added by Amendment 1 on 2026-08-26 — an amendment this session's own findings
produced. Scored by the Pivot Architect across two passes, the second after revealed-preference and
unserved-need data arrived from sibling agents.

| # | Candidate | Buyer (specifically) | Job it does | Build (weeks) | Distribution answer | Score | Verdict |
|---|---|---|---|---|---|---|---|
| ALT-0 | **dashero exactly as reshaped** (the specification) | Unnamed. A description, not a list — someone on a low Google tier who publishes numbers weekly | Turn my sheet into a shareable dashboard I do not have to fix | 15-17 | **None.** Modelled at roughly 4 paying customers across every enumerated channel | **8** | **Last of eight. Fails all three weighted criteria.** |
| ALT-1 | Per-recipient fan-out over one Sheet, scoped | Producers-for-hire serving many clients — top decile of 300+ named, messageable PeoplePerHour profiles by completed-job count | One report definition, N branded per-recipient links, each showing only their slice | 6-7 | Cold outreach to a named, countable list, contactable this week | **22** | Recommended, but weakened after the KC-15 check — see below |
| ALT-2 | Service-funded add-on | Solo bookkeepers and fractional CFOs with 5-20 clients | Done-for-you monthly reports now, product later, funded by the service | 5 + service | Cold outreach from week 1, then a warm Marketplace listing | 20 | Fails its own revenue gate once the labour anchor is applied |
| ALT-3 | Pure done-for-you report service | Same buyer as ALT-2 | Someone competent makes my monthly numbers presentable | 0 | Cold outreach to a public directory from week 1 | 19 | Fails gate. It is a job, not an asset. Bridge only |
| ALT-4 | Open-source commandments library | Developers generating charts programmatically | Stop my generated charts being wrong, and make them title themselves | 3-5 | Show HN, npm, the Vega community — attention, not revenue | 19 | Scores well, earns nothing. Kept as a calibration check that the rubric is not a ranking function |
| ALT-5 | Single-chart Sheets add-on | Anyone selecting a range who needs one chart for a deck or email | Make the one chart I am about to paste somewhere actually say something | 5.5 | Marketplace search rank only — passive, cold start, no one is contactable | 17 | Best 18-month asset in the table; loses only on the clock |
| ALT-6 | Bookkeeper client-report product | Solo bookkeeper or fractional CFO | Produce the branded monthly client report on time | 10-14 | Accountant directory outreach, but arrives after the product ships in December | 16 | Right buyer, build size reproduces exactly the failure that killed ALT-0 |
| ALT-7 | Print-quality board-pack PDF | Nonprofit ops manager, association secretary, school district | The quarterly board pack that must look like a document | 8-12 | Nonprofit registry outreach; quarterly cycle misses the clock entirely | 14 | Dead — an incumbent is closing this gap this month |

**Scoring criteria used:** buildable solo in under 8 weeks; has a reachable buyer contactable this
month; plausibly reaches $1,000 MRR by 2026-12-25 and by what arithmetic; survives the obvious
incumbent response; fits a $20/month inference budget; reuses the assets this session already paid
for; requires no designer. **Reachable-buyer and revenue arithmetic were double-weighted**, because
distribution was established as the binding constraint and the operator's own stop-rule is a revenue
number. Revenue was additionally treated as a pass/fail gate rather than a score, given the stated
goal of making money immediately — which is what eliminated ALT-2 through ALT-7 regardless of their
totals.

**Why the winner beats the specification (or does not):** ALT-1 beats ALT-0 on the only two criteria
that were ever binding. Its buyer is a named list rather than a description, and its build fits the
window with selling time left over. The asymmetry that decided it: the service candidates competed
against a market anchor *below* their price, while ALT-1 appeared to compete against one far above
it. **That advantage has since narrowed and the brief should not pretend otherwise.** The KC-15 check
run on 2026-08-26 found AgencyAnalytics already supports Google Sheets as a data source with
per-client white-labelled reports, and DashThis already advertises flat-rate pricing that is not
per-client at $429/month for 50 dashboards. The price wedge is therefore roughly 4x, not the 16x the
scoring assumed. ALT-1 remains ranked first, but its margin over ALT-2 is now thin enough that KC-14
decides it rather than the rubric. For ALT-0 to have won, the SMB-with-one-recurring-report buyer
would have had to be findable — and a targeted search established the opposite.

**Evidence that each alternative is not already served:** ALT-1 — partially served; AgencyAnalytics
does this at $20/client and DashThis at $429 flat for 50 dashboards (E-53, E-54, and the KC-15 check
of 2026-08-26), so the claim is price and simplicity, not absence. ALT-2 and ALT-6 — the
spreadsheet-native slot below Fathom's AUD$59 and Reach Reporting's $149 appears open, but "open
below the price floor" and "worth paying for" are different claims and only the first is evidenced.
ALT-4 — the 18 commandments as executable rules with hard render gates does not exist as a library;
Vega-Lite is the substrate, not a competitor (E-14). ALT-5 — the aesthetics-only in-Sheets position
is proven to monetise (E-41, E-42), but an add-on shipping approximately the auto-insight concept
shows 24 installs (E-64), so a listing is not distribution. ALT-7 — Datawrapper paywalls PDF export
and Reach Reporting serves nonprofits at $149 (E-59), leaving the print-quality slot below both real,
but an incumbent is closing it this month (E-60). ALT-3 — **not established.** Freelance
data-visualisation pricing could not be reached; Fiverr and Upwork both returned HTTP 403 and the
session's search budget was exhausted, so ALT-3's price is unanchored against its own market.

---

## Verdict

**Decision:** `RESHAPE` — and after the generative dispatch, the reshape is product-level rather
than feature-level. Conditional, with a dated precondition that resolves to a stop if unmet.

**What changed between the first verdict and this one.** The verdict recorded after the five
Clause #11 agents was a feature-level reshape of dashero — cut the free-tier viewer AI, re-price off
sheet count, add a confirmation screen — and it carried an explicit self-criticism from the
steel-man that a reshape leaving the two load-bearing objections untouched was a stop wearing a
costume. The three generative agents then addressed exactly those two objections, and the answer was
not a better version of dashero. It was a different product for a different buyer, built from the
same banked assets, whose build inventory is 6-7 weeks rather than 15-17 and whose buyer exists as a
named, publicly messageable list rather than as a description. **dashero as reshaped scored last of
eight candidates on a rubric that double-weighted the two things that killed it.** The reasoning
below is preserved because it remains accurate about the specified product; it is superseded as a
plan.

**The recommended shape.** Parameterized fan-out over a Google Sheet — one report definition, one
key column, N per-recipient signed URLs, each recipient seeing only their own slice, each branded as
theirs, every chart stating its own finding. Sold flat at $49-99/month for up to 50 recipients
against an incumbent charging roughly $800/month for the same client count. Ten customers at $99
clears the operator's threshold. All 18 commandments carry over, the dashboard grammar returns, and
declarative titles are worth more in this shape than in any other, because one template across N
slices produces N distinct findings.

**Reasoning (on the specified product, retained):** dashero as specified fails on three independent
grounds, each argued by a
different agent working a different lens: the free-tier viewer AI is insolvent roughly an order of
magnitude below the user count needed to reach the revenue target, the paywall fires on a frequency
event that most users never reach, and no enumerated channel closes the funnel at any sourced
conversion rate. The reshaped product — confirm-the-shape onboarding, declarative titles, no
free-tier viewer AI, metered pricing on AI turns rather than sheet count — draws no fatal objection
from any of the five agents, and the one genuinely unoccupied position found in the entire session
(charts that state their own finding, which Datawrapper leaves manual, Power BI puts in a side panel,
and Tableau retired) is cheap to build and sits exactly where the operator's stated ambition points.
**But two load-bearing objections survive the reshape untouched: the build inventory runs roughly
2.5-3x the available time, and there is still no distribution answer.** The reshape adds work to a
schedule already over budget and offers no channel where none existed. That is why this verdict is
conditional rather than clean.

**If RESHAPE — what changes:** Position on *the dashboard you do not have to fix* rather than *the
most beautiful charts*, because zero-effort presentability is an operational property that compounds
and taste is not. Ship a 15-second confirmation screen at connect time that establishes table
boundary, header row, column types, and per-metric polarity — the single interaction that two agents
reached independently from unrelated premises, and the precondition for declarative titles being
honest rather than confidently wrong. Cut free-tier viewer AI, cut the second-sheet paywall, and stop
treating virality as a growth plan rather than a lottery ticket. Meter on AI turns and seats, never
on sheet count. Rename before any brand equity exists. And name a real first buyer before writing
product code — the sharpest available candidate is someone on a Google Workspace Business Starter
account or a free consumer account who publishes numbers to a third party weekly, because they are
excluded from Sheets canvas by tier and they satisfy the condition under which taste has historically
beaten free.

**Strongest argument against this verdict:** The people this plan proposes to sell to have already
solved the problem — badly, laboriously, but for free — and the evidence for the gap is simultaneously
evidence that they will not pay to close it. The thread anchoring the whole finding is an operator
moving 80 clients *off* paid tooling *onto* free Looker Studio, which demonstrates price sensitivity
rather than willingness to pay. The workaround catalogue reads the same way: reverse-proxying behind
nginx basic-auth, running headless Chrome to render a PDF, Apps Script cron jobs, screenshotting a
dashboard with the Windows Snipping Tool. Every one of those is a person who chose unpaid labour over
a subscription. A market whose defining behaviour is building the workaround yourself is a market
that will admire the product and not buy it — and if that is what is happening here, the revenue
score is wrong by exactly the mechanism that made the previous recommendation's revenue score wrong,
namely pricing against what the job is worth rather than against what these specific people have
demonstrated they will pay. The week-one pre-sale in KC-14 is the only thing standing between that
hypothesis and eleven wasted weeks, which is why nothing gets built before it clears.

**Strongest argument against the earlier feature-level verdict, retained for provenance:** RESHAPE is
the verdict an advocate always reaches,
because it preserves whatever survived and discards whatever was refuted, and it therefore feels like
analysis while functioning as permission. Examine what was actually discarded here — free-tier viewer
AI, sheet-count pricing, unbounded virality. None of those were the load-bearing objections. The
load-bearing objections are that the build is roughly three times the available time and that the
expected number of paying customers across every enumerated channel is approximately four against a
target of forty. This reshape touches neither, and adds work to the first. A RESHAPE that leaves both
load-bearing objections untouched is a NO-GO wearing a costume, and the honest form of this verdict
is that it holds only while KC-13 holds. If no specific reachable buyer can be named by 2026-09-08,
the correct verdict is NO-GO and it should be recorded without argument.

**Cheapest next test:** One week, roughly $0, no code. Run KC-15 first — one hour establishing
whether any incumbent under $100/month already sells flat-rate per-client fan-out with branding,
because a yes collapses the price wedge from 16x to 1x and the recommendation falls. Then run KC-14:
write one page describing the artifact — one report definition, one key column, N branded
per-recipient links, $99/month flat up to 50 recipients — and send it to roughly 50 producers-for-hire
drawn from the top decile of named, publicly messageable PeoplePerHour profiles by completed-project
count, plus identifiable AgencyAnalytics defectors. Ask for a $99 pre-order or a written letter of
intent. **Build only if five say yes by 2026-09-12.** Run the one-day `drive.file` persistence spike
(KC-1) alongside it, since fan-out reintroduces the snapshot dependency, and settle the name (KC-12).
The superseded concierge test below remains a valid fallback probe if the pre-sale returns ambiguous
signal rather than a clean no.

**Superseded cheapest next test, retained for provenance:** A concierge test, one weekend, $0. Take
5 real spreadsheets the operator did not author — from public help forums, a local business, a
freelancer's client reporting — and hand-build for each the dashboard dashero would generate,
including a declarative title on every chart stating what the data shows. Deliver each as a static
link. Then ask for $25. This is decisive in a way nothing else in this session is, because it tests
all three load-bearing unknowns simultaneously (is the inference achievable, does the declarative
title read as *the point* to the person who owns the data, will anyone pay) and produces the first
five candidate customers as a byproduct. It also subsumes the 30-sheet study that two agents
independently requested — score the same corpus for boundary accuracy and polarity accuracy. Run two
one-day tasks alongside it: publish a stub OAuth app requesting only `drive.file` and read the actual
user quota, resolving KC-2 and gating FOR-1; and settle the name. If nobody pays $25 for a hand-made
version built with unlimited human taste and unlimited human domain knowledge, no automated version
can rescue it — and that will have been learned in a weekend rather than in fifteen weeks.

---

## Handoff to Wave 0

**Wave 0 does not begin on this verdict alone.** KC-13 gates it. The concierge test and the named
buyer come first; if they fail, this brief closes at NO-GO and no phase spec is written.

**P1 scope this implies:** A single-user web application that connects one Google Sheet through the
Google Picker under the `drive.file` scope, profiles the selected range, and presents a short
confirmation screen establishing the table boundary, header row, per-column type, and per-metric
polarity. On confirmation it stores a parsed, typed snapshot refreshed by background sync on an
interval, never read-on-load, with an explicit as-of timestamp and a manual refresh control. From the
snapshot it infers a dashboard of charts as Vega-Lite specifications validated against the published
JSON Schema before render, applying the commandment set in `plans/design-canon-notes.md` — three of
which are hard render gates — and generating a declarative title per chart from the data, gated
behind known polarity so that an unknown polarity yields a neutral title rather than a wrong claim.
Aggregates are built with an n≥5 suppression rule applied before any chart or model sees them.
Creator-side conversational refinement edits the validated spec. The dashboard is published at a
per-user namespaced URL reachable by unlisted link. A workspace record exists from the first
migration with exactly one member, so shared team namespaces are a later migration rather than a
rewrite. The insight-extraction prompt lives in a versioned file in the repository.

**Out of scope for P1, deliberately:** viewer-side AI on the free tier; database and warehouse
connectors; 100M-row scale; organisations, roles and invitations; a public gallery; embedding;
scheduled refresh; alerting; the second-sheet paywall; and virality treated as a growth mechanism
rather than an unremovable attribution badge.

**Stack decision + rationale:** TypeScript on Node, single application, deployed to a container host
with a persistent volume — Fly.io, Railway with a volume, or a plain VPS — explicitly **not** a
serverless platform, because SQLite requires a persistent filesystem that serverless does not provide
and discovering that mid-build would force a migration inside the runway. SQLite in WAL mode is the
datastore, which is defensible at this workload (read-heavy per-user snapshots, single-writer
background sync, aggregate counts well under any columnar threshold) and honours the operator's
stated preference for something simple and local; the deferred database-connector phase is the point
at which this is revisited, not before. Charts are Vega-Lite, chosen because it is the only major
library shipping a live JSON Schema, which lets a model emit a specification that a validator rejects
before it reaches a renderer and removes any need for sandboxed code execution. Google access is
Picker plus `drive.file` only, never `spreadsheets.readonly` and never any `drive.*` restricted
scope, because that classification is what avoids sensitive-scope review and the annual CASA
assessment entirely. LLM inference runs on a paid tier of any provider — never an unpaid tier, which
Google's Workspace API policy forbids because unpaid tiers train on submitted content and permit
human review — routing cheap high-volume paths to a low-cost model and reserving a stronger model for
creator-side generation. Print-quality PDF export, if built, is a later paid-tier feature rendered
from the same aggregates, and is the one place where the operator's LaTeX instinct is technically
correct.

**Open questions deferred to a later phase:** whether the `drive.file` grant persists for unattended
background re-reads (KC-1, spike before any build); whether the 100-user cap binds non-sensitive
Published apps (KC-2); whether snapshot persistence is permitted under Google APIs ToS section 5.e
(KC-9); the final name and domain (KC-12); the exact price points, which the reshape sets as $0 / $12
/ $39 / $99-team pending the concierge test's willingness-to-pay signal; and whether Robertson's
*How to Draw Charts and Diagrams* contains craft guidance that would amend the commandment set, which
remains unresearched and is the highest-value reading the operator can do personally.
