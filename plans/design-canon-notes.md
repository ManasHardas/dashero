# Design-canon notes — the received canon of information design, translated for dashero

**Status:** Wave -1 research artifact (Clause #11 adversarial ideation gate)
**Scope:** nine books, read for what they actually say and what a program can execute
**Date:** 2026-08-25

---

## How to read the confidence labels

Every attributed idea below carries one of three labels. This is a Clause #11 Rule 3 requirement,
and it is load-bearing: the dominant failure mode for this assignment is confidently inventing
plausible book content.

- **`SOURCED`** — I found the claim in a citable source and can point at it. Where I quote, the
  quotation was verified against a scan or PDF of the book itself, not a summary of it.
- **`WIDELY-ATTRIBUTED`** — well-established in the literature that this book contains this idea,
  corroborated across independent secondary sources, but not verified against the primary text.
- **`UNVERIFIED`** — I believe it but could not confirm it. Treat as a lead, not a fact.

**Never-invented-quotation rule:** every string in quotation marks below was pulled from a
retrieved source. Where I could not verify exact wording I paraphrase and say so.

### What I actually had access to

| Book | Access achieved | Quote confidence |
|---|---|---|
| *The Visual Display of Quantitative Information* | Full-text search of two scanned copies (Internet Archive `bwb_C0-AZE-209`, `bwb_W9-CRW-531`) | High — key quotes verified verbatim |
| *Envisioning Information* | **Complete 127-page PDF** | Highest — read directly, page-cited |
| *Visual Explanations* | Full 30-page chapter reprint (ch. 2) + full-text search of scan (`visualexplanatio0000tuft`) | High |
| *Beautiful Evidence* | Full-text search of scan (`beautifulevidenc0000edwa`) | High — all six principles verified verbatim |
| *A Practical Guide to Designing with Data* (Suda) | **Complete book text** | Highest — read directly |
| *Design for Information* (Meirelles) | Full-text search of scan (`designforinforma0000meir`) + her own 2010 paper in full | Medium-high — phrase-level verification only |
| *Information Graphics* (Rendgen) | Full-text search of scan (`informationgraph0000rend`) + publisher page + two author interviews | Medium |
| *The Secret Language of Maps* (Carter) | Published book excerpt (SSIR) + long author interview (Stamen) | Medium |
| *How to Draw Charts & Diagrams* (Robertson) | **Publisher/catalogue description only** | **Low — see honest finding below** |

---

# PART 1 — Per-book notes

## 1. Edward Tufte, *The Visual Display of Quantitative Information* (1983/2001)

**Core premise.** Statistical graphics are instruments of reasoning about quantitative information,
and they are held to the same standards of integrity as any other evidence. Excellence is the
well-designed presentation of *interesting data* — a matter of substance first, statistics second,
design third. Most graphical failures are failures of honesty or of nerve, not of taste.

**Most important specific ideas.**

- **Data-ink ratio.** Data-ink is the non-erasable core of a graphic. The prescription is a five-step
  editing loop: *"Above all else show the data. Maximize the data-ink ratio. Erase non-data-ink.
  Erase redundant data-ink"* — each qualified *"within reason"* — and then *"Revise and edit."*
  `SOURCED` (verified verbatim in scan). Note the *"within reason"* qualifier; it is routinely
  dropped by people citing Tufte, and dropping it is how the principle becomes a fetish.
- **Lie factor.** `Lie Factor = (size of effect shown in graphic) / (size of effect in data)`.
  `SOURCED` (formula verified verbatim). The commonly cited acceptable band of 0.95–1.05 is
  `WIDELY-ATTRIBUTED` — I verified the formula and the "equal to one" framing, not the band.
- **Graphical integrity, principle 1.** *"The representation of numbers, as physically measured on
  the surface of the graphic"* must be directly proportional to the quantities represented.
  `SOURCED` (opening clause verified verbatim).
- **"Show data variation, not design variation."** `SOURCED` (verified verbatim). This is the single
  most machine-relevant sentence in the book: it says the visual system must be held constant so
  that everything that moves is data.
- **Chartjunk and "the duck."** Decoration that carries no data — moiré vibration, heavy grids,
  and graphics distorted into illustrations. `WIDELY-ATTRIBUTED` for VDQI specifically; the "duck"
  argument is quoted at length from Venturi in *Envisioning Information* p. 33 `SOURCED`.
- **Aspect ratio.** *"Graphics should tend toward the horizontal, greater in length than height."*
  `SOURCED` (verified verbatim). The frequently repeated "about 50% wider than tall" gloss is
  `WIDELY-ATTRIBUTED`.
- **Graphical excellence** gives the viewer *"the greatest number of ideas in the shortest time with
  the least ink in the smallest space."* `SOURCED` (verified across many citing works).

**What it is for that the others are not.** VDQI is the integrity book. It is the only one of the
nine that gives you a *number* you can compute and assert against (the lie factor). For a product
that renders charts without a human in the loop, this is the book that supplies the test suite.

**Operationally actionable for software.** Extremely. Proportional-ink is a checkable invariant.
Lie factor is computable. "Show data variation, not design variation" is a rule about holding the
render config constant across a series. The data-ink editing loop is a list of DOM elements to
not emit.

---

## 2. Edward Tufte, *Envisioning Information* (1990)

**Core premise.** All information display happens on a two-dimensional surface, and the central
craft problem is escaping that flatland — representing high-dimensional, dense, complex information
without producing noise. Complexity is not the enemy; clutter is, and clutter is a design failure,
never a property of the data.

Chapters, verified from the book itself `SOURCED`: *Escaping Flatland; Micro/Macro Readings;
Layering and Separation; Small Multiples; Color and Information; Narratives of Space and Time.*

**Most important specific ideas.**

- **"Confusion and clutter are failures of design, not attributes of information."** (p. 53)
  `SOURCED` — read directly. The follow-on is the operative part: find design strategies that reveal
  detail, *"rather than to fault the data for an excess of complication. Or, worse, to fault viewers
  for a lack of understanding."*
- **The 1 + 1 = 3 effect** (borrowed from Josef Albers). Two marks produce a third, unplanned visual
  artifact in the negative space between them. *"Most of the time, that surplus visual activity is
  non-information, noise, and clutter."* (p. 61) `SOURCED`. And critically, the quantitative version:
  *"The noise of 1 + 1 = 3 is directly proportional to the contrast in value (light/dark) between
  figure and ground. On white backgrounds, therefore, a varying range of lighter colors will minimize
  incidental clutter."* (p. 62) `SOURCED`. **This is a directly implementable rule, and it is also the
  one place the canon is provably theme-dependent — see Part 5.**
- **Four fundamental uses of colour**: *"to label (color as noun), to measure (color as quantity),
  to represent or imitate reality (color as representation), and to enliven or decorate (color as
  beauty)."* (p. 81) `SOURCED`. Preceded by the first principle of colour in information design:
  *"Above all, do no harm."* `SOURCED`.
- **Imhof's colour rules**, quoted approvingly (p. 82) `SOURCED`. First rule: pure, bright or very
  strong colours *"have loud, unbearable effects when they stand unrelieved over large areas adjacent
  to each other, but extraordinary effects can be achieved when they are used sparingly on or between
  dull background tones."* Second rule: light, bright colours mixed with white placed next to each
  other usually produce unpleasant results, especially over large areas. Tufte's constructive gloss:
  *"color spots against a light gray or muted field highlight and italicize data."* (p. 83) `SOURCED`.
- **Small multiples.** *"At the heart of quantitative reasoning is a single question: Compared to
  what?"* and the design consequence: *"Constancy of design puts the emphasis on changes in data, not
  changes in data frames."* Panels are *"positioned within the eyespan, so that viewers make
  comparisons at a glance."* (p. 67) `SOURCED`.
- **Micro/macro readings.** Overview and detail in the same graphic, at different reading distances.
  *"In all these micro/macro designs, the same ink serves more than one informational purpose;
  graphical elements are multifunctioning."* (p. 46) `SOURCED`.
- **On chartjunk and contempt.** *"If the numbers are boring, then you've got the wrong numbers."*
  (p. 34) `SOURCED`. And: *"the operating moral premise of information design should be that our
  readers are alert and caring."* `SOURCED`.

**What it is for that the others are not.** This is the *composition* book — how multiple things
coexist on one surface without fighting. For a dashboard product (many charts, one page) it is the
most directly relevant Tufte volume, and it is the one people skip.

**Operationally actionable for software.** The most, of the four Tuftes. 1+1=3 becomes stroke-weight
and opacity rules. Imhof becomes a palette policy (saturated = small areas only; large fills muted).
Small multiples becomes a faceting threshold with shared scales. Micro/macro becomes the dashboard
layout itself.

---

## 3. Edward Tufte, *Visual Explanations* (1997)

**Core premise.** Where VDQI is about nouns (quantities), this is about verbs — mechanism, motion,
process, cause and effect. Its central claim is that displaying evidence is an act with consequences,
and that a display can be *correct in its data and still fail catastrophically* if it does not
display the causal structure.

Chapter list partially verified `SOURCED`: *Images and Quantities; Visual and Statistical Thinking;
Explaining Magic; Instructions and Disinformation Design (p. 55); The Smallest Effective Difference
(p. 73); Parallelism: Repetition and Change.*

**Most important specific ideas.**

- **The Snow / Challenger pairing.** John Snow's cholera map as the triumph; the Challenger pre-launch
  charts as the catastrophe. Snow's method, as Tufte lists it, begins:
  *"1. Placing the data in an appropriate context for assessing cause and effect."* `SOURCED`
  (read directly from the chapter reprint).
- **"The passage of time is a poor explanatory variable."** `SOURCED`. Tufte's point is that a
  chronology of an epidemic is *description*, not *explanation* — *"descriptive narration is not
  causal explanation."* **For a product whose default move is "there's a date column, make a time
  series," this is the sharpest warning in the entire canon.**
- **"Numbers become evidence by being in relation to."** `SOURCED`. The Challenger analysts plotted
  only the launches *with* O-ring damage, omitting the damage-free launches — *"The flights without
  damage provide the statistical leverage necessary to understand the effects of temperature."*
  In the Snow map, the cholera-free workhouse and brewery are what Tufte calls *"those essential
  compared-with-what cases."* `SOURCED`.
- **"They had the correct theory and they were thinking causally, but they were not displaying
  causally."** `SOURCED`. The most important sentence in the book for this project.
- **Ordering by the suspected cause.** Tufte's corrected Challenger table is *"ordered by the possible
  cause, temperature, from coolest to warmest launch"* `SOURCED` — versus the originals, which were
  ordered by flight number.
- **Ordinal scales must be encoded monotonically.** Of a post-accident chart: *"the scale's visual
  representation is disordered: the cross-hatching varies erratically from dark, to light, to medium
  dark, to darker, to lightest — a visual pattern unrelated to the substantive order of the measured
  scale."* And on legends: *"A letter-code accompanies the cross-hatching. Such codes can hinder
  visual understanding."* `SOURCED`.
- **The smallest effective difference.** *"Make all visual distinctions as subtle as possible, but
  still clear and effective"*; it is *"the Occam's razor"* of information design. `SOURCED`
  (verified verbatim in scan, ch. 4, p. 73).

**What it is for that the others are not.** This is the *causality and consequences* book. It is
the only one that argues, with a body count, that choosing the wrong comparison is a moral failure
and not a stylistic one.

**Operationally actionable for software.** Partly, and the part that isn't is the whole product
problem. "Order by the suspected cause" is implementable. "Don't filter out the zero cases" is
implementable. "Encode ordinal data monotonically" is implementable. *"Display causally"* is not
implementable, because the machine does not know what causes what. See Part 4.

---

## 4. Edward Tufte, *Beautiful Evidence* (2006)

**Core premise.** How seeing turns into showing. Evidence is evidence regardless of medium — words,
numbers, images, diagrams — and it should be assessed by one consistent standard. The book's
contribution is to state, finally and explicitly, a short list of principles for analytical design,
derived by reverse-engineering Minard's 1869 map of the Russian campaign.

**The six principles of analytical design.** All six verified verbatim against a scan of the book
`SOURCED`:

1. **"Show comparisons, contrasts, differences."** With the gloss: *"The fundamental analytical act
   in statistical reasoning is to answer the question 'Compared with what?'"*
2. **"Show causality, mechanism, explanation, systematic structure."**
3. **"Show multivariate data; that is, show more than 1 or 2 variables."**
4. **"Completely integrate words, numbers, images, diagrams."**
5. **Documentation** — thoroughly describe the evidence: provenance, authorship, sources, scales,
   measurement, so the display can be assessed and trusted. (Verified as principle 5 by position;
   exact wording of the imperative not verified — treated as `WIDELY-ATTRIBUTED`.)
6. **"Analytical presentations ultimately stand or fall depending on the quality, relevance, and
   integrity of their content."** `SOURCED` verbatim.

**Other important ideas.**

- **Sparklines.** *"Sparklines are datawords: data-intense, design-simple, word-sized graphics."*
  `SOURCED` verbatim from the book. Word-height, typographic resolution, embedded inline with the
  number they contextualize, no axes or decoration. (Specific pixel dimensions circulating online —
  e.g. "14–20px tall" — I found only in derived/secondary material and treat as `UNVERIFIED`.)
- **"The Cognitive Style of PowerPoint,"** pp. 156–185. `SOURCED`. Argument: the medium's templated,
  low-resolution, hierarchical-bullet format degrades evidence and the reasoning that depends on it.
  **A dashboard is structurally the same object as a slide deck — templated, low-resolution, one
  metric per tile, stripped of context. This chapter is a critique of dashero's product category
  and should be read as such.**

**What it is for that the others are not.** It is the only one that states a checklist. Principles
1–3 are Axis A (what to show); principles 4–5 are Axis B and provenance; principle 6 is the
arbitration rule between them.

**Operationally actionable for software.** Principles 1, 3, 4, 5 are all mechanizable to a useful
degree. Principle 2 is not. Principle 6 is the acceptance criterion, not a rule.

---

## 5. Isabel Meirelles, *Design for Information* (Rockport, 2013)

**Core premise.** Rather than organizing the field by chart type, organize it by the *structure of
the information* — because the structure determines which visual encodings are legitimate. The
visualization process is grounded in design, cognition, perception and HCI, not in aesthetic
preference.

**Structure** (verified from the book's own contents page `SOURCED`): six chapters —
*Hierarchical Structures: Trees; Relational Structures: Networks; Temporal Structures: Timelines and
Flows; Spatial Structures: Maps; Spatio-temporal Structures; Textual Structures*, plus an
*Appendix: Data types*.

**Most important specific ideas.**

- **Encoding must be congruent with the data's structure, or it misleads.** From the book, verified:
  *"...the corresponding visual encoding. If that is not the case, then the visual encoding is
  unsuitable and could be misleading. As Ware explains..."* `SOURCED` (phrase-level verification;
  I could not retrieve the full surrounding sentence). This is the load-bearing claim of the book
  and it is a *bridge claim*: it says Axis A (what the data is) constrains Axis B (how it may be
  drawn). It is not a taste rule; it is a validity rule.
- **"Assigning visual encoding to abstract data is a crucial step"** — verified phrase `SOURCED`.
  The context is that abstract data, unlike physical phenomena, *"[doesn't] provide visual cues,"*
  so the encoding is a designed act with no natural referent to fall back on.
- **Every case study is annotated with a structured "DATA TYPE AND VISUAL ENCODING" breakdown**
  — verified `SOURCED`; retrieved instances show fields including *Categorical: … Encoding: …*,
  *Temporal: … Encoding: …*, *Quantitative: … Encoding: …*. **This is, almost literally, a schema
  for a chart-inference engine's intermediate representation, and I'd copy it.**
- **Gestalt laws** are treated as the perceptual foundation for grouping and organization —
  verified that the book discusses *"a series of principles—known as the Gestalt laws"* `SOURCED`.
- **Cognitive function of graphic displays.** From Meirelles' own 2010 paper (read in full, so
  `SOURCED`, though this is the paper not the book): displays are *cognitive artefacts*, and the
  cognitive principles underlying them are *"to record information; to convey meaning; to increase
  working memory; to facilitate search; to facilitate discovery; to support perceptual inference;
  to enhance detection and recognition; and to provide models of actual and theoretical worlds."*
  She attributes this to Norman (1993), Card et al. (1999), Ware (2004). She also adopts Card's
  definition of visualization as *"the use of computer-supported, interactive, visual representations
  of abstract data to amplify cognition."*

