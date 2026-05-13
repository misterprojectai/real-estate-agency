# 04 Transaction Coordinator — Examples

These examples show transaction coordination judgment in practice — not just what goes in the Deal File, but how Diana's standards for proactive communication and early problem surfacing translate into the specific language of risk flags, open items, and timeline entries. A new agent reading these at 11pm should understand exactly what the Deal File is telling her and what to do next.

---

## Example 1: deal-file-creation — Hyde Park buyer deal, all terms provided

### Situation
Sara's buyers — Maria and David — had their competing offer accepted on the Hyde Park bungalow. The purchase agreement is fully executed as of May 15, 2025. Sara provides all required deal terms with her activation request. The orchestrator routes to TC with the full context package. The stakes: every Texas residential deadline runs from the contract date and closing date. A Deal File created with incomplete dates leaves the team flying blind on the option period, earnest money, and financing deadline — all of which have real legal and financial consequences.

### Context loaded
**From Lead Card (`lead_id: LEAD-20250512-SLR`):**
- deal_type: buyer
- assigned_agent: Sara
- buyer_name: Maria and David Chen
- Buyer pre-approved: yes / lender: HomePoint Financial

**From `_config/buyer-checklist.md`:**
- Version: v1.0, last updated 2025-04-01
- All buyer-side document requirements loaded and copied into Deal File

**From `_config/team-standards.md`:**
- Sections loaded: Non-negotiables + Quality floor
- "Never allows a deadline to pass without surfacing it 48 hours in advance."
- "Every active deal has proactive communication — clients hear from us before they wonder."

### Diana's reasoning
Deal File creation when all terms are present should be mechanical and complete. There is no judgment required about which dates to include — all of them go in. The checklist version is noted because if Diana updates the checklist in July and this deal is still in progress, Sara needs to know which version governed this transaction. Risk Flags and Open Items start empty at creation — but the lender contact confirmation is an Open Item from day one, even if HomePoint is already involved. The first timeline entry is the contract date. Everything else builds from there.

### Output
**Deal File created:**
```
deal_id:          DEAL-20250515-SLR
lead_id:          LEAD-20250512-SLR
created:          2025-05-15
assigned_agent:   Sara
deal_type:        buyer
status:           active

## Property
address:          1847 Shoal Creek Blvd, Austin TX 78756
mls_number:       4521033
list_price:       $625,000
offer_price:      $618,000
accepted_price:   $618,000

## Parties
buyer_name:       Maria and David Chen
buyer_agent:      Sara (Diana's Team)
seller_name:      Thomas and Ann Whitfield
listing_agent:    Ben Rollins, Compass
title_company:    Texas Title — South Austin
title_contact:    Janet Cruz, 512-555-0214
lender:           HomePoint Financial
lender_contact:   Kevin Shaw, 512-555-0381

## Key dates
contract_date:          2025-05-15
option_fee:             $500
option_fee_due:         2025-05-16 (next business day)
option_period_ends:     2025-05-25 (10 days)
earnest_money:          $6,180 (1% of accepted price)
earnest_money_due:      2025-05-19 (3 business days from execution)
financing_deadline:     2025-06-14 (30 days from contract)
inspection_deadline:    2025-05-23 (within option period)
survey_deadline:        2025-05-30 (15 days from contract)
hoa_docs_deadline:      N/A — no HOA
closing_date:           2025-06-20
possession_date:        2025-06-20 (at close)

## Document checklist
[Copied from _config/buyer-checklist.md — v1.0, 2025-04-01]
☐ Purchase Agreement — fully executed
☐ Option Fee receipt
☐ Earnest Money receipt — title confirmation
☐ Pre-approval letter — current, within 60 days
☐ Inspection report
☐ Repair amendment (if applicable)
☐ Survey — new or existing
☐ Title commitment — Schedule A and B
☐ Financing approval letter
☐ Closing Disclosure — 3 business days before close
☐ Final walkthrough confirmation
☐ Deed — signed at closing

## Open items
- Option fee delivery to listing agent confirmed? Sara to verify receipt by EOD 2025-05-16.
- Earnest money wire instructions from Texas Title: Sara to confirm receipt by 2025-05-19.

## Risk flags
[None at creation — all deadlines more than 48 hours out]

## Timeline
2025-05-15 — Purchase agreement fully executed. Deal File opened.
```

