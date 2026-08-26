# dashero — what we worked out, in plain words

**Written 2026-08-26.** This is the readable version. The formal gate document is
`plans/ideation-dashero.md` (65 evidence rows, 12 failure modes, 15 stop-conditions) and the design
research is `plans/design-canon-notes.md` (18 rules for making charts good automatically). Read
those only if you want the workings. Everything that matters is here.

---

## The original idea

Connect a Google Sheet, get a good-looking dashboard automatically, share it at a link like
`dashero.com/yourname/sales`. Charts chosen for you based on what the data looks like. Talk to an AI
to improve them. Free for one sheet, paid after that.

## What we found out

We ran eight research agents over two days. Five were told to attack the idea. Three were told to
look for opportunities. Here is what came back, sorted by how much it matters.

### Google shipped most of this twelve days before we started

On 10 August 2026 Google launched "Sheets canvas". You type what you want in plain English and it
builds an interactive dashboard inside your spreadsheet, updating live, shareable like any sheet.

It is not available to free Gmail accounts, or to Business Starter, or Enterprise Starter. So there
is a gap — but the gap is "people on Google's cheapest tiers", and Google can close it whenever it
decides to.

### The name is already taken

`DASHERO` is a registered trademark in the European Union, owned by a Spanish company called Dashero
S.L., in the exact category that covers software. It covers 29 countries. `dashero.com` is owned by
someone else and parked for sale at an unknown price.

**The name has to change.** This costs nothing today and gets expensive later.

### Someone already built this exact thing and quietly killed it

Medium built "Charted" in 2014 — paste a Google Sheets link, get a good-looking chart that refreshes
every 30 minutes. They archived it in November 2018 without ever explaining why.

Looking at twelve dead products in this space, none of them died because their charts were ugly. They
died because this turns out to be a *feature* that big companies absorb, not a company. Google built
and killed two of these itself.

### The maths didn't work

- To get 40 paying customers you need roughly 8,000 visitors, based on real conversion figures from
  200 similar businesses. Adding up every realistic channel — Product Hunt, Hacker News, Reddit,
  search, cold email — gets you to about **4 paying customers**, not 40.
- The work adds up to **15–17 weeks** of full-time building. You have 6–8 weeks if you want any time
  left to sell.
- Letting strangers chat with an AI on a shared dashboard would have eaten your entire $20/month
  budget from **one** successful share.

### The good part

The research also found something genuinely valuable, and it is worth keeping regardless of what
gets built.

**Charts that write their own headline is an empty space.** A chart titled *"Revenue fell 12% in
March, the largest drop in two years"* is doing something almost no tool does. Datawrapper — the best
chart tool there is — makes you type that yourself. Power BI puts a paragraph in a side panel
instead. Tableau built it and switched it off in January 2025.

It costs almost nothing to build: one sentence template plus one calculation.

**But it only works if you know which direction is good.** Sales going up is good. Customer churn
going up is bad. Headcount going up is neither. A computer cannot tell from a column name, gets it
wrong roughly 40% of the time, and never knows it got it wrong. A green upward arrow on a churn chart
is worse than no chart at all.

**The fix is to ask.** One screen, fifteen seconds, at setup: *here's the table I found, here's the
header row, here's what each column is, and for each number — is up good or bad?* Two separate
research agents arrived at this same screen from completely different starting points, which is the
strongest signal we got all session.

---

## The second idea, and why it also got weaker

The research pointed at a different customer: **people who send the same report to a lot of people
every month.**

A marketing agency with 40 clients has to send each client a report. Today they either maintain 40
near-identical dashboards or paste screenshots into 40 PDFs. One agency owner: *"I have around 100ish
clients — the templates are just BS."* A factory analyst had the same problem with 50 production
lines.

The idea: keep everything in one sheet with a column saying who each row belongs to. Set up one
report. Get 40 links out. Each person sees only their own numbers with their own logo. Update the
sheet, press publish, all 40 update.

**Then we checked whether the market leader already does this. It does.**

AgencyAnalytics supports Google Sheets, does per-client reports, white-label branding, a client
portal, AI insights, and 85 other data connections. DashThis already advertises *"we don't charge per
client"* and costs $429/month for 50 dashboards, not the $800 we'd assumed.

So the price advantage is about 4×, not 16×, and you'd be offering far less for it.

---

## Who we'd be up against

| Who | What they do | What they earn | Price |
|---|---|---|---|
| AgencyAnalytics | Market leader. 85+ data sources including Sheets, per-client branded reports | **$15.7M/yr (Jul 2025). No outside money ever. 143 staff. Says 7,000+ agencies** | $20 per client/month |
| DashThis | Same job, charged per dashboard instead of per client | **$5.3M/yr (Nov 2023). No outside money. 40 staff. 2,600 customers** | $44 (3 dashboards) → $429 (50+) |
| Whatagraph | Same job, bigger customers | **$3.7M/yr (Oct 2024). Raised $9.6M. Staff cut from 105 to 63** | From ~€699/month |
| Looker Studio | Google's free version. Where agencies go when they stop paying | Free | $0 |

Three things worth noticing.

**The two biggest never raised money.** The one that raised $9.6M is the smallest and is shrinking.
This market rewards people who build cheaply, which suits you — but it also means the competition is
efficient rather than wasteful.

**DashThis publishes the numbers you'd plan against.** Average customer pays $135/month. Costs $450
to win one. So 3.3 months to break even. Around 3% of revenue leaves every month.

**Whatagraph loses about 40% of its customers a year.** Agencies do leave. That is the only opening
there is.

---

## What we would build, if we build

Not the original dashboard product. Something narrower:

**For agencies and freelancers whose client data already sits in a spreadsheet, and who don't need 85
advertising connectors.** One sheet, one setup, many branded links, every chart with its own plain
headline. Around $99/month flat.

**What it feels like to use:**

1. Pick your Google Sheet
2. Confirm what the tool found — the table, the header row, what each column means, and whether up is
   good or bad for each number. Fifteen seconds.
3. Point at the column that says who each row belongs to
4. Design one report — charts appear on their own, each with a written headline
5. Add a logo and a colour
6. Press publish, get one link per client
7. Next month: update the sheet, press publish again

That's it.

---

## Why we haven't started building

**Nobody has confirmed anyone will pay.** The strongest evidence for is that these people complain
constantly. The strongest evidence against is that when they get annoyed enough, they move to
something **free** — the clearest example we found was an agency shifting 80 clients onto free Looker
Studio. And every workaround we found in the wild is somebody choosing their own unpaid effort over a
subscription: screenshots pasted into PDFs, Apps Script cron jobs, running a headless browser to make
a PDF, a monthly copy-paste ritual between tabs.

A market whose defining habit is *doing it yourself for free* may admire this and never buy it.

**That is a one-week question, not a four-month one.** See `plans/outreach-draft.md`.

---

## The stop conditions we agreed, so they're not renegotiated later

- **Stop if** fewer than 5 people say they'd pay, out of roughly 50 contacted, by **12 September
  2026**. No code before this clears.
- **Stop if** fewer than 40 paying customers (or the revenue equivalent) by **25 December 2026**, or
  spend passes **$1,000** — whichever comes first.
- **Rename before** buying a domain or telling anyone the name.
- **Re-think entirely if** Google extends Sheets canvas to free accounts, or ships "publish this as a
  shareable page".

The whole value of writing these down now is refusing to move them later.

---

## What this cost, and what it saved

Two days, no code. The alternative was finding out about Sheets canvas, the trademark, the price of
the competition, and the 15-week build in month three of four.

Not building this is still a legitimate answer. It just needs to be a decision, not a drift.