**What it is for that the others are not.** It is the *taxonomy* book, and it is the only one of the
nine grounded in the perception/cognition literature (Bertin, Ware, Card, Norman) rather than in the
author's own connoisseurship. Tufte asserts; Meirelles cites.

**Operationally actionable for software.** The most structurally useful of the nine. Her
structure-first taxonomy maps directly onto the inference problem dashero actually has: *given an
unknown table, what kind of thing is this?* Tree / network / temporal / spatial / spatio-temporal /
textual is a better first branch than "bar or line?"

**Honest limitation:** I verified her book at phrase level only, not paragraph level. I could not
retrieve her encoding-recommendation tables in full, and I do not know exactly which encodings she
recommends for which data type. Treat the taxonomy as `SOURCED` and any specific encoding
recommendation I might attribute to her as `UNVERIFIED`. Anything about encoding *accuracy ordering*
below comes from Cleveland & McGill, not from her.

---

## 6. Brian Suda, *A Practical Guide to Designing with Data* (Five Simple Steps, 2010)

*(The operator's list says "Designing with Data"; this is the book — Five Simple Steps, 2010,
foreword by Jeremy Keith. I read the complete text.)*

**Core premise.** A working web designer's translation of the statistical-graphics tradition into
screen practice, organized around a single conviction: charts exist to tell the story in the data,
and almost every default produced by standard software actively obstructs that. It is deliberately
practical and deliberately opinionated.

**Structure** `SOURCED` — five parts, 21 chapters: *The visual language of data* (Graph genesis;
Chart literacy; Dynamic and static charts; Does this make me look fat?; Chart junk) · *Colour and ink*
(Data to pixel ratio; How to draw attention to the data; Rasterization ain't got those curves; Just a
splash of colour; In Rainbows) · *How to deceive with data* (Trompe l'œil; Relative versus absolute;
Sins of omission; Caught red-handed: the problem of false positives; Fudge factor) · *Common types of
charts* (Line; Bar; Area; Pie; Scatter) · *Not so common charts* (Maps, choropleths and cartograms;
Radar plots; …).

**Most important specific ideas.** All of the following read directly from the book text, `SOURCED`:

- **Data-to-pixel ratio.** His explicit port of Tufte to screens: *"On screen, we're not dealing with
  ink. Instead, we can think of this value as a data to pixels ratio. How many unnecessary pixels
  were displayed to convey the message?"*
- **Four mechanisms for drawing attention** — an unusually implementable list:
  1. **Colour** — *"Using a single colour within a black and white bar graph calls attention to that
     information without the need for extra labels."* And the key constraint: *"When each piece of
     the chart is a different colour, then the impact of any individual colour is lost."*
  2. **Intensity** — vary brightness/lightness/transparency within one hue; *"If the other bars are
     lighter they will fall away into the background; they remain visible for comparison if needed,
     but the main value has focus."*
  3. **Weight** — thicker stroke for the focal series. With a warning that matters:
     *"changing an item's weight might indicate something other than straightforward emphasis…
     It is important to change the weight of a variable only when it won't be mistaken for another
     factor."*
  4. **Position / white space** — deliberate gaps create perceptual groups.
- **Bar vs. line is a data-type decision, not a style decision.** A line implies every intermediate
  point has a value; a bar models discrete values, *"which is why there is normally a space between
  the bars."* Consequently: *"With bar charts, order is not necessarily important… With a line graph,
  the correct order is essential since the data represented is continuous."*
