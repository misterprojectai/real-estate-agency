# 01 Lead Qualifier — Examples

These examples show intake judgment in practice — not just what fields to fill, but why the standard matters and what goes wrong when it is not met. A new agent reading these before her first lead qualification will understand what Diana expects a completed Lead Card to look like, and why.

---

## Example 1: new-buyer-lead — Travis Heights referral, timeline blocker fires

### Situation
Marcus calls in a referral from a past client — Jennifer Chen, looking to buy in Travis Heights, budget around $550–650k, first-time buyer. He provides good context but does not mention a timeline. The four-field blocker means the Lead Card cannot be written without `timeline_months`. The stakes: if the blocker is ignored and a partial card is written, downstream specialists have no timeline context to work with — property research cannot flag timing-sensitive market conditions, and a communication specialist cannot gauge urgency. A card with a missing required field is worse than no card.

### Context loaded
**From agent-provided information:**
- name: Jennifer Chen — captured
- direction: buyer — captured
- budget_min: $550,000 / budget_max: $650,000 — captured
- assigned_agent: Marcus — captured
- timeline_months: not provided — **blocker fires**
- source: referral — captured
- target_neighborhoods: Travis Heights — captured

**From `_config/team-standards.md`:**
- Section loaded: Quality floor + Client philosophy
- "Knows the answer before the client asks the question" — a Lead Card without a timeline cannot tell an agent how urgently to prioritize follow-up, which affects every downstream interaction.
- "Hard conversations happen early, when they can still change outcomes" — timeline and budget ceiling belong in intake, not discovered at offer time.

### Diana's reasoning
A less experienced intake process might write the card anyway — leaving `timeline_months: [ask]` and moving on. The problem: `[ask]` in a required field means the card is structurally incomplete. The four-field rule is absolute precisely because these four fields are what every downstream specialist needs before they can do useful work. Timeline is not a nice-to-have — it determines how much time the team has to research and prepare before the window closes. One question, one answer, card complete. That is the standard.

### Output
**Blocking question sent to Marcus:**
"What is Jennifer's target timeline? Roughly how many months until she wants to close?"

**Completed Lead Card after Marcus confirms 6 months:**
```
lead_id:          LEAD-20250514-MRK
created:          2025-05-14
source:           referral
assigned_agent:   marcus
status:           new

## Contact
name:             Jennifer Chen
phone:            [ask]
email:            [ask]
preferred_contact: [ask]

## Intent
direction:        buyer
timeline_months:  6
urgency:          3

## Buyer profile
budget_min:       550000
budget_max:       650000
pre_approved:     no
lender:           [ask]
target_neighborhoods: Travis Heights
must_haves:       [ask]
dealbreakers:     [ask]
owns_currently:   no
selling_first:    n/a

## Notes
Referral from past client. First-time buyer. Travis Heights is her stated preference —
Marcus should confirm whether she is open to adjacent neighborhoods (Bouldin Creek,
South Congress area) before any research is scoped.

## Activity log
2025-05-14 — Lead Card created — Marcus
```

### Why this meets team standards
The four-field blocker fires on `timeline_months` and stops card creation with a single targeted question — not a list of everything missing. The card is not written until the blocker is resolved. The notes field captures the context Marcus provided that is not in a structured field — a new agent picking up this lead mid-stream can read the card and understand the situation without a briefing call.

---

## Example 2: new-seller-lead — Barton Hills home, complete intake, buy-after-sell profile

### Situation
Diana is working with Robert and Lisa Navarro — they own a Barton Hills home and want to sell it, then buy in the Mueller or East Austin area. Their direction is `both`: they are sellers first, buyers second. Diana has a full intake conversation and provides complete information. No required fields are missing. The stakes here are not about a blocker — they are about intake quality. A Lead Card that captures only the four required fields passes the minimum bar. A Lead Card that captures the Navarros' full picture tells the next agent who opens it everything she needs to serve them well.

### Context loaded
**From agent-provided information:**
- direction: both (selling Barton Hills, buying Mueller/East Austin) — captured
- budget_min/max: $650,000–$850,000 for their next purchase — captured
- assigned_agent: Diana — captured
- timeline_months: 5 (Diana has a buyer relocating in late fall) — captured
- All contact information, buyer and seller profiles provided

**From `_config/team-standards.md`:**
- Section loaded: Quality floor + Client philosophy
- "Every client receives a response within [committed window]" — a complete Lead Card is what makes that possible for every agent, not just Diana.
- "The client's timeline is the right timeline, not ours" — the Navarros' timeline is driven by Diana's relocating buyer; the card must capture this dependency so whoever touches this lead understands the constraint.

### Diana's reasoning
The Navarros have a sell-first constraint and a timeline tied to a specific buyer Diana is already working with. A minimal Lead Card would capture that they are buyers and sellers with a five-month timeline. A Diana-standard Lead Card captures why the timeline is five months, what their must-haves for the new place are, and that their selling and buying are linked. If Diana is out of town and Priya needs to follow up with the Navarros, Priya should be able to read this card and serve them at Diana's level — without calling Diana.

