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

Upon completion, if lead_id was provided, I add one line to the Lead Card Activity Log:
`[YYYY-MM-DD] — Research brief created: RESEARCH-[slug]-[YYYYMMDD].md`

This forward reference allows downstream specialists to locate the correct brief
without searching _shared/research/.

---

## Trigger

Agent requests analysis on a specific property, neighborhood, or market segment.

---

## Incomplete protocol

### No lead_id provided

Produce unlinked general-market brief. Note at top of document:
*"General-market brief — not client-scoped. Link to a Lead Card for scoped analysis."*
Do not ask — unlinked briefs are valid outputs.

### No address or area provided

Ask before proceeding. Cannot produce a brief without a subject.

### must_haves or dealbreakers marked [ask] in Lead Card

Produce brief scoped to budget range only.
Note at top of document:
*"Client must-haves and dealbreakers not yet captured — scoping is budget-range only.
Recommend completing these fields in the Lead Card before using this brief in a
client conversation."*

Do NOT ask the agent to provide must-haves or dealbreakers here.
That is 01_lead_qualifier's scope. Maintain one-way dependencies.