- **Pie charts.** He is hostile and specific: *"The most effective pie charts comprise only two items…
  If we introduce more than two wedges, the eye must rotate at least one of the wedges to a cardinal
  point to figure out the percentage value."* Once you must label both category *and* value,
  *"you have pretty much recreated some tabular data with an ugly dot in the middle."* Also the
  validity check: a pie's values *"must represent all the answers for a single question"* — his
  worked example is three separate yes/no poll questions wrongly combined into one pie exceeding 100%.
  Doughnut charts he rejects outright: removing the centre *"further hinders the ability to judge the
  weight of each segment."*
- **3D is disqualifying.** Perspective makes equal wedges unequal: *"wedges 1 and 4 are identical in
  value, but you'd never know that because of the perspective."*
- **Never move the origin.** *"Even though our goal is to remove unnecessary pixels, we mustn't
  sacrifice understanding… the scale must remain anchored and consistent."*
- **Colour vision deficiency** — a whole chapter, and *the only substantive accessibility treatment
  in the entire nine*. ~8% of males have some form of colour blindness; *"instead of referring to
  'the red line' you can change the thickness or add shapes."* Redundant encoding, stated plainly.
- **Precision error as a data-quality signal.** *"An indication that the data is not statistically
  sound is when it is almost too precise."* $127.86/week is less trustworthy than $130/week.
- **Aspect ratio** — and here he is weak. His chapter offers the golden ratio, Fibonacci, 3:2, 4:3,
  16:9, and the silver ratio, concluding *"There is no correct answer as to what proportions are
  best."* This is aesthetic convention, and it is **not** the perceptual answer. See the note on
  banking-to-45° in Part 2B.
- **On story.** *"Designing with data needs to be about clarity in the story. Sometimes you need some
  characters to stand out and others to play a supporting role, but both are important in advancing
  the plot."*

**What it is for that the others are not.** It is the only one of the nine written *for screens, by
someone shipping software*, and the only one that treats accessibility as a first-class concern.
It is also the least intellectually ambitious, which is exactly why it is the most immediately
useful: it is nearly a spec.

**Operationally actionable for software.** Highest of the nine. Large parts of it can be transcribed
into code with very little interpretation.

---

## 7. Bruce Robertson, *How to Draw Charts & Diagrams* (North Light Books, 1988; DIANE reprint 1999)

### Honest finding: I could not research this book deeply.

**Limited public material found.** This is the one book of the nine for which I could establish
almost nothing beyond catalogue metadata. Here is exactly what I could and could not establish.

**What I could establish** `SOURCED`:
- Bruce Robertson (1934–2014), ARCA. 192 pages. North Light Books, Cincinnati, 1988;
  ISBN 0891342427. Reprinted by DIANE Publishing, 1999, ISBN 0788163531.
- Publisher/catalogue description: the book teaches evaluating data, selecting an appropriate
  visualization style, and *executing the artwork* in physical media — *"colored pencil, markers,
  and airbrush techniques."* It covers graphs, pie charts, maps and bar charts, with many examples
  of effective and ineffective approaches.
- Its framing premise, from the catalogue copy: *"Communicating raw data through diagrams and charts
  is an exciting alternative to communicating through words."*
- Robertson also wrote *Learn to Draw Charts and Diagrams Step-by-Step* (Macdonald, 1987) — a
  closely related companion title — and *Fantasy Art*, plus several drawing workbooks. His author
  bio in *Fantasy Art* identifies him as *"the author of How to Draw Charts and Diagrams and four
  drawing workbooks."* `SOURCED`

**What I could NOT establish:**
- Any chapter list or table of contents.
- Any specific design rule, principle, or named concept from the book.
- Any substantive review, academic engagement, or excerpt. The only academic reference I located
  was a bare bibliographic citation in a curriculum guide.
- Any verified quotation from the body text.

**Queries run** (all returned only catalogue/retail metadata or unrelated matches):
`"How to Draw Charts and Diagrams" Robertson North Light 1988 review contents` ·
`"How to Draw Charts and Diagrams" Robertson "table of contents" chapters library catalog` ·
Google Books API lookup on volume IDs `toIGAAAACAAJ` and `cWlYAAAAYAAJ` (both returned empty
volumeInfo) · Internet Archive advanced search on `title:(charts and diagrams) AND creator:(Robertson)`
(returned only the 1987 companion title, not this book) · Open Library full-text search on
`"How to draw charts and diagrams" Robertson` (returned only third-party citations *to* it, confirming
the book itself is not in the full-text corpus).

**Assessment of its likely role in the canon, clearly labelled `UNVERIFIED`.** Based on the period
(1988), the publisher (North Light — a practical art-instruction house, not an academic press), the
page count, and the emphasis on airbrush and marker rendering, this is almost certainly a *studio
production manual* from the pre-desktop-publishing era: how a working graphic artist physically makes
a chart look professional. If so, its value to the canon is as the **craft/pictorial counterweight to
Tufte** — the tradition that assumes a chart is an illustration to be rendered well, not a statistical
instrument to be stripped bare. That is a real and useful position, and it is genuinely adjacent to
Rendgen's territory.

**But I want to be explicit: I am inferring that from the book's metadata, not from its contents.**
I have not read a single sentence of its argument. **No commandment below is traced to Robertson**,
and none should be until someone reads the book. If the operator has a copy, it is the single
highest-value thing he could read and report back on, precisely because it is the one book here
that might disagree with Tufte from a craft direction rather than a journalistic one.

---

## 8. Carissa Carter, *The Secret Language of Maps* (Stanford d.school / Ten Speed Press, 2022)

**Core premise.** A "map" is anything where information is organized spatially and presented
visually — so infographics, frameworks and diagrams are all maps. Every map is an argument made by
a person, carrying that person's bias, and reading maps critically is *"an essential skill for an
informed society."* The book teaches a framework for deconstructing any map and then for making one.

**Most important specific ideas.**

- **The three-part framework: Data, Bias, Craft.** `SOURCED` (author interview, corroborated by the
  published excerpt).
  - **Data** is *"your raw material"* — but explicitly not neutral. Her formulation:
    *"Don't ask the data. It can't talk. People are the talkers."* `SOURCED`. The questions to ask of
    it are selection questions: what was collected, what wasn't, what was left out, how it was
    organized.
  - **Bias** is *"your preference… shaped by your perspective… born from your culture, your lived
    experiences, and your current context."* `SOURCED`. Notably she treats bias as a neutral,
    unavoidable force to be surfaced — not a defect to be eliminated.
  - **Craft** is *"the skin on your data, the house for your frameworks, the frontwoman for your big
    ideas."* `SOURCED`.
- **"Viewers don't know the difference between intention and default."** `SOURCED`.
  **This is the single most important sentence in the canon for this product**, and I would put it
  at the top of the engineering README. Every default dashero ships — every colour, every sort order,
  every axis range — will be read by a viewer as an editorial choice the creator made. There is no
  such thing as a neutral default in a published artifact.
- **Deconstructing a map for bias — three elements to attend to** `SOURCED` (from the published
  excerpt): the **viewer's reaction** (what does it evoke, and why); the **creator's intent** (is
  there an agenda; who is the target); and the **bias "cloud"** (is the bias explicit or implicit,
  harmful or harmless, hidden or announced).
- **Explicit vs. implicit bias.** Explicit biases are intentional choices; implicit ones are automatic,
  operating *"as muscle memory."* Her example: *"Always making female things pink and male things blue
  shows an implicit bias."* `SOURCED`. Machine defaults are pure implicit bias, industrialized.
- **Explore before explain.** Iterative, hands-on manipulation of the information before committing
  to an explanation. `SOURCED`.
- **Two creators, same data, different maps.** Meaning is not in the data; it is in the decisions
  about inclusion, exclusion and emphasis. `SOURCED`.

**What it is for that the others are not.** It is the only one of the nine that is fundamentally about
**subjectivity and authorship** rather than accuracy or clarity. Tufte's implicit model is that there
is a correct display and the designer's job is to find it. Carter's model is that there is no view
from nowhere, so the designer's job is to *own* the view and disclose it. These are genuinely
different epistemologies, and for an AI-generated product Carter's is the more honest one.

**Operationally actionable for software.** Indirectly but profoundly. It doesn't give you rules; it
gives you a *disclosure obligation* and a UX consequence: surface the choices the machine made, and
make them editable. That is a feature spec, not a style rule.

---

## 9. Sandra Rendgen (ed.), *Information Graphics* (Taschen, 2012)

**Core premise.** Information graphics are a continuous 1,200-year practice, not a recent trend, and
the contemporary explosion is one more chapter in a long history of visual sense-making. The book is
a curated compendium — argument by exhibition rather than by doctrine.

**Structure** `SOURCED`: 464 pages, ~400+ graphics. Two parts. (1) An illustrated introductory
section with essays by Rendgen, Paolo Ciuccarelli, Richard Saul Wurman and Simon Rogers, tracing the
form from prehistory to the present. (2) 200 contemporary projects, each with a fact sheet and an
explanation of method and goals, organized into four topic chapters: **Location, Time, Category,
Hierarchy.**

Her introduction opens: *"Data are the new raw material."* `SOURCED` (verified from a scan of the book).

**Most important specific ideas.**

- **The four-way organizing schema — Location / Time / Category / Hierarchy** `SOURCED`. Note how
  closely this rhymes with Meirelles' structure-first taxonomy, arrived at independently and from a
  curatorial rather than cognitive direction. **Two of the nine books converge on "classify by the
  shape of the information, not by the shape of the chart." That convergence is a strong signal.**
- **Complexity and clarity must be held in tension.** Infographics demand *"not only creative skills,
  but also analytical thinking"*; a successful one has *"a clear focus"* where *"the key message must
  be accessible quickly, in a clear visual structure."* `SOURCED` (author interview).
- **Accuracy is non-negotiable.** Verifying *"correct data and dimension units"* and ensuring
  *"proportions depicted properly"* are *"absolutely indispensable."* `SOURCED`. Rendgen is **not** a
  permissive aesthete; she holds the proportional-ink line as firmly as Tufte does.
- **But design is what earns the reading.** *"It is the design that makes us want to look at the
  data."* `SOURCED`. **This is the cleanest one-sentence statement of the position Tufte rejects,
  from a serious person, and it is the crux of the disagreement in Part 2.**