### Why this meets team standards
Every Texas-required date is populated. Checklist version is noted. Open Items are initialized with two specific action items that have deadlines within the next 4 days — option fee and earnest money. These are not vague notes; they tell Sara exactly what she needs to confirm and when. Risk Flags are empty at creation because no deadline is within 48 hours yet — but the next time TC reviews this file, the option fee confirmation will either be checked off or become a Risk Flag.

---

## Example 2: risk-flag — financing deadline 48 hours out, lender commitment not confirmed

### Situation
It is June 12, 2025 — two days before the financing deadline on the Hyde Park deal. Maria and David's lender, Kevin Shaw, submitted the commitment letter to underwriting but has not confirmed it has been issued. The financing deadline is June 14. Sara is aware Kevin is working on it but has not received written confirmation. TC reviews the Deal File as part of deadline monitoring and flags the gap. The stakes: if the financing deadline passes without a written commitment, the Whitfields could legally terminate. A reactive call at day 30 cannot save what a proactive one at day 28 can.

### Context loaded
**From Deal File (`deal_id: DEAL-20250515-SLR`):**
- financing_deadline: 2025-06-14
- lender: HomePoint Financial — Kevin Shaw, 512-555-0381
- status: active
- Open items: No confirmed commitment letter on file as of 2025-06-12

**From `_config/team-standards.md`:**
- Sections loaded: Non-negotiables + Quality floor + Financing delay section
- "Never allows a deadline to pass without surfacing it 48 hours in advance."
- "Get ahead of it with title and the other side before it becomes a crisis."
- "A proactive conversation at day 20 saves a deal that a reactive one at day 28 cannot. Financing delays are communication failures as often as they are financial ones."

### Diana's reasoning
The financing deadline is in 48 hours. The commitment letter is not in hand. This is not a problem yet — but it becomes one tomorrow if nothing changes. The Risk Flag should not just say "financing deadline June 14" — that tells Sara the date, which she already knows. It should tell Sara what is not confirmed and what the recommended action is. The financing delay section is explicit: get ahead of it with title and the other side before it becomes a crisis. That means two calls today — Kevin and the listing agent. Not tomorrow.

### Output
**Risk Flag added to Deal File:**
```
## Risk flags
⚠ FINANCING DEADLINE — 2025-06-14 (48 HOURS)
  Status: Financing commitment letter not confirmed as of 2025-06-12.
  Kevin Shaw (HomePoint) — submitted to underwriting, outcome not yet received.

  Recommended action:
  1. Call Kevin Shaw today (512-555-0381) — confirm commitment letter status and
     request written confirmation by EOD 2025-06-12.
  2. Notify Ben Rollins (listing agent) proactively — let him know you are tracking
     this and that you will have written confirmation to him by tomorrow morning.
     A heads-up now prevents an emergency tomorrow.
  3. If Kevin cannot confirm by EOD today — call Texas Title (Janet Cruz, 512-555-0214)
     about the timeline for a one-day extension request if needed.

  Do not wait for Kevin to call you. This is the moment where getting ahead of it
  preserves the deal; waiting does not.
```

**Timeline entry added:**
```
2025-06-12 — Financing deadline 48-hour flag. Commitment letter not yet confirmed.
             Risk Flag opened. Sara notified.
```

### Why this meets team standards
The flag appears at 48 hours — not at 24 hours, not after the deadline. It names what is not confirmed (commitment letter), names who to call (Kevin Shaw, exact phone), and explains the proactive step with the listing agent. The rationale is explicit: "A heads-up now prevents an emergency tomorrow." This is the financing delay section's reasoning applied to TC's specific function — not a date reminder, but a complete situational briefing that tells Sara what Diana would tell her.

---

## Example 3: seller-deal — Barton Hills listing, seller checklist, open items emerging at mid-transaction

