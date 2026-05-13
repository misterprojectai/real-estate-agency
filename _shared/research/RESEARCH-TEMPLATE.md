# Research Brief — Schema Template

**Location:** `_shared/research/RESEARCH-[address-slug]-[YYYYMMDD].md`
**Created by:** 02_property_research
**Read by:** 03_client_communication (when communication follows a showing)

---

```
research_id:       RESEARCH-[address-slug]-[YYYYMMDD]
property_address:
linked_lead_id:    [LEAD-YYYYMMDD-XXX] | unlinked
requested_by:      [agent name]
date:              [YYYY-MM-DD]
status:            draft | final

## Price analysis
list_price:
suggested_range:   [low] – [high]
confidence:        high | medium | low
confidence_basis:  [e.g. "3 comps within 90 days, same street, similar sqft"]

## Comparable sales  [3–5 entries]
| Address | Beds/Baths | SqFt | Sale price | Days on market | Sale date |
|---------|------------|------|------------|----------------|-----------|
|         |            |      |            |                |           |
|         |            |      |            |                |           |
|         |            |      |            |                |           |

## Neighborhood profile
walkability:
schools:           [names and ratings]
commute_notes:
character:         [2–3 sentences describing the lived experience]

## Red flags
[bulleted list, or "None identified"]

## Talking points  [for agent's client conversation — lead with these]
-
-
-

## Recommended questions to ask client
-
-
-
```

---

## Scoping notes

When `linked_lead_id` is populated, the analysis is scoped to that client's:
- Budget range (`budget_min` / `budget_max`)
- Must-haves
- Dealbreakers
- Target neighborhoods

Red flags and talking points are evaluated against these constraints — not generically.

When `linked_lead_id` is `unlinked`, note at the top of the document:
*"General-market brief — not client-scoped. Link to a Lead Card for scoped analysis."*

## [ask] field protocol

If `must_haves` or `dealbreakers` are marked `[ask]` in the linked Lead Card:
- Produce brief scoped to budget range only
- Note at top: *"Client must-haves and dealbreakers not yet captured — scoping is budget-range only. Recommend completing these fields before using this brief in a client conversation."*
- Do not ask the agent for must-haves/dealbreakers — that is 01_lead_qualifier's scope