- **Storytelling as craft skill.** On Minard, she describes how he *"had evolved some sort of
  storytelling skills"* and *"streamlined"* a complex military catastrophe into a coherent narrative
  through visual form. `SOURCED`. Note that this is the *same graphic* Tufte uses to derive his six
  analytical principles — and she reads it as a **narrative** achievement where he reads it as an
  **analytical** one. The canon's central disagreement is visible in two readings of one map.
- **Historiographic corrective.** The received history is too thin; the famous figures *"are just
  sort of the icebergs looking out of the ocean, but there's so much more."* `SOURCED`.

**What it is for that the others are not.** It is the *evidence base* — the corpus. Its function in
the canon is to prove, by 400 counterexamples, that the space of legitimate information graphics is
far larger than the statistical-graphics tradition admits.

**Operationally actionable for software.** Least directly of the nine. It contains no rules. Its use
to dashero is as a **reference library for what "visually stunning" actually looks like**, and as the
empirical basis for arguing against over-fitting to Tufte.

**Honest limitation:** I verified structure, the opening line of the introduction, and Rendgen's
views from two interviews. I did **not** read the introductory essays. Any claim about what
Ciuccarelli, Wurman or Rogers argue in this book would be invention, so I make none.

---

# PART 2 — The two axes, held separately

The operator was right that these are different questions, and the canon supports the distinction
more sharply than most contemporary writing does.

## Axis A — WHAT data is shown

**The canon's position, in one sentence:** a graphic's job is to make a *comparison* that supports a
*judgment*, and choosing the wrong comparison is an error that no amount of rendering can repair.

**Where the canon agrees.**

1. **Comparison is the primitive.** Tufte states it three separate times across three books:
   *"The fundamental analytical act in statistical reasoning is to answer the question 'Compared
   with what?'"* (BE, principle 1); *"At the heart of quantitative reasoning is a single question:
   Compared to what?"* (EI p. 67); *"Numbers become evidence by being in relation to"* (VE).
   All `SOURCED`. **A number with no comparison is not evidence. This is the most repeated claim in
   the entire corpus and should be dashero's first gate.**
2. **Include the cases that didn't happen.** The Snow workhouse and brewery; the Challenger
   damage-free launches. Filtering to the interesting rows destroys the leverage that makes the
   pattern visible. `SOURCED`.
3. **Time is a weak explanatory variable.** *"descriptive narration is not causal explanation; the
   passage of time is a poor explanatory variable, practically useless in discovering a strategy of
   how to intervene."* `SOURCED`. Tufte's remedy is to order by the *suspected cause* instead.
4. **Multivariate is the normal case.** BE principle 3; VDQI's "graphical excellence is nearly always
   multivariate." Univariate displays are usually an admission of failure to gather context.
5. **Provenance is part of the data.** BE principle 5. Rendgen independently: units and proportions
   are *"absolutely indispensable."* Suda independently: over-precision is a *symptom of unsound
   data*. Three of the nine, from three traditions, converge on "document the evidence."
6. **Selection is authorship.** Carter: what was collected, what wasn't. Tufte: "graphics must not
   quote data out of context." Same claim from opposite ends of the field.
7. **Structure before chart type.** Meirelles (cognitive) and Rendgen (curatorial) independently
   organize the field by the *shape of the information* — hierarchical / relational / temporal /
   spatial / textual, and location / time / category / hierarchy. Neither organizes by "bar, line,
   pie." **The canon says the first question is "what kind of thing is this data," not "which chart."**

**Where the canon disagrees with itself on Axis A.**

- **Is there a correct comparison, or only an owned one?** Tufte's entire Challenger argument assumes
  there *was* a right display and the engineers failed to find it. Carter's position is that meaning
  is never in the data — *"Don't ask the data. It can't talk"* — and that two honest people will make
  two different maps from one table. These are not reconcilable by hand-waving. Tufte is a realist
  about displays; Carter is a constructivist. **For dashero this matters concretely: Tufte's framing
  implies the machine should try to find the right chart; Carter's implies the machine should
  surface its choice and hand the authorship to the user.** I think Carter is right about what is
  *achievable* and Tufte is right about what is *at stake*.
- **How much should be shown at once?** Tufte pushes maximum data density and multivariate richness.
  Rendgen requires that *"the key message must be accessible quickly, in a clear visual structure"* —
  a focus constraint that trades density away. Suda sides with Rendgen operationally.

**Where the canon is silent on Axis A.** Nothing in these nine books tells you how to *infer* what
matters from an unlabelled table. Every one of them presumes an author who already knows the point.
That is precisely the gap dashero must fill, and the canon offers no help. See Part 4.

## Axis B — HOW it is shown

**The canon's position, in one sentence:** hold the visual system constant so that everything which
varies is data; spend contrast only where it buys a distinction; and let the encoding be dictated by
the data's structure rather than by preference.

**Encoding accuracy.** The canon books do not themselves supply the perceptual ranking — Meirelles
points at it via Bertin and Ware, but the empirical result belongs to **Cleveland & McGill (1984)**,
*JASA* 79(387):531–554, `WIDELY-ATTRIBUTED` with citation. Their ordering of elementary perceptual
tasks, most to least accurate: **position along a common scale → position along non-aligned identical
scales → length → direction → angle → slope → area → volume → shading → colour saturation.** Replicated
by Heer & Bostock (2010) via crowdsourcing. Mackinlay extended it to ordinal and nominal data in APT.
**This is the backbone of any automated encoding decision and it comes from outside the nine books —
worth flagging, since the operator's list has no perception title in it.**

**Where the canon agrees.**

1. **Erase what isn't data — within reason.** Tufte's data-ink loop; Suda's data-to-pixel port.
   Both explicitly qualified. `SOURCED`.
2. **Smallest effective difference.** *"Make all visual distinctions as subtle as possible, but still
   clear and effective."* Corollary that Tufte states directly: when everything is emphasized,
   nothing is. `SOURCED`. Suda reaches the identical conclusion from practice: *"When each piece of
   the chart is a different colour, then the impact of any individual colour is lost."* `SOURCED`.
   **Two books, independent routes, same rule. High confidence.**
3. **Layering by visual weight.** EI ch. 3. Data darkest, structure lighter, decoration lightest or
   absent. Avoid 1+1=3 by never placing two heavy elements adjacent.
4. **Colour is for labelling, measuring, imitating, or enlivening — and above all, do no harm.**
   Imhof's rules as Tufte transmits them: saturated colour only on small areas, against muted or grey
   fields; avoid adjacent light-bright-plus-white over large areas. `SOURCED`.
