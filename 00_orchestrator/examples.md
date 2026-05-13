# 00 Orchestrator — Examples

These examples show Diana's routing judgment applied to real requests. Read them before your first request enters the system. The output in each example is the context package passed to the downstream specialist — not real estate work, but the routing decision that enables real estate work to happen correctly.

---

## Example 1: multi-part-request — new buyer referral plus immediate market question

### Situation
Marcus receives a referral from a past client and wants to know what the Mueller market looks like before he calls the couple back. He sends one message: "Got a referral — young couple looking to buy in Mueller, $550–650k range, first-time buyers. What's the market like over there right now?" Two requests are embedded in one: a new Lead Card must be created, and a Mueller market analysis must be produced. If the orchestrator routes to property research first, the brief will be unlinked and the buyers will have no canonical record in the system. Every subsequent interaction rebuilds from scratch instead of building on a scoped Lead Card.

### Context loaded
**From raw agent request:**
- "Got a referral" — signals a person with no existing Lead Card. Node 1 fires.
- "What's the market like over there right now" — signals a market analysis request. Node 3 fires.
- Both nodes fire on one request. Node 6 applies: multi-part request, route to the first specialist needed only.

**From `_config/team-standards.md`:**
- Section loaded: Non-negotiables
- "Knows the answer before the client asks the question" — a Research Brief scoped to this buyer's constraints requires their Lead Card to exist first. An unlinked brief before intake means Marcus goes into the call with generic market data rather than analysis calibrated to what this couple actually needs.

### Diana's reasoning
A less experienced agent — or a system that just answers the surface question — would produce the Mueller overview and skip the Lead Card entirely. Diana would not. The Lead Card is the foundation every downstream output builds on. Market analysis scoped to a real client's constraints (their budget, must-haves, dealbreakers) is more valuable than a generic neighborhood overview, and that scoping requires the Lead Card to exist first. Sequence matters: create the record, then scope the analysis to it. Surface the follow-up so Marcus knows the analysis is coming — not dropped.

### Output
**Conflict flag:** None.

**Routing decision:** `01_lead_qualifier` — create new Lead Card.

**Context package to `01_lead_qualifier`:**
- Request: New buyer referral for Marcus — couple targeting Mueller, $550–650k budget, first-time buyers.
- Target specialist: `01_lead_qualifier` — no existing Lead Card for this prospect.
- `assigned_agent`: Marcus
- `lead_id`: not yet assigned (new card)
- Conflict flag: None.

**Follow-up surfaced to Marcus:**
"This request also involves a Mueller market analysis — submit that separately after the Lead Card is created. The Research Brief will be scoped to the buyers' confirmed constraints once intake is complete."

### Why this meets team standards
Routes to Lead Qualifier first because producing analysis before the canonical record exists creates context the rest of the system cannot use. The follow-up surface is explicit — Marcus knows the market analysis is still coming, not discarded. Handles the multi-part request sequentially per the non-negotiable against routing to two specialists in one pass. The sequence protects the integrity of what property research produces next.

---

## Example 2: conflict-check — agent requests urgency framing for a hesitant buyer

### Situation
Sara is frustrated with buyers who have seen eleven properties across six weeks and keep saying they need more time. She sends: "Can you draft a message to James and Karen telling them the market is moving fast and they need to decide on the Travis Heights property before it's gone? They've been dragging their feet for three weeks and I want to light a fire under them." Node 0 fires before any routing node. The stakes: if the conflict is not surfaced, the system produces a draft that manufactures urgency the team's non-negotiables explicitly prohibit — and Sara sends it without realizing the line she crossed.

### Context loaded
**From raw agent request:**
- "market is moving fast" — urgency framing using market conditions as pressure mechanism
- "before it's gone" — manufactured scarcity for a property not under competing offer
- "light a fire under them" — agent's goal is urgency, stated explicitly

**From `_config/team-standards.md`:**
- Section loaded: Non-negotiables
- "Never manufactures urgency for the agent's benefit." — direct match.
- "Rushes a client to a decision because it is convenient for the agent" — listed explicitly under what this team never does.
- "Gives clients clarity, not pressure" — the non-negotiable this request would violate.