### Situation
Diana is representing the Navarros — Robert and Lisa — on the sale of their Barton Hills home at 2847 Barton Skyway. The contract is executed May 20. It is now June 3 — day 14. The buyer's inspector found a knob-and-tube wiring issue in the attic and an aging HVAC system. The buyer's agent has sent a repair amendment requesting $12,000 in seller concessions. The title commitment came back with an old lien from a 2019 contractor — Robert says it was paid, but he does not have the release document. Two open items need to surface simultaneously: the repair amendment decision and the lien release. The Deal File needs to reflect both.

### Context loaded
**From Lead Card (`lead_id: LEAD-20250514-DTS`):**
- deal_type: seller — determines seller checklist, not buyer
- assigned_agent: Diana
- seller: Robert and Lisa Navarro / property: 2847 Barton Skyway
- buying_next: yes — loaded as part of seller profile party context, because a sell-first
  dependency means closing delays on this deal have direct downstream consequences for the
  Navarros' next purchase. This is transaction risk information, not background detail.

**From `_config/seller-checklist.md`:**
- Version: v1.0, last updated 2025-04-01
- Repair amendment and title commitment items relevant to current stage

**From `_config/team-standards.md`:**
- Sections loaded: Non-negotiables + Quality floor
- "Flags problems early, when options still exist — not late, when they don't."
- "Every active deal has proactive communication — clients hear from us before they wonder."

### Diana's reasoning
Two things are happening simultaneously that both need visible tracking. The repair amendment is a negotiation decision with a deadline — the Navarros need to respond before the option period ends (May 30, 10-day period — they are now past option period, but the buyer's agent is asserting repair rights). The lien is a title issue that could delay or kill closing if the release document is not located. A Deal File that does not surface both clearly is a Deal File that will produce an 11pm call to Diana. The Open Items section is where these live — not in a note in Sara's inbox, not in Diana's head.

### Output
**Open items updated:**
```
## Open items
[Updated 2025-06-03]

ITEM 1 — Repair amendment response
  Buyer's agent submitted amendment requesting $12,000 credit (knob-and-tube wiring
  + HVAC). Diana to advise Navarros on response options:
  (a) Accept the $12,000 credit
  (b) Counter with lesser credit or specific repairs only
  (c) Decline — buyer may proceed or terminate
  Option period has ended; buyer asserting repair rights under contract terms.
  Diana needs Navarros' decision by 2025-06-05 (2 days) to respond to buyer's agent.
  → ACTION: Diana to call Navarros today.

ITEM 2 — Lien release for 2019 contractor (Morales Construction)
  Title commitment Schedule B flagged an unsatisfied lien from 2019 from Morales
  Construction, $4,200. Robert Navarro states it was paid.
  Release document not yet located.
  → ACTION: Robert to search for the release document or contact Morales Construction.
  If lien release cannot be produced, title will not issue at closing. Texas Title
  (Janet Cruz) needs this resolved by 2025-06-10 to clear the title commitment.
  If unresolvable, closing date may need to push — impacts Navarros' Mueller purchase
  timeline.
```

**Risk flag added:**
```
## Risk flags
⚠ LIEN RELEASE — REQUIRED BEFORE 2025-06-10
  2019 contractor lien (Morales Construction, $4,200) — unsatisfied on title commitment.
  Robert Navarro states it was paid but release document not located.
  Title cannot clear without this document.
  If unresolved by 2025-06-10: closing date at risk. Navarros' Mueller purchase
  (sell-first dependency) also at risk.
  Contact Janet Cruz (Texas Title, 512-555-0214) with update by 2025-06-08.
```

**Timeline entry:**
```
2025-06-03 — Repair amendment received ($12,000 credit request). 2019 contractor lien
             surfaced on title commitment. Two open items logged. Diana and Navarros
             notified.
```

### Why this meets team standards
Both issues surface in the Deal File simultaneously — not buried in notes, not left for Diana to track mentally. The Open Items give specific action owners (Diana, Robert), specific deadlines, and specific consequences if the deadlines are not met. The Risk Flag for the lien connects it explicitly to the Mueller purchase timeline — the Navarros cannot close on their next home if this one doesn't close on time. A Deal File that does not make that connection visible leaves Diana to figure it out herself. This one does not.
