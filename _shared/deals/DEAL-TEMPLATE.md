# Deal File — Schema Template

**Location:** `_shared/deals/DEAL-[YYYYMMDD]-[agent-initials].md`
**Created by:** 04_transaction_coordinator
**Maintained by:** 04_transaction_coordinator through close

Not created until purchase agreement is fully executed — all parties signed, effective date confirmed.

---

```
deal_id:          DEAL-[YYYYMMDD]-[agent-initials]
lead_id:          LEAD-[YYYYMMDD]-[agent-initials]
created:          [YYYY-MM-DD]
assigned_agent:   [agent name]
deal_type:        buyer | seller
status:           pending | active | closing | closed | fallen

## Property
address:
mls_number:
list_price:
offer_price:
accepted_price:

## Parties
buyer_name:
buyer_agent:
seller_name:
listing_agent:
title_company:
title_contact:
lender:           [buyer deals — OPEN ITEM if not yet obtained]
lender_contact:   [buyer deals — OPEN ITEM if not yet obtained]

## Key dates
contract_date:
option_fee:
option_fee_due:
option_period_ends:
earnest_money:
earnest_money_due:
financing_deadline:
inspection_deadline:
survey_deadline:      [buyer deals]
hoa_docs_deadline:    [if HOA present]
closing_date:
possession_date:

## Document checklist
[TC copies applicable items from _config/buyer-checklist.md or
 _config/seller-checklist.md per deal_type and tracks status here.
 Checklist version used: see last_updated in _config/ file.]

## Open items
[TC populates as gaps are identified — who owes what to whom]

## Risk flags
[TC populates when deadlines are at risk — 48 hours minimum advance warning]

## Timeline
[YYYY-MM-DD] — Contract executed
[YYYY-MM-DD] — [subsequent events]
```

---

## Hard blockers — Deal File cannot be created without both

- `contract_date` — all calculated dates depend on it
- `closing_date` — entire deadline table depends on it

## Lender exception

If lender information is missing on a buyer deal:
- Create the Deal File with `lender: [OPEN ITEM]`
- Add to Risk Flags: "Lender contact not obtained — required before financing deadline"
- Do not block Deal File creation

## Checklist versioning

Note which checklist version was used when creating the Deal File.
Active deals do not inherit new checklist requirements mid-transaction.