5. **Direct labelling over legends.** BE principle 4 (*"Completely integrate words, numbers, images,
   diagrams"*); VE on letter codes (*"Such codes can hinder visual understanding"*). `SOURCED`.
6. **Small multiples with constant frames.** *"Constancy of design puts the emphasis on changes in
   data, not changes in data frames."* `SOURCED`.
7. **Ordinal data requires monotonic encoding.** VE's critique of cross-hatching that varies
   *"erratically… unrelated to the substantive order of the measured scale."* `SOURCED`.
8. **Proportional ink; no 3D.** VDQI's integrity principle 1; Suda's demonstration that perspective
   makes identical wedges look different. `SOURCED` in both.
9. **Redundant encoding for accessibility.** Suda alone, but unambiguous: don't rely on hue; add
   thickness or shape. `SOURCED`.

**Where the canon disagrees with itself on Axis B. This is the live one.**

**Tufte's minimalism vs. the pictorial/narrative tradition.** This is a real disagreement between
serious people and it should not be smoothed over.

- **Tufte's position:** decoration is not neutral; it is evidence of contempt. *"Lurking behind
  chartjunk is contempt both for information and for the audience… If the numbers are boring, then
  you've got the wrong numbers."* (EI p. 34) `SOURCED`. Decoration also *costs credibility* —
  *"who would trust a chart that looks like a video game?"* `SOURCED`. Suda follows him faithfully.
- **Rendgen's position:** *"It is the design that makes us want to look at the data."* `SOURCED`.
  Attention is a precondition, not a vanity. Her 400-graphic corpus is the argument.
- **Carter's position:** craft is *"the frontwoman for your big ideas"* — the vessel is not separable
  from the message. `SOURCED`.
- **The same artifact, read two ways:** Tufte derives six austere analytical principles from Minard's
  1869 map. Rendgen reads the same map as evidence of *storytelling* skill and *streamlining*.
  Both `SOURCED`. They are looking at one graphic and seeing different achievements.
- **And the empirical evidence favours the pictorial side on one specific dimension.** Bateman et al.,
  CHI 2010, *"Useful Junk? The Effects of Visual Embellishment on Comprehension and Memorability of
  Charts"*: comprehension accuracy for embellished (Holmes-style) charts was **no worse** than for
  plain charts, and **recall after a two-to-three-week gap was significantly better.** The authors
  explicitly decline to generalize it into a design rule, warning that strong imagery can bias
  interpretation. `SOURCED`. **This is a measured result that contradicts a strong reading of the
  data-ink doctrine, and dashero should know it exists.**

**Where the canon is thin or wrong on Axis B.**

- **Aspect ratio is the clearest case of the canon being weaker than the literature.** Tufte gives a
  direction (*"tend toward the horizontal"*) `SOURCED`. Suda gives aesthetic conventions and concedes
  *"There is no correct answer."* `SOURCED`. Neither mentions **banking to 45°** — Cleveland's result
  that a line chart's aspect ratio should be set so the average absolute segment orientation is 45°,
  which maximizes discriminability of rates of change. Extended by Heer & Agrawala (2006) to
  multi-scale banking. `WIDELY-ATTRIBUTED` with citation. **This is a computable optimum the canon
  doesn't know about, and dashero should implement it.**
- **Typography** is treated seriously only by Tufte (integrated labels, typographic resolution of
  sparklines) and only in passing. No systematic guidance in any of the nine.
- **Layout across multiple charts** — i.e., the actual dashboard problem — is addressed only obliquely,
  via micro/macro and small multiples. Nobody in these nine books designs a dashboard.

## Where does Axis A dominate Axis B, and vice versa?

The canon's answer is **asymmetric**, and the asymmetry is the useful part.

**Tufte states the arbitration rule explicitly, and it is his sixth and final principle:**
*"Analytical presentations ultimately stand or fall depending on the quality, relevance, and
integrity of their content."* `SOURCED`. Content adjudicates. And *"If the numbers are boring, then
you've got the wrong numbers"* `SOURCED` says the same thing negatively: **a WHAT problem cannot be
fixed by HOW.** No rendering rescues the wrong comparison.

**But the reverse is not symmetric.** The Challenger chapter is the demonstration: the engineers
*had* the right theory, *had* the data, and *"were thinking causally, but they were not displaying
causally"* `SOURCED`. Correct WHAT + failed HOW killed seven people. So HOW cannot rescue a wrong
WHAT, but HOW can absolutely destroy a right one.

**The operational consequence for dashero:**

| | Error in Axis A (wrong comparison) | Error in Axis B (wrong rendering) |
|---|---|---|
| **Visibility to user** | Silent. Looks fine. | Visible. Looks wrong. |
| **Recoverability** | Unrecoverable by any styling | Recoverable by restyling |
| **Who catches it** | Only someone who knows the domain | Anyone, immediately |
| **Right response** | **Gate it. Refuse to render. Ask.** | **Theme it. Ship a default, allow override.** |

This table is the single most important design decision in the product. **Axis A errors should block;
Axis B errors should be tunable.** A beautiful rendering of the wrong comparison is exactly the failure
the operator named, and the defence against it is not better rendering — it is a refusal to render
until the comparison is established.

**Where Axis B legitimately dominates:** at the moment of *first contact*. Rendgen is right that
nothing gets read if nothing invites reading, and dashero's growth loop is a shared link, where the
first two seconds are everything. The resolution is not a compromise on integrity; it is recognizing
that A and B answer to different constituencies — A answers to the person making a decision, B answers
to the person deciding whether to look. **Hold A absolutely; spend B generously.**

---

# PART 3 — The Commandments

Eighteen. Each is an imperative, tagged, traced, given a machine-executable rule, and paired with the
specific failure it prevents. These are written to become the design system and the chart-inference
engine's system prompt, so they are deliberately concrete about chart properties.

Throughout: `n` = number of rows/categories; `series` = number of encoded groups; `measure` = the
quantitative field; `dimension` = the categorical/temporal field.

---

### I. `[WHAT]` — Never render a number without its comparison.
**Source:** *Beautiful Evidence* principle 1 · *Envisioning Information* p. 67 · *Visual Explanations*
(*"Numbers become evidence by being in relation to"*).

**Rule.** Every chart spec must carry a non-null `comparison` field with a value from:
`{across_categories, over_time, vs_target, vs_prior_period, vs_group_baseline, part_to_whole,
across_two_measures}`. If the inference engine cannot populate it, do **not** render a chart —
emit a stat tile and queue a clarifying question in the conversation thread. A bare aggregate with
no second term is never a chart.

**Prevents.** The single-number chart, the "Total Revenue: $2.4M" bar with one bar, and the whole
class of charts that answer a question nobody asked because no question was ever formed.

---

### II. `[WHAT]` — Order categories by the measure, never by the label.
**Source:** *Visual Explanations* (Challenger table *"ordered by the possible cause, temperature,
from coolest to warmest"*) · Suda (*"With bar charts, order is not necessarily important… they can
be sorted alphabetically, by value or in some other order — as long as it best tells the story"*).

**Rule.** For a nominal `dimension` against a `measure`: default `sort = measure DESC`. Override only
when `dimension.type ∈ {ordinal, temporal}` or when the dimension matches a known-ordered lexicon
(day names, month names, size scales, quartiles, likert scales, funnel stages). Never inherit the
spreadsheet's row order and never sort alphabetically unless the user explicitly asks.

**Prevents.** Alphabetical bar charts — where the ranking, which is the actual finding, is scrambled
into noise by an accident of naming.

---

### III. `[WHAT]` — Keep the cases where nothing happened.
**Source:** *Visual Explanations* — the cholera-free workhouse and brewery (*"those essential
compared-with-what cases"*); the damage-free Challenger launches (*"The flights without damage
provide the statistical leverage necessary"*).

**Rule.** Never silently drop rows where `measure == 0` or `measure IS NULL`. Zeros render as
zero-length marks; nulls render as explicit gaps, never as zero and never as interpolated line
segments. If any filter reduces the row count, render `n excluded` in the chart footer with the
filter predicate.

**Prevents.** The survivorship-bias chart. This is the exact mechanism of the Challenger failure and
it is trivially easy for a query-generating machine to reproduce by writing `WHERE value > 0`.

---

### IV. `[WHAT]` — Do not let a date column end the analysis.
**Source:** *Visual Explanations* (*"the passage of time is a poor explanatory variable… descriptive
narration is not causal explanation"*).

**Rule.** If the table has a temporal column **and** ≥1 other dimension, the generated dashboard must
include at least one **non-temporal** cut (breakdown by category, or a two-measure scatter). Time
series may not exceed 60% of the charts on a generated dashboard.

**Prevents.** The all-line-charts dashboard: twelve views of "over time" that describe everything and
explain nothing. This is the default failure mode of every auto-charting tool on the market and the
easiest place to visibly beat them.

---

### V. `[WHAT]` — Classify the information's structure before choosing a chart.
**Source:** Meirelles (six structures: hierarchical / relational / temporal / spatial /
spatio-temporal / textual; the per-case *"DATA TYPE AND VISUAL ENCODING"* schema) · Rendgen
(Location / Time / Category / Hierarchy).

**Rule.** The inference pipeline's first stage emits a `structure` classification, not a chart type.
Detect: self-referencing parent/child columns → **hierarchical**; source/target pairs → **relational**;
date/datetime → **temporal**; lat-lon, country/region/postcode → **spatial**; free text → **textual**;
otherwise → **categorical-quantitative**. Chart-type selection is a *downstream* function of
`(structure, cardinality, measure_count)`. Persist the classification on the chart spec.

**Prevents.** Forcing a network, a tree, or a geography into a bar chart because bar charts are what
the library does well. Also prevents the reverse — a treemap for six flat categories.

---

### VI. `[WHAT]` — Refuse the chart when a number or a table is better.
**Source:** *Beautiful Evidence* (sparklines as datawords) · Suda (*"you have pretty much recreated
some tabular data with an ugly dot in the middle"*).

**Rule.**
- `n == 1` → stat tile, no chart.
- `n == 2` → stat tile with delta and direction.
- `n ≤ 4` **and** the user's question implies value lookup → sorted table with an inline bar column.
- Any time-series stat tile gets an embedded sparkline (no axes, no labels, endpoint dot).
- `n > 30` categories → do not render 30 bars; render top 10 + explicit `Other` aggregate, and say so.

**Prevents.** Chart-shaped tables. The three-bar bar chart that is slower to read than the three
numbers it contains.

---

### VII. `[WHAT]` — Declare the aggregation and respect the precision of the sample.
**Source:** *Beautiful Evidence* principle 5 (documentation) · Suda (*"An indication that the data is
not statistically sound is when it is almost too precise"*) · Rendgen (units and proportions
*"absolutely indispensable"*).

**Rule.** Axis titles and tile labels must name the aggregation and the unit —
`"Median order value (USD)"`, not `"Value"`. Round displayed aggregates to
`min(source_precision, 3 significant figures)`. If `n < 30` for any aggregated group, mark it
`small sample` on hover and exclude it from any automatic "highest/lowest" annotation.

**Prevents.** `$127.8642` as a group mean over four rows, presented with the same visual authority as
a mean over forty thousand.

---

### VIII. `[WHAT]` — Never mix relative and absolute, and never compare unadjusted money across years.
**Source:** VDQI graphical-integrity principles (deflated/standardized units for money) `WIDELY-ATTRIBUTED`
· Suda ch. 12, *Relative versus absolute*.

**Rule.** A single axis may not carry both a count and a percentage. If two measures with different
units share a chart, use a dual-axis **only** with both axes labelled with units and both series
directly labelled — otherwise facet. If a measure is detected as currency **and** the temporal span
exceeds 24 months, surface an inflation-adjustment toggle and annotate the axis `nominal` until it
is resolved.

**Prevents.** The growth chart that is really an inflation chart — the exact confusion Tufte calls out
in the diamond-price example (EI p. 34, *"a crucial confusion because the graph chronicles a time of
high inflation"*) `SOURCED`.

---

### IX. `[WHAT]` — Attach provenance to every chart, permanently.
**Source:** *Beautiful Evidence* principle 5 · Carter (Data: what was selected, what wasn't).

**Rule.** Every rendered chart carries an always-visible footer: source spreadsheet name + tab +
column names used + row count + last-sync timestamp + any filter or aggregation applied. On a shared
unlisted link this footer is **not** suppressible. Machine-generated charts get a visible
`auto-generated` marker until a human edits or confirms them.

**Prevents.** An unattributed, undated, unfiltered chart circulating in Slack as fact. Also directly
serves Carter's disclosure obligation: it is how the viewer learns which choices were defaults.

---

### X. `[HOW]` — Encode by perceptual accuracy, most important measure first.
**Source:** Meirelles (*"the visual encoding is unsuitable and could be misleading"*; via Bertin and
Ware) · Cleveland & McGill 1984 for the ordering (external to the nine, cited).

**Rule.** Assign channels in strict priority: **position on a common scale** → **length** →
**position on non-aligned scales** (i.e., faceting) → **angle** → **area** → **colour value/shading**
→ **hue**. The primary measure always takes position-on-common-scale. Area is permissible only for
part-of-whole and geographic marks. **Volume and any 3D depth channel are forbidden outright.**
A quantitative measure is never encoded in hue alone — always value/lightness, optionally plus hue.

**Prevents.** The bubble chart where the finding is buried in the least accurate available channel.

---

### XI. `[HOW]` — Enforce proportional ink; assert the lie factor.
**Source:** VDQI (*"The representation of numbers, as physically measured on the surface of the
graphic"* must be proportional; `Lie Factor = size of effect shown / size of effect in data`) ·
Suda (*"the scale must remain anchored and consistent"*; the 3D pie demonstration).

**Rule.** Bar, column, area and any filled mark: `yAxis.min = 0`, non-negotiable, not user-overridable.
Line and scatter may use a non-zero baseline but must render an explicit axis-break marker and must
never fill to the axis. No 3D, no perspective, no depth shadow on any mark. Compute
`lie_factor = (rendered_extent_ratio / data_value_ratio)` for the largest and smallest marks; assert
`0.95 ≤ lie_factor ≤ 1.05` in the render test suite and **fail the build**, not the request.

**Prevents.** The truncated-axis bar chart — the most common and most effective lie in business
reporting — and the 3D pie where equal wedges look unequal.

---

### XII. `[HOW]` — Spend contrast only where it buys a distinction.
**Source:** *Visual Explanations* ch. 4 (*"Make all visual distinctions as subtle as possible, but
still clear and effective"*) · Suda (*"When each piece of the chart is a different colour, then the
impact of any individual colour is lost"*).

**Rule.** Exactly **one** accent per chart. Default series colour is a neutral grey ramp; the accent
is applied to at most one series or one mark — the one named by the chart's `focus` field. If `focus`
is null, no accent is applied and the chart renders entirely in the neutral ramp. Axis lines, ticks
and gridlines derive from a single `--chart-structure` token, never from a series colour.

**Prevents.** The rainbow dashboard where seven fully saturated series compete and none wins — the
literal state Tufte describes as everything emphasized, therefore nothing emphasized.

---

### XIII. `[HOW]` — Never place two heavy elements adjacent. (The 1+1=3 rule.)
**Source:** *Envisioning Information* ch. 3 (Albers) — *"The noise of 1 + 1 = 3 is directly
proportional to the contrast in value (light/dark) between figure and ground."*

**Rule.** Maintain a strict three-tier weight hierarchy, expressed as theme tokens rather than fixed
values: **data marks** (highest contrast against background) > **reference lines / axis** (mid) >
**gridlines** (lowest). Constraints: gridline contrast must be strictly less than axis contrast, which
must be strictly less than data contrast. At most one stroke ≥ 2px per chart layer. Never render a
gridline and a data line at the same weight, and never place two ≥2px strokes within 4px of each
other. **Because this rule is defined by figure/ground *contrast*, it must invert correctly in dark
mode — see Part 5.**

**Prevents.** The vibrating chart: dense gridlines at data weight producing moiré and phantom bands,
which is precisely the "worst index ever designed" failure Tufte documents.

---

### XIV. `[HOW]` — Saturate small areas; mute large ones.
**Source:** *Envisioning Information* ch. 5, quoting Imhof's first and second rules — strong colours
*"have loud, unbearable effects when they stand unrelieved over large areas"* but achieve
*"extraordinary effects… used sparingly on or between dull background tones"*; and
*"color spots against a light gray or muted field highlight and italicize data."*

**Rule.** Map fill area to saturation ceiling. Marks covering `> 20%` of the plot area: max chroma
capped low (muted/desaturated). Marks covering `< 5%` (points, endpoint dots, annotation markers,
the single highlighted bar): full chroma permitted. Choropleth and treemap fills always take the
muted ramp. Never place two light-tint-plus-white fills adjacent over large areas (Imhof's second
rule). Categorical palettes cap at **7 hues**; beyond 7, group into `Other` or facet.

**Prevents.** The fully saturated choropleth and the seven-colour stacked area chart — both of which
read as loud and cheap, which is the opposite of the operator's stated goal.

---

### XV. `[HOW]` — Label directly; kill the legend.
**Source:** *Beautiful Evidence* principle 4 (*"Completely integrate words, numbers, images,
diagrams"*) · *Visual Explanations* (*"A letter-code accompanies the cross-hatching. Such codes can
hinder visual understanding"*).

**Rule.** If `series ≤ 5` and horizontal space allows, label each series at its rightmost point
(line/area) or inside/adjacent to its mark (bar), and **emit no legend**. If a legend is unavoidable,
order its entries to match the visual order of the series at the chart's right edge — never
alphabetically, never by insertion order. Bar charts with `n < 8`: drop the measure-axis gridlines
entirely and label each bar with its value directly.

**Prevents.** The legend round-trip — the eye leaving the data to decode a colour, returning, and
losing its place. Note this is also the operator's own example rule, and it is correct.

---

### XVI. `[HOW]` — Facet rather than overplot; hold the frame constant.
**Source:** *Envisioning Information* ch. 4 — *"Constancy of design puts the emphasis on changes in
data, not changes in data frames"*; panels *"positioned within the eyespan."*

**Rule.** If `series > 5` on a line chart, or `series > 3` on an area chart, convert to small
multiples. Across facets: **identical** x and y scales, identical axis ranges, identical colour
mapping, identical mark styling — only the data varies. Draw axis labels once on the outer edge, not
per panel. Sort facets by the measure (descending), never alphabetically. Grid layout: prefer 3–4
columns; each panel ≥ 120px wide or fall back to a ranked list.

**Prevents.** Spaghetti line charts. Also prevents the subtler and more damaging failure of facets
with independently scaled axes, where the visual comparison the layout invites is actively false.

---

### XVII. `[HOW]` — Set aspect ratio by computation, not by container.
**Source:** VDQI (*"Graphics should tend toward the horizontal, greater in length than height"*) ·
Cleveland's banking-to-45° (external to the nine, cited) · Suda's aspect-ratio chapter, which
concedes *"There is no correct answer."*

**Rule.** Default `width:height = 1.6:1`, always wider than tall. For line charts specifically,
compute the banking-to-45° optimum — the ratio at which the median absolute segment orientation is
45° — and clamp to `[1.2, 3.0]`. Never let a responsive grid cell produce a chart taller than it is
wide; below the breakpoint where that would happen, switch the chart to a horizontal-bar or ranked-list
form instead of squeezing it.

**Prevents.** The tall-narrow line chart that exaggerates every wiggle into a crisis, and the
short-wide one that flattens a real trend into nothing. Both are lie-factor violations produced
purely by layout.

---

### XVIII. `[HOW]` — Make the dashboard readable at two distances.
**Source:** *Envisioning Information* ch. 2, micro/macro (*"the same ink serves more than one
informational purpose; graphical elements are multifunctioning"*) · *Beautiful Evidence* (sparklines
as inline datawords).

**Rule.** Fixed dashboard grammar. **Macro row:** stat tiles, each carrying value + delta vs. the
declared comparison + an inline sparkline (word-height, no axes, endpoint dot). **Micro region:**
the charts, ordered so that each one decomposes a tile above it, with an explicit visual link between
tile and chart. Every dashboard must survive a squint test — at 25% zoom the macro row must still
communicate direction and magnitude. Assert this in CI by rendering at reduced scale and checking
that tile text remains above minimum legible size.

**Prevents.** The dashboard as an undifferentiated wall of twelve equal-weight charts with no reading
order — which is Tufte's PowerPoint critique reproduced in a browser.

---

## Non-negotiable vs. tunable

Per the Part 2 asymmetry, these commandments do **not** all have the same status.

- **Gate (block the render, never override):** I, III, XI. These are integrity invariants. A violation
  is a lie, not a preference.
- **Strong default (override requires an explicit user action that is recorded):** II, IV, V, VI, VII,
  VIII, IX, X, XV, XVI, XVII.
- **Theme-level (a style the product may ship several of):** XII, XIII, XIV, XVIII. These encode
  Tufte's *austerity*, which is a taste, not a truth. See Part 5.

---

# PART 4 — "Tell a story": the honest boundary

The operator asked for the honest read rather than encouragement. Here it is.

## What the canon actually says makes a graphic narrative rather than merely accurate

Stripping the mysticism out, the canon identifies five concrete mechanisms:

1. **A stated comparison.** Not an implied one. Tufte's *"Compared with what?"* is a question the
   graphic must visibly answer, which means the baseline must be *drawn*, not assumed.
2. **Ordering that constitutes a claim.** Sorting by magnitude asserts a ranking. Ordering by the
   suspected cause — Tufte's Challenger fix — asserts a hypothesis. Ordering is the cheapest
   argumentative act available and the canon uses it constantly.
3. **Contrast that names a protagonist.** Suda states this in exactly those terms: *"Sometimes you
   need some characters to stand out and others to play a supporting role, but both are important in
   advancing the plot."* `SOURCED`. One accent against a muted field — Imhof's rule reused as a
   narrative device.
4. **Integrated words.** BE principle 4. A graphic with a sentence in it makes a claim; a graphic with
   only labels reports a state. This is the difference between a chart and an argument, and it is
   almost entirely a *text* problem rather than a graphics problem.
5. **Sequence.** Small multiples ordered by a variable; micro/macro so the eye has a path; the
   dashboard reading top-to-bottom overview-then-detail. Narrative requires an order of encounter.

Note what is *not* on this list: illustration, iconography, animation, or novel chart forms. The
canon's account of narrative is almost entirely about **selection, ordering, contrast and words**.
That is good news, because four of those five are cheap in software.

## What a program can do automatically — and it is more than the operator may expect

These are all mechanizable today, with no domain knowledge:

- **Rank and sort by magnitude.** Pure computation. Produces a ranking claim.
- **Detect and mark the outlier.** IQR or z-score on the residuals. Produces "X is unlike the others."
- **Detect the change point.** Standard changepoint detection on a series. Produces "something
  happened in March."
- **Compute the delta against a chosen baseline.** Trivial once the baseline exists.
- **Apply the single accent to the detected focal mark.** Commandment XII, driven by the above.
- **Position the annotation without collision.** Solved layout problem.
- **Hold frames constant across facets.** Commandment XVI.
- **Impose a reading order on the dashboard.** Commandment XVIII.
- **Write a declarative title from the data.** *"Revenue fell 12% in March, the largest single-month
  drop in two years"* is fully derivable from the table. **This is the highest-leverage automatable
  storytelling move that exists**, because it converts a chart from a lookup surface into a claim,
  and it costs one template and one statistic.

If dashero does only these eight things well, its charts will read as far more argued than anything
Sheets or Excel produces. That is a real and achievable differentiator, and none of it requires
understanding the business.

## What fundamentally requires knowing what the point is

And here is the part that does not yield, listed in descending order of how much damage it does:

1. **Polarity — is up good?** Revenue up is good; churn up is bad; latency up is bad; headcount up
   is ambiguous and depends entirely on the company's situation. A machine cannot reliably infer this
   from a column name. `churn_rate`, `cancellations`, `p99_ms`, `days_to_close`, `cost_per_acquisition`
   — a lexicon catches maybe 60% of real-world column names and fails silently on the rest, and it
   fails hardest on the custom names real spreadsheets actually contain. **Getting polarity wrong
   inverts the story.** A green up-arrow on a churn spike is not a small error; it is the product
   confidently telling the user the opposite of the truth, and it destroys trust permanently on first
   occurrence.
2. **Which comparison is the decision-relevant one.** Any table of moderate width supports dozens of
   defensible comparisons. Only the domain says which one bears on a decision. This is *exactly* the
   Challenger failure — the engineers had the data and the correct theory and still displayed the
   wrong comparison. If trained rocket engineers with their colleagues' lives at stake picked the
   wrong cut, a language model reading column headers will too.
3. **Whether a difference is material.** Statistical significance is computable; business
   significance is not. A 3% movement may be noise or may be the whole quarter. Annotating the
   statistically notable point is easy and frequently annotates the wrong thing.
4. **Causality.** Beautiful Evidence principle 2 asks for *"causality, mechanism, explanation,
   systematic structure."* A program can show correlation and can order by a suspected cause **if
   told which variable is suspected.** It cannot identify the cause, and it must never phrase a
   correlation as one. **The canon's second principle is the one automation cannot satisfy, and
   pretending otherwise is the most dangerous thing this product could do.**
5. **What the audience already knows.** Narrative is departure from expectation. The machine has no
   model of the viewer's prior, so it cannot know which of twenty true statements is *news*.

## The honest boundary, stated plainly

**A program can reliably make a chart *emphatic*. Only knowledge of the purpose can make it
*right-to-emphasize*.** Every automatic storytelling technique — the accent colour, the annotation,
the declarative title, the sort order — is an amplifier. Applied to the correct finding it is the
product's entire value. Applied to an arbitrary finding it manufactures false confidence, and it does
so *invisibly*, because the output looks exactly as polished either way.

Carter names the mechanism precisely: **"viewers don't know the difference between intention and
default."** `SOURCED`. Every default dashero ships is read as an authored claim. An auto-generated
dashboard shared by unlisted link is a document that *looks* like somebody meant it. That is the
product's core promise and its core liability, and they are the same property.

My estimate — `UNVERIFIED`, offered as a working assumption rather than a measurement — is that
naive automatic emphasis on real-world spreadsheets will pick a defensible focal point most of the
time and a misleading one often enough to matter, with polarity errors being the largest single
contributor. The distribution is what matters, not the mean: the failures are not evenly boring,
they are concentrated in exactly the high-stakes metrics people actually share.

## The design consequence — and it is good news

**Do not try to infer the point. Elicit it, cheaply, and then apply the full storytelling machinery
safely.** The conversational layer is not a polish feature bolted onto the charts; it is the
mechanism that supplies the one variable the canon assumes and the machine lacks. Reframed that way,
the conversation *is* the product and the charts are its output.

Concretely, and in priority order:

1. **Ask for polarity per metric, once, at connect time.** One pass over the detected measures:
   "for each of these, is higher better, worse, or neither?" Thirty seconds of user time. It unlocks
   colour semantics, delta arrows, declarative titles, and the "worst performer" annotation — the
   majority of the storytelling machinery — and it eliminates the highest-damage failure mode
   outright. **This is the highest return-on-effort decision in the entire product.**
2. **Ask what decision the dashboard supports.** One sentence. It supplies the focus and the
   comparison for every chart downstream.
3. **Gate declarative titles behind known polarity.** Until polarity is known, titles are neutral and
   descriptive (`"Revenue by month"`). Once known, titles become claims
   (`"Revenue fell 12% in March"`). Never guess in between — a neutral title is honest, a wrong
   claim is not.
4. **Let the user pin the comparison,** and treat a pinned comparison as sticky across regeneration.
5. **Show the machine's reasoning as editable state.** Surface `focus`, `comparison`, `sort` and
   `polarity` as visible, changeable chips on each chart rather than hidden inference. This is
   Carter's disclosure obligation implemented as UI, and it converts an invisible A-axis error into
   a visible, one-click-fixable one — which, per the Part 2 table, is the whole game.

**The strongest argument against my own read here:** it is possible that in practice most business
spreadsheets are narrow, conventionally named, and dominated by a handful of metric archetypes
(revenue, count, rate, duration), such that a good lexicon plus an LLM's world knowledge gets
polarity right ~95% of the time and the elicitation step is friction users resent. If that's true,
my recommendation over-indexes on a rare failure. **This is cheap to test before building anything:
take 30 real spreadsheets, have the model guess polarity for every measure column, and check by hand.**
That single experiment resolves the largest open design question in the product, and it should be run
in Wave 0.

---

# PART 5 — The critique

Adversarial, per Clause #11.

## 5.1 Which commandments cannot be automated without domain meaning — and what happens anyway

| Commandment | Why it needs domain meaning | Failure when the machine proceeds regardless |
|---|---|---|
| **I** (comparison) | Data supports many comparisons; only purpose selects one | Picks the widest-coverage comparison, which is usually the least interesting. Charts are technically valid and practically inert. |
| **II** (ordering) | Semantic order often isn't in the data — `Qualified / Negotiation / Closed Won` alphabetizes wrong | Funnel stages scrambled; a process chart reads as a ranking. Confidently wrong, visually clean. |
| **IV** (causal cut) | Cannot distinguish confounder from cause | Offers a spurious breakdown with equal prominence to a real one. Correlation laundered into apparent explanation. |
| **VIII** (deflation) | Requires knowing the measure is nominal money | Either never offers adjustment (understates), or offers it for non-monetary counts (nonsense). |
| **XII** (single accent) | The accent *is* the editorial claim | Highlights the statistical outlier, which is often a data-entry error or a tiny-denominator artifact. The product's most confident visual statement lands on garbage. |
| **XIV** (diverging palettes) | Requires knowing the neutral midpoint | Centres a red/green ramp on the arithmetic mean, so half of a healthy distribution renders as "bad." |
| **XVIII** (tile deltas) | Requires polarity | Green arrow on rising churn. Single most trust-destroying possible output. |

**The pattern is the important part.** These do not fail loudly. They fail into **plausible,
well-rendered, confidently-emphasized wrongness.** An ugly chart gets fixed; a beautiful wrong one
gets forwarded. Because dashero's distribution mechanism is a shared link, its errors propagate
faster than its corrections — the artifact travels without the creator attached to explain it.
**Polish raises the cost of being wrong.** That is not a reason to avoid polish; it is a reason to
gate the A-axis (Commandments I, III, XI as hard blocks) rather than the B-axis.

## 5.2 Where slavishly following Tufte produces charts users actively dislike

This tension is real, commercially significant, and under-acknowledged by people who quote Tufte.

- **Tufte optimizes for reasoning; dashboards are largely used for monitoring and reporting.** The
  data-ink loop assumes an analyst extracting insight. A weekly-metrics viewer wants to look up a
  number and leave. Stripping gridlines (Commandment XV) genuinely makes lookup harder. Tufte's
  answer would be that lookup is a table's job — correct, and irrelevant to what buyers want.
- **The empirical evidence contradicts a strong data-ink position on memorability.** Bateman et al.
  (CHI 2010): embellished charts showed **no loss in comprehension accuracy** and **significantly
  better recall at two-to-three weeks.** `SOURCED`. Memorability is *precisely* the dimension a
  share-by-link product depends on. The authors decline to generalize it, and their caution is
  well-taken — imagery can bias interpretation — but the result stands and it cuts against austerity.
- **Density vs. scannability.** Tufte wants maximum data density. SaaS users, on laptops, scrolling,
  want whitespace, big numbers and cards. Maximum density on a dashboard reads as "overwhelming,"
  and users bounce.
- **Sparklines are lovely and nearly unusable on a phone.** Word-height graphics assume print
  resolution and a stationary reader.
- **The pie chart fight is not worth having.** Tufte and Suda both despise them. But for
  part-to-whole with ≤4 slices, pies are *fine*, users request them by name, and refusing to render
  one reads as the product being opinionated at the customer's expense. Suda's own position actually
  concedes the two-item case is effective. Ship pies, cap them at 5 slices, sort by magnitude, direct-label,
  and stop fighting.
- **"Beautiful" to this operator's customer probably means closer to *Information is Beautiful* or
  Rendgen's corpus than to Tufte.** A Tufte-pure product risks shipping charts that are *correct and
  boring* — and losing to a competitor whose charts have gradients. The operator explicitly said bars
  and scatter plots "just won't do." **Tufte's answer to that request is essentially "yes they will,
  if the numbers are interesting." That is intellectually defensible and commercially a losing
  answer.**

**Resolution I'd propose:** split the doctrine, which is what the Commandments' status table already
does. **Integrity rules (I, III, XI) are absolute and shipped as gates.** **Austerity rules
(XII, XIII, XIV, XVIII) are a *theme* — "Editorial" — and dashero should ship two or three themes,
one of which is meaningfully more expressive.** Tufte's rules are excellent constraints and a poor
brand. Treating data-ink as a tunable rather than a commandment is a defensible reading of Tufte's
own repeated *"within reason"* qualifier, which is in the original text and which almost everyone
citing him drops.

## 5.3 Where the canon is silent or actively wrong for a web product in 2026

The nine books are print artifacts. Eight of nine predate responsive design; the newest substantive
guidance on screens is Suda (2010). Specific gaps:

- **Interactivity — silent, and it changes the arithmetic.** Tooltips dissolve the central tension
  Tufte spends chapters resolving: you no longer must choose between density and precise value
  lookup, because hover supplies precision on demand. *Envisioning Information* mentions computer
  screens only pejoratively — windows *"surrounded by a frame of system commands and other computer
  administrative debris"* `SOURCED` — and offers no positive theory. **Several data-ink prescriptions
  are simply less binding when hover exists**, and dashero should exploit that rather than obey rules
  written for paper.
- **Responsive layout — silent.** No aspect-ratio rule in the canon survives a 375px viewport. Small
  multiples at phone width are unreadable; sparklines vanish; direct labels collide. The canon offers
  no degradation order, so dashero must invent one. Proposed, and this is my synthesis rather than
  anything from the books: **drop gridlines → drop minor tick labels → drop direct labels for a
  legend → reduce facet count → switch chart form entirely** (line → sparkline + delta; grouped bar →
  ranked list).
- **Dark mode — silent, and the canon is *actively wrong* here in one specific, checkable place.**
  Tufte's rule is *"The noise of 1 + 1 = 3 is directly proportional to the contrast in value
  (light/dark) between figure and ground. **On white backgrounds, therefore, a varying range of
  lighter colors will minimize incidental clutter.**"* `SOURCED`. **The conditional is explicit in
  the text and the conclusion inverts on a dark ground** — on dark backgrounds, lighter greys are
  *higher* contrast against the ground and produce *more* 1+1=3 noise, not less. The correct
  generalization is the first sentence (minimize figure-ground *value contrast* for non-data
  elements), not the second. Imhof's rules have the same problem: they are stated for ink on paper.
  **Implementation consequence:** Commandment XIII must be expressed as *contrast ratios against the
  current background token*, never as fixed grey hex values. A dashero theme that hard-codes
  `#e0e0e0` gridlines will be correct in light mode and broken in dark. This is a concrete,
  falsifiable bug that a naive Tufte reading produces.
- **Real-time / changing data — silent.** No book here considers a chart whose underlying data
  changes while someone watches. Unaddressed: axis-range stability across refreshes (a rescaling axis
  makes every value appear to move), how to indicate staleness, what "last updated" obligations exist.
  For a Google-Sheets-backed product where the sheet changes under the link, this is a first-order
  concern the canon cannot help with. **Proposed rule, mine not the canon's: axis ranges are sticky
  within a session and only rescale on an explicit threshold breach, with the rescale announced.**
- **Accessibility — near-total silence, and one direct conflict.** Suda is the honourable exception
  (colour-vision-deficiency chapter, redundant encoding, ~8% of males). The other eight are silent.
  Colour-universal palettes like Okabe-Ito postdate every book here except Carter and Suda.
  **The direct conflict:** WCAG 2.2 SC 1.4.11 requires **3:1 contrast** for graphical objects
  essential to understanding, including *"lines in line graphs and slices in pie charts."* `SOURCED`.
  Tufte's smallest-effective-difference says make distinctions *as subtle as possible*, and his
  gridline advice is to let structure whisper. **These genuinely conflict, and "follow Tufte" produces
  WCAG failures.** The resolution is implementable and worth stating precisely: **meaning-bearing
  elements** (series lines, marks, reference lines, category fills) must meet 3:1 against adjacent
  colours, no exceptions; **non-meaning-bearing decoration** (gridlines, which are navigational rather
  than informational) may go below, because the standard scopes the requirement to objects *required
  to understand the content*. So: Tufte governs gridlines, WCAG governs data. That is a clean split
  and it should be encoded in the theme tokens directly.
  Also entirely absent from the canon: screen readers. No book here imagines a non-visual consumer.
  Every chart needs a generated table fallback and a text summary — and note that **the same
  declarative-title machinery from Part 4 generates the alt text for free.** This is an area where
  the canon's silence is an opportunity rather than a constraint: essentially no competitor in this
  category does it well.

## 5.4 Is "beautiful charts" a defensible differentiator? — the skeptical case, argued properly

**The skeptical case, which I think is largely correct:**

1. **Visual style is the single most copyable thing in software.** Chart aesthetics are a stylesheet
   and a palette. A competitor who sees dashero's output can approximate it in a sprint. There is no
   accumulating advantage in a colour ramp.
2. **The floor has risen and "not ugly" is now table stakes.** Vega-Lite, Observable Plot, ECharts and
   Recharts all produce respectable output by default. The gap between "default charting library" and
   "considered design" is much narrower in 2026 than it was when the operator formed the intuition
   that Excel charts are ugly. **The comparison class is not Excel 2010; it is every well-funded
   analytics startup shipping today.**
3. **Aesthetics invite competition on a dimension where a funded competitor with a real designer
   wins.** The operator is solo and has no designer. Choosing "most beautiful" as the axis of
   competition means choosing to compete where he is structurally weakest. That is backwards.
4. **Beauty is a acquisition mechanism, not a retention mechanism.** People do not renew a
   subscription because the gradients are nice. They renew because the thing is connected to their
   data and correct and they'd have to redo work to leave.
5. **The genuinely hard, genuinely defensible problems in this product are unglamorous:** inference
   quality on messy real-world sheets (merged cells, header rows, mixed types, multiple tables per
   tab); Sheets auth and schema-drift resilience; whether the conversational repair loop actually
   converges instead of frustrating; and the share-loop mechanics. **None of those is "beautiful
   charts," and all of them are harder to copy.**

**The steelman, which is not nothing:**

1. **The growth loop is a shared link, and memorability is measured to improve with visual
   distinctiveness** (Bateman et al.). A chart screenshotted into Slack *is* the acquisition channel.
   Aesthetics → shares → growth is a real mechanism, not vanity.
2. **The defensible version of "beautiful" is not taste — it is *reliability of default quality at
   scale*.** "80% of auto-generated dashboards are presentable with zero edits" is an inference-quality
   claim wearing an aesthetics costume, and inference quality *does* compound with usage data.
   That is a moat. "Our blue is nicer" is not.
3. Rendgen's point stands: *"It is the design that makes us want to look at the data."* Engagement is
   a precondition for delivering any value at all.

**Verdict.** **Beauty is a wedge, not a moat.** It earns the first look and the first share; it does
not survive a competitor's sprint and it does not drive renewal. **The commandments above are worth
implementing not because they make charts pretty, but because they are the mechanism by which the
*default* output is good without a human in the loop — and zero-effort-presentable is an operational
property that compounds, where taste does not.** I would reposition the product's internal thesis
from *"the most beautiful charts"* to *"the dashboard you don't have to fix,"* keep every one of the
eighteen commandments, and spend the saved ambition on inference quality and the polarity-elicitation
step from Part 4.

**Strongest argument against my own verdict:** in a crowded, undifferentiated category where every
competitor's *functional* claims sound identical, aesthetics may be the only signal a buyer can
actually evaluate in the ten seconds they give a landing page. If so, beauty is not a moat but it may
be the only viable *go-to-market*, and dismissing it as a wedge under-rates that wedges are how solo
founders get in at all. I hold my verdict, but not strongly, and it is testable: **ship two landing
pages with identical copy and materially different chart aesthetics, and measure signup.**

---

# Appendix — What I could not verify

Stated plainly, per Clause #11 Rule 3, because "no public data found" is a finding.

1. **Bruce Robertson, *How to Draw Charts & Diagrams* — essentially unresearched.** I established
   only catalogue metadata and one line of publisher copy. No table of contents, no chapter list, no
   review, no excerpt, no verified quotation, no specific design principle. The book is not in the
   Internet Archive or Open Library full-text corpus; the only academic hits were bare bibliographic
   citations *to* it. Queries run are listed in Part 1 §7. **No commandment is traced to Robertson,
   and my characterization of it as a pre-desktop-publishing studio production manual is inference
   from metadata, explicitly `UNVERIFIED`.** If the operator owns a copy, reading it is the highest-value
   research action remaining.
2. **Meirelles' specific encoding recommendations.** I verified her taxonomy, her per-case
   *"DATA TYPE AND VISUAL ENCODING"* schema, her Gestalt grounding, and the phrase *"the visual
   encoding is unsuitable and could be misleading"* — but only at phrase level via full-text search.
   I could not retrieve her encoding tables in full and **do not know which encodings she recommends
   for which data type.** The perceptual ordering in Commandment X is Cleveland & McGill's, not hers.
3. **Beautiful Evidence principle 5's exact imperative wording.** I verified principles 1, 2, 3, 4
   and 6 verbatim against a scan. Principle 5 I confirmed by position and topic (documentation of
   evidence) but not by exact phrasing.
4. **The lie factor's 0.95–1.05 acceptable band.** I verified the formula and Tufte's "equal to one"
   framing in the primary text. The specific tolerance band appears only in secondary sources and is
   `WIDELY-ATTRIBUTED`, not `SOURCED`. Commandment XI's use of it is a reasonable engineering choice,
   not a quotation.
5. **Sparkline dimensions.** The "14–20 pixels tall" figure circulating online appears only in
   derived material, some of it plausibly AI-generated. Not verified against *Beautiful Evidence*.
   Treated as `UNVERIFIED` and not used in any commandment.
6. **Rendgen's and her co-authors' introductory essays.** I read the publisher's structure, verified
   the introduction's opening line from a scan, and drew her views from two interviews. I did **not**
   read the essays by Ciuccarelli, Wurman or Rogers and make no claim about their arguments.
7. **Carter's book beyond the Data/Bias/Craft framework.** Sourced from one published excerpt and one
   long interview. I did not access the full text, and I know nothing specific about the embedded
   mystery-story device beyond that it exists.
8. **VDQI's six graphical-integrity principles as a numbered list.** I verified principle 1 and the
   "show data variation, not design variation" principle verbatim in a scan. The other four I have
   from corroborating secondary sources only.
9. **My estimate of automatic-emphasis error rates in Part 4** is a working assumption, explicitly
   labelled `UNVERIFIED`, with a proposed experiment attached. It is not a measurement and should not
   be cited as one.

**A closing caution on this document's own status.** Everything above is a reading of nine books by
someone who read two of them in full, one substantially, and six through keyhole searches and
interviews. The commandments are my synthesis, not the canon's own words — the canon nowhere states
an if/then rule about gridline counts. Where I have converted a principle into a threshold, the
threshold is an engineering judgment that the source does not license. Those numbers should be
treated as defaults to be tuned against real output, not as findings.
