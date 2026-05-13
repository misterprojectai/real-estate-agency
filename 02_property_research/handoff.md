# 02 Property Research — Handoff Contract

---

## What I receive

From the orchestrator context package:
- Property address, neighborhood, or market segment for analysis
- lead_id if research is client-specific (optional — unlinked briefs are valid)
- assigned_agent name

---

## What I read

### Lead Card at lead_id (when provided) — five fields only

- `budget_min`
- `budget_max`
- `must_haves`
- `dealbreakers`
- `target_neighborhoods`

These five fields scope the analysis. I load only these — not the full Lead Card.
Comps, red flags, and talking points are evaluated against these constraints.

### `_config/team-standards.md` — quality floor section

Frames how findings are presented: options and implications for the client,
not a list of problems to overcome.

---

## What I produce

A Research Brief written to:
`_shared/research/RESEARCH-[address-slug]-[YYYYMMDD].md`

Contents:
- Price analysis with confidence basis
- 3–5 comparable sales
- Neighborhood profile (walkability, schools, commute, character)
- Red flags evaluated against client constraints
- Talking points for agent's client conversation
- Recommended questions to ask client

Upon completion, if lead_id was provided, I append one line to the Lead Card Activity Log:
`[YYYY-MM-DD] — Research brief created: RESEARCH-[slug]-[YYYYMMDD].md`

This forward reference allows downstream specialists to locate the correct brief
without searching _shared/research/. This is an append operation — no other field
or prior entry is altered.

---

## Trigger

Agent requests analysis on a specific property, neighborhood, or market segment.

---

## Incomplete protocol

### No address or area provided

Ask before proceeding. Cannot produce a brief without a subject.

### No lead_id provided

Produce unlinked general-market brief. Note at top of document:
*"This brief is unlinked — analysis reflects the property and market, not a specific
client's constraints. Recommend completing intake and requesting a client-scoped
brief before a showing."*
Do not ask — unlinked briefs are valid outputs.

### lead_id provided but Lead Card not found

Surface the issue and present two explicit options:
"No Lead Card found at lead_id: [value]. Please either (1) verify the ID — it may
contain a typo — or (2) confirm you want a general-market brief with no client scoping."
Wait for the agent's decision. Do not default to an unlinked brief without confirmation.
The agent provided a lead_id intending client-scoped analysis.

### must_haves or dealbreakers marked [ask] in Lead Card

Produce brief scoped to budget range only.
Note at top of document:
*"Client must-haves and dealbreakers not yet captured — scoping is budget-range only.
Recommend completing these fields in the Lead Card before using this brief in a
client conversation."*
Do NOT ask the agent to provide must-haves or dealbreakers here.
That is 01_lead_qualifier's scope. Maintain one-way dependencies.

### budget range is [ask] in Lead Card

Ask for the budget range before proceeding.
Price analysis scoped to budget range is not possible without it.
This is a harder dependency than must_haves or dealbreakers — those allow a
reduced-scope brief. Budget cannot be reduced further.
