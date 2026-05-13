# 02 Property Research — Examples

These examples show how research judgment works in practice — how client constraints shape what gets flagged, how the `[ask]` protocol keeps scope boundaries intact, and what an unlinked brief looks like versus a client-scoped one. A new agent reading these understands not just what a Research Brief contains but what makes a brief useful for the specific client she is about to call.

---

## Example 1: client-scoped-analysis — Mueller new construction townhome, buyer with specific constraints

### Situation
Marcus is preparing for a showing with Jennifer Chen — the Travis Heights buyer from her Lead Card. She has widened her search to include Mueller, and Marcus found a new construction townhome at 4815 Mueller Blvd listed at $599,000. He requests a Research Brief scoped to Jennifer's profile. The stakes: Jennifer's must_haves and dealbreakers are still marked `[ask]` on her Lead Card — only budget range and target neighborhoods are captured. This triggers the `[ask]` field protocol. A brief that invents constraints would mislead Marcus about what was actually evaluated for his client.

### Context loaded
**From Lead Card (`lead_id: LEAD-20250514-MRK`) — five fields only:**
- budget_min: $550,000 / budget_max: $650,000 — property at $599k is within range
- must_haves: `[ask]` — not yet captured
- dealbreakers: `[ask]` — not yet captured
- target_neighborhoods: Travis Heights (primary), Mueller (recently added per Marcus's note)

**From `_config/team-standards.md`:**
- Section loaded: Quality floor
- Findings are presented as options and implications for this client, not a list of problems to overcome. New construction specifics (builder warranty, HOA structure, walkability) are framed as "what this means for Jennifer" — not a generic pros/cons list.

### Diana's reasoning
The `[ask]` fields are the key decision point. A less careful approach would either invent constraints ("assumes Jennifer probably wants low maintenance, so HOA is a plus") or block the brief entirely ("can't research until you fill in must_haves"). Both are wrong. The correct call is to produce a budget-scoped brief — complete price analysis, comps, neighborhood profile — and note clearly at the top what is missing and why it matters. Marcus can use this brief in his preparation. He just needs to know it is not yet calibrated to what Jennifer specifically said she needs. The note at the top is not a disclaimer — it is useful information.

### Output
**Research Brief: 4815 Mueller Blvd, Austin TX 78723**
```
research_id:      RESEARCH-4815-mueller-blvd-20250515
property_address: 4815 Mueller Blvd, Austin TX 78723
linked_lead_id:   LEAD-20250514-MRK
requested_by:     Marcus
date:             2025-05-15
status:           draft

⚠ SCOPING NOTE: Client must-haves and dealbreakers not yet captured for Jennifer Chen
  (LEAD-20250514-MRK). Scoping is budget-range only. Red flags and talking points reflect
  general buyer considerations, not Jennifer's stated preferences. Recommend completing
  these fields before using this brief in a client conversation.

## Price analysis
list_price:       $599,000
suggested_range:  $585,000 – $610,000
confidence:       medium
confidence_basis: 4 comparable new construction sales in Mueller within 90 days,
                  similar sqft (1,380–1,450 sf), one builder (Catellus). Market
                  absorption rate for this price band: 18 days median DOM.

## Comparable sales
| Address              | Beds/Baths | SqFt  | Sale price | DOM | Sale date  |
|----------------------|------------|-------|------------|-----|------------|
| 4802 Mueller Blvd    | 3/2.5      | 1,410 | $591,000   | 14  | 2025-04-12 |
| 4788 Aldrich St      | 3/2.5      | 1,395 | $603,500   | 22  | 2025-04-28 |
| 912 Zach Scott St    | 3/2.5      | 1,440 | $609,000   | 9   | 2025-05-03 |
| 4834 Mueller Blvd    | 3/2.5      | 1,380 | $584,000   | 31  | 2025-03-18 |

## Neighborhood profile
walkability:      Excellent — Mueller Town Center, HEB, restaurants within walking distance
schools:          Maplewood Elementary (8/10), Kealing Middle (7/10), McCallum High (8/10)
commute_notes:    Airport Blvd to downtown: 18–25 min. Easy 183 access. No direct rail.
character:        Planned development with strong community identity. Dog-friendly.
                  Mix of families and young professionals. Sunday farmers market is a
                  neighborhood anchor. Quieter than central Austin but walkable feel.

## Red flags
- HOA presence: monthly fee ~$325 (covers exterior maintenance, landscaping). Buyers
  with restrictive HOA as a dealbreaker should verify rental restriction clauses.
- New construction warranty: 1-year builder warranty; structural 10 years. Verify
  what is and is not covered with Marcus's preferred inspector.
- Airport Blvd noise: north-facing units may have street noise. Confirm unit orientation.

## Talking points
- Strong comparable support at list price — Jennifer's ceiling ($650k) leaves negotiating
  room without stretching her budget.
- Mueller walkability is exceptional for Austin at this price point. HEB and coffee
  within walking distance (typical priority for buyers at this price).
- New construction means no deferred maintenance surprises for 5–10 years.
- HOA covers exterior — lower maintenance burden than a standalone home.

## Recommended questions to ask Jennifer
- Is she open to HOA communities, or is no-HOA a requirement?
- How important is walkability vs. a quieter, more residential feel?
- Is she considering the Mueller property as an alternative to Travis Heights, or is she
  comparing two different lifestyle profiles?
- What is her commute situation — airport Blvd access may matter.
```

**Forward reference appended to Lead Card LEAD-20250514-MRK:**
```
2025-05-15 — Research brief created: RESEARCH-4815-mueller-blvd-20250515.md
```
This entry means Marcus, Priya, or any agent reading Jennifer's Lead Card can locate the Research Brief immediately — without searching `_shared/research/` by address.

### Why this meets team standards
Produces the brief rather than blocking it. The `[ask]` scoping note at the top is specific and actionable — it tells Marcus exactly what is missing and why it matters before the client conversation. Red flags are framed as "verify this" and "confirm with inspector," not "this is a problem." Recommended questions are calibrated to what is unknown about Jennifer specifically — not a generic buyer checklist. The forward reference in the Lead Card closes the loop — any downstream specialist can find this brief by reading the activity log, not by searching the file system. Marcus walks into the showing prepared.

---

## Example 2: ask-field-protocol — Hyde Park bungalow, must_haves and dealbreakers both `[ask]`

### Situation
Sara is previewing a Hyde Park bungalow at 1847 Shoal Creek Blvd listed at $625,000 for clients whose Lead Card has `must_haves: [ask]` and `dealbreakers: [ask]` — intake is still in progress. Sara requests a Research Brief before intake is complete because she wants to preview the property before calling the clients. This is a legitimate request. The research specialist does not block it. The `[ask]` protocol produces a useful brief with a clear limitation noted at the top.

### Context loaded
**From Lead Card (`lead_id: LEAD-20250510-SLR`) — five fields only:**
- budget_min: $560,000 / budget_max: $650,000 — property at $625k is within range
- must_haves: `[ask]`
- dealbreakers: `[ask]`
- target_neighborhoods: Hyde Park, Travis Heights

**From `_config/team-standards.md`:**
- Section loaded: Quality floor
- A brief that makes the agent feel prepared is better than no brief, even with limited scoping. Presenting findings as options — not problems — applies here too.

### Diana's reasoning
Sara is doing the right thing: previewing before calling. The fact that must_haves and dealbreakers are uncaptured is not property research's problem to solve. That belongs to Lead Qualifier. The correct behavior is to give Sara everything that can be researched without client constraints — price analysis, comps, neighborhood profile — and tell her clearly at the top what will change once she finishes intake. A less well-designed specialist would either block the brief ("complete intake first") or silently invent constraints and produce a scoped brief that misleads Sara about what was actually evaluated. Neither is acceptable.

### Output
**Research Brief: 1847 Shoal Creek Blvd, Austin TX 78756**
```
research_id:      RESEARCH-1847-shoal-creek-blvd-20250514
property_address: 1847 Shoal Creek Blvd, Austin TX 78756
linked_lead_id:   LEAD-20250510-SLR
requested_by:     Sara
date:             2025-05-14
status:           draft

⚠ SCOPING NOTE: Client must-haves and dealbreakers not yet captured (LEAD-20250510-SLR).
  Scoping is budget-range only ($560k–$650k). Red flags and talking points reflect general
  Hyde Park buyer considerations only. Recommend completing intake before using this brief
  in a client conversation.

## Price analysis
list_price:       $625,000
suggested_range:  $610,000 – $635,000
confidence:       high
confidence_basis: 5 comps in Hyde Park within 60 days, similar era bungalows
                  (1940s–1950s), 1,200–1,350 sqft. Strong demand at this price band —
                  median 11 days on market.

## Comparable sales
| Address              | Beds/Baths | SqFt  | Sale price | DOM | Sale date  |
|----------------------|------------|-------|------------|-----|------------|
| 1823 Shoal Creek Blvd| 3/1        | 1,280 | $618,000   | 8   | 2025-04-30 |
| 4301 Avenue F        | 3/2        | 1,310 | $629,500   | 14  | 2025-04-18 |
| 4412 Speedway        | 3/1        | 1,240 | $611,000   | 21  | 2025-03-29 |
| 1901 Shoal Creek Blvd| 3/2        | 1,350 | $638,000   | 6   | 2025-05-09 |
| 4308 Avenue G        | 3/1        | 1,195 | $605,000   | 17  | 2025-04-05 |

## Neighborhood profile
walkability:      Very good — Shipe Park, Hyde Park Bar & Grill, Quack's Bakery
                  within walking distance. Central Market 5 min drive.
schools:          Lee Elementary (8/10), Kealing Middle (7/10), McCallum High (8/10)
commute_notes:    Guadalupe to downtown: 15–20 min. No major arterial noise on Shoal Creek.
character:        Established, tree-lined neighborhood. Strong community identity.
                  Mix of long-time residents and newer buyers. Weekend farmers market
                  at Shipe Park draws the neighborhood together.

## Red flags
- 1940s construction: expect deferred maintenance findings in inspection. Common issues
  at this price point: original cast iron plumbing, knob-and-tube wiring in attic,
  pier-and-beam foundation — all manageable but worth budgeting for.
- No garage: street parking only on Shoal Creek. Depends on client's car situation.
- Lot size: 6,250 sqft — standard for Hyde Park. Clients wanting significant outdoor
  space may find this limiting.

## Talking points
- Hyde Park commands a premium because of walkability and community — comps support
  the list price; not much negotiating room.
- 1940s bungalow = character and lot size you cannot get in new construction at this
  price. The trade-off is maintenance.
- Shoal Creek frontage is a walkability asset — trail access one block away.

## Recommended questions to ask client
- Are they comfortable with the maintenance profile of a 1940s home, or do they prefer
  newer construction?
- How important is a garage/off-street parking?
- Is yard size a priority? Hyde Park lots are modest.
```

**Forward reference appended to Lead Card LEAD-20250510-SLR:**
```
2025-05-14 — Research brief created: RESEARCH-1847-shoal-creek-blvd-20250514.md
```
When Sara completes intake and a downstream specialist reads this Lead Card, the activity log tells them a brief exists and where to find it.

### Why this meets team standards
Does not block the brief. Does not invent constraints. Produces complete price analysis, comps, and neighborhood profile with the scoping limitation clearly noted at the top. The forward reference is appended to the Lead Card — the brief is discoverable by anyone reading the activity log, not just Sara. When she completes intake and requests an updated scoped brief, both the original and updated briefs will be visible in the activity log. Sara goes into the preview with real data and the record reflects that this property has been researched.

---

## Example 3: unlinked-brief — Bouldin Creek neighborhood overview, no lead specified

### Situation
Diana wants a general Bouldin Creek neighborhood overview for a buyer she is meeting next week who mentioned the neighborhood in passing. No Lead Card has been created yet — Diana is doing preliminary research before the intake call. She sends: "Can you give me an overview of Bouldin Creek — what's selling, what the neighborhood is like, $600–800k range." No `lead_id` provided. This is a valid unlinked analysis request. The research specialist produces it without asking for a lead_id and notes the absence at the top.

### Context loaded
**From orchestrator context package:**
- Property/area: Bouldin Creek neighborhood, Austin TX
- Price range: $600,000–$800,000 (provided by Diana in the request)
- `lead_id`: not provided — unlinked brief

**From `_config/team-standards.md`:**
- Section loaded: Quality floor
- The brief tells Diana what she needs for a productive first buyer conversation — neighborhood character, realistic price expectations, what to expect in the $600–800k range — not a comprehensive market data dump.

### Diana's reasoning
Unlinked briefs are a legitimate output. Diana is preparing for a meeting, not scoping to a specific client's constraints. The brief should be calibrated to the price range she mentioned, give her talking points she can use to gauge whether Bouldin Creek is actually the right fit for this buyer, and give her questions to ask during intake. A research specialist that asks "can you provide a lead_id first?" is creating a delay that serves no one.

### Output
**Research Brief: Bouldin Creek Neighborhood Overview**
```
research_id:      RESEARCH-bouldin-creek-overview-20250515
property_address: Bouldin Creek, Austin TX 78704 (neighborhood analysis)
linked_lead_id:   unlinked
requested_by:     Diana
date:             2025-05-15
status:           draft

Note: This brief is unlinked — analysis reflects the neighborhood and market at $600k–$800k,
not a specific client's constraints. Recommend completing intake and requesting a
client-scoped brief before a showing.

## Price analysis
Price band: $600,000–$800,000
suggested_range:  $620,000–$780,000 depending on lot, sqft, and renovation level
confidence:       high
confidence_basis: 12 sales in Bouldin Creek in the past 90 days, price band $575k–$830k.
                  Strong buyer demand — median 9 days on market at $700k and below.
                  Above $750k: more negotiating room (median 24 DOM).

## Comparable sales (representative — $600k–$800k range)
| Address           | Beds/Baths | SqFt  | Sale price | DOM | Sale date  |
|-------------------|------------|-------|------------|-----|------------|
| 1512 Bouldin Ave  | 3/2        | 1,420 | $649,000   | 7   | 2025-04-25 |
| 1728 Newning Ave  | 3/2        | 1,650 | $718,500   | 12  | 2025-04-10 |
| 605 W Annie St    | 4/3        | 2,100 | $779,000   | 19  | 2025-03-28 |
| 1603 Bouldin Ave  | 3/2        | 1,580 | $695,000   | 5   | 2025-05-08 |
| 814 W Milton St   | 3/2.5      | 1,850 | $742,000   | 28  | 2025-04-17 |

## Neighborhood profile
walkability:      Excellent — South Congress Ave walking distance, Bouldin Creek Greenbelt
                  trailhead nearby. High walkability score for Austin.
schools:          Becker Elementary (8/10), O. Henry Middle (7/10), Austin High (7/10)
commute_notes:    S Congress to downtown: 15 min drive, 35 min bike. No direct rail;
                  Congress Ave bus is reliable.
character:        South Austin's most walkable, most hip neighborhood. Dense with
                  restaurants, boutiques, and coffee. Mix of original Austinites and newer
                  residents. Higher price per sqft than almost anywhere south of the river.
                  Premium is for the lifestyle, not the square footage.

## Red flags (general — not client-scoped)
- Premium pricing: Bouldin Creek commands $450–520/sqft. Buyers expecting Hyde Park value
  at Bouldin Creek prices will be disappointed.
- Older housing stock: Most homes are 1940s–1960s. Renovation is common and prices
  reflect it — but uninspected renovations are a risk.
- Lot size: Small. $700k often buys 6,000–7,500 sqft lots. Buyers wanting space should
  be flagged.
- S Congress noise: Properties within two blocks of S Congress may have foot traffic and
  bar noise late nights. Matters for clients sensitive to noise.

## Talking points
- Bouldin Creek is one of Austin's most desirable walkable neighborhoods. Buyers who
  prioritize lifestyle over square footage tend to love it.
- At $600–800k, expect 1,400–2,100 sqft, older homes, likely renovated. Character over
  newness.
- The greenbelt access is a major draw for buyers who want outdoor connection from home.

## Recommended intake questions (for client scoping)
- Is walkability a priority, or are they more focused on space?
- How do they feel about older homes with renovation history?
- Do they have a car or commute regularly — the S Congress / downtown drive matters?
- Are they open to properties adjacent to Bouldin Creek (Travis Heights, Zilker) or
  specifically focused on the Bouldin Creek zip?
```

### Why this meets team standards
Produces the unlinked brief immediately — no request for a lead_id. Notes at the top that this is unlinked and recommends completing intake before a showing. Diana gets everything she needs to prepare for the first buyer conversation: realistic price expectations, neighborhood character, red flags to listen for in intake, and specific questions to ask. The brief earns its place in Diana's preparation without pretending to know what this specific buyer cares about.