### Output
**Completed Lead Card:**
```
lead_id:          LEAD-20250514-DTS
created:          2025-05-14
source:           referral
assigned_agent:   diana
status:           qualified

## Contact
name:             Robert and Lisa Navarro
phone:            512-555-0187
email:            rnavarro@email.com
preferred_contact: phone

## Intent
direction:        both
timeline_months:  5
urgency:          4

## Buyer profile
budget_min:       650000
budget_max:       850000
pre_approved:     in progress
lender:           HomePoint Financial — Lisa's contact
target_neighborhoods: Mueller, East Austin, Windsor Park
must_haves:       home office (dedicated room), yard for dog, walkable to coffee
dealbreakers:     HOA with restrictive rental rules, flood zone, busy arterial street
owns_currently:   yes
selling_first:    yes

## Seller profile
property_address: 2847 Barton Skyway, Austin TX 78704
estimated_value:  $775,000
reason_for_selling: Upsizing — current home too small, need dedicated office space
timeline_flexibility: firm
buying_next:      yes

## Notes
Sell and buy are linked — Navarros will not buy until they have an executed contract on
Barton Skyway. Timeline driven by Diana's relocating buyer interested in Barton Hills;
target close on sale is late October. Must-haves for next purchase are non-negotiable —
Robert works from home full-time, dedicated office is the primary driver.

## Activity log
2025-05-14 — Lead Card created — Diana
```

### Why this meets team standards
Every required field is present. The notes field explains the timeline dependency — any agent reading this card understands why the five-month timeline is firm and what drives it. The must-haves and dealbreakers are specific and concrete, not vague placeholders. A Research Brief produced from this card will be scoped to exactly what the Navarros said matters. This is what "knows the answer before the client asks the question" looks like in a Lead Card.

---

## Example 3: update-path — Mueller buyer's budget ceiling shifts after pre-approval increase

### Situation
Priya has been working the Garcia lead — Carlos and Maria Garcia, buyers targeting Mueller at a $580–650k ceiling with a pre-approval in progress. Two months later, their lender came back with a higher pre-approval: $715k. Carlos and Maria want to open their search slightly. Priya routes through the orchestrator, which fires Node 2 and sends the update to Lead Qualifier with `lead_id: LEAD-20250315-PDV`. The stakes: the existing card has a Research Brief scoped to the $580–650k range. Updating only the specified fields and flagging the potentially stale brief is the correct behavior. Rewriting the card wholesale would corrupt the activity log and overwrite context that may still be relevant.

### Context loaded
**From orchestrator context package:**
- `lead_id`: LEAD-20250315-PDV
- Changed fields specified by Priya: `budget_max` ($650,000 → $715,000), `pre_approved` (in progress → yes), `lender` ([ask] → Austin Capital Mortgage, Raj Patel)

**From existing Lead Card (read in full before update):**
- budget_min: 580000 / budget_max: 650000
- pre_approved: in progress / lender: [ask]
- Research Brief activity log entry: `2025-04-02 — Research brief created: RESEARCH-4210-mueller-dr-20250402.md`
- All other fields unchanged

**From `_config/team-standards.md`:**
- Section loaded: Quality floor
- "Every active deal has proactive communication" — updating the record accurately is how the team stays aligned without calling Priya to ask which fields changed.

### Diana's reasoning
A less careful update process might rewrite the whole buyer profile — "their situation changed, so let me refresh everything." That is the wrong call. The activity log, the original budget floor, the must_haves, the dealbreakers — all of these are still accurate. Only three fields changed. Updating only those three protects the integrity of the record. The existing Research Brief was scoped to $650k. The Garcias can now consider properties up to $715k — which means the brief may not reflect the full range of what they can afford. This is worth noting in the update, so Priya knows to consider whether new research is warranted.

### Output
**Fields shown to Priya for confirmation before writing:**
```
budget_max:    $650,000 → $715,000
pre_approved:  in progress → yes
lender:        [ask] → Austin Capital Mortgage — Raj Patel (512-555-0294)
```
"Confirming these three changes to the Garcia Lead Card. The existing Research Brief at `RESEARCH-4210-mueller-dr-20250402.md` was scoped to a $650k ceiling — you may want to request updated research now that their ceiling has increased. Confirm to write."

**Activity log entry appended after confirmation:**
```
2025-05-14 — Card updated: budget_max ($650k → $715k), pre_approved (in progress → yes),
             lender (Austin Capital Mortgage, Raj Patel) — Priya
```

### Why this meets team standards
Only the three specified fields are updated — the rest of the card is untouched. The activity log receives an append, not an overwrite. The agent confirms the changes before they become the canonical record. The note about the potentially stale Research Brief is surfaced in the confirmation step — not buried, not silently resolved, not ignored. Priya now has everything she needs to decide whether to request new analysis before the next showing.