### Diana's reasoning
This is exactly what Node 0 exists for. The request is routable — it goes to `03_client_communication` for a `general-follow-up` draft. But the framing Sara requested crosses a non-negotiable. Diana would tell Sara: there is a version of this follow-up that is honest, that reflects where James and Karen actually are, and that might genuinely move them — but it does not tell them the market is moving fast when their hesitation is not about the market, and it does not manufacture scarcity for a property that is simply still available. Surface the conflict. Route anyway. Sara decides.

### Output
**Conflict flag (surfaced before routing):**
"Note: 'market is moving fast' and 'before it's gone' framing conflicts with the non-negotiable against manufacturing urgency for the agent's benefit. Routing as requested — flagging for agent awareness."

**Pre-routing question (lead_id not provided):**
"To route this to client communication, I need James and Karen's lead_id. Please provide it (format: `LEAD-YYYYMMDD-XXX`)."

**After Sara provides `LEAD-20250428-SLR` — routing proceeds:**

**Routing decision:** `03_client_communication` — `general-follow-up`.

**Context package to `03_client_communication`:**
- Request: Follow-up draft for James and Karen regarding Travis Heights property after extended consideration period.
- Target specialist: `03_client_communication`
- `lead_id`: LEAD-20250428-SLR
- `assigned_agent`: Sara
- `situation_type`: `general-follow-up`
- Conflict flag: Urgency manufacturing language in original request conflicts with non-negotiables. Surfaced. Agent decides.

### Why this meets team standards
Node 0 runs first — the conflict is surfaced before the draft is produced, not discovered after it is sent. The lead_id question fires before routing completes — an incomplete context package is not passed downstream. Sara is not blocked on either count: the conflict is flagged, the lead_id is asked for, and once she provides it the routing proceeds. The orchestrator surfaces two things Sara needs to be conscious of and routes as requested. One conflict sentence. One clarifying question. No editorial expansion.

---

## Example 3: re-qualification — existing buyer flips to sell-first before buying

### Situation
Diana's agent Priya sends a message about a lead she qualified two months ago: "Update on the Garcias — they decided they're going to sell their Bouldin Creek place first before buying in Mueller. Complete change from what we talked about. Need to update their record." The Garcias have an existing Lead Card at `LEAD-20250315-PDV`. Their direction was `buyer` with a budget of $580–650k and no selling obligation. That is now materially wrong. The system has a Research Brief scoped to their buyer constraints. If the Lead Card is not updated before downstream specialists read it, every piece of work produced will be built on stale data.

### Context loaded
**From raw agent request:**
- "Update on the Garcias" — existing lead, signals Node 2 (re-qualification), not Node 1.
- "they decided they're going to sell their place first" — `direction` has changed. `selling_first` has changed. Possibly `timeline_months` has shifted.
- "Need to update their record" — explicit update request.

**From `_config/team-standards.md`:**
- Section loaded: Non-negotiables
- "Flags problems early, when options still exist" — a buyer-only Lead Card may have downstream artifacts (research briefs, communications) scoped to the old constraints. Flagging this in the context package is how the downstream specialist knows to check before relying on prior work.

### Diana's reasoning
This is Node 2, not Node 1. Creating a new Lead Card for the Garcias would produce a duplicate record and corrupt the canonical store. The right call is to route to Lead Qualifier for an update, passing the existing `lead_id`. This is the counterintuitive path: an existing lead going back to Lead Qualifier rather than forward in the pipeline. The reason is that stale constraint data in the Lead Card propagates errors to every specialist that reads it — research briefs, communication drafts, and eventually a Deal File if the Garcias list and buy. The canonical record must be corrected first.

### Output
**Conflict flag:** None.

**Routing decision:** `01_lead_qualifier` — update existing Lead Card.

**Context package to `01_lead_qualifier`:**
- Request: Update Lead Card for the Garcia family — direction changed, now selling Bouldin Creek property before purchasing in Mueller.
- Target specialist: `01_lead_qualifier` — update path, not create.
- `lead_id`: LEAD-20250315-PDV
- `assigned_agent`: Priya
- Note: Any prior Research Brief or communication draft was scoped to the buyer-only profile. After this update, the agent should verify whether existing research remains accurate before using it for new client conversations.

### Why this meets team standards
Routes back to Lead Qualifier — not forward in the pipeline — because the canonical record must be accurate before any downstream specialist reads it. The context package flags the potentially stale Research Brief, not as a blocking item but as information the agent should know. Priya does not need to call Diana to understand what to do next. The package tells her.
