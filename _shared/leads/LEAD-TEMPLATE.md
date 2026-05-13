# Lead Card — Schema Template

**Location:** `_shared/leads/LEAD-[YYYYMMDD]-[agent-initials].md`
**Created by:** 01_lead_qualifier
**Read by:** 02_property_research, 03_client_communication, 04_transaction_coordinator

---

```
lead_id:          LEAD-[YYYYMMDD]-[agent-initials]
created:          [YYYY-MM-DD]
source:           referral | website | open-house | cold-call | other
assigned_agent:   diana | [agent-2] | [agent-3] | [agent-4]
status:           new | contacted | qualified | nurturing | inactive

## Contact
name:
phone:
email:
preferred_contact: phone | email | text

## Intent
direction:         buyer | seller | both
timeline_months:   [integer — months until target close]
urgency:           1–5  [1 = browsing, 5 = must move now]

## Buyer profile  [complete when direction = buyer or both]
budget_min:
budget_max:
pre_approved:      yes | no | in progress
lender:
target_neighborhoods:
must_haves:
dealbreakers:
owns_currently:    yes | no
selling_first:     yes | no | n/a

## Seller profile  [complete when direction = seller or both]
property_address:
estimated_value:
reason_for_selling:
timeline_flexibility: flexible | firm
buying_next:       yes | no | undecided

## Notes

## Activity log
[YYYY-MM-DD] — [action taken]
```

---

## Required fields — Lead Card is blocked without all four

1. `budget_min` / `budget_max`
2. `timeline_months`
3. `direction`
4. `assigned_agent`

Fields that cannot be determined from intake are marked `[ask]` — never left blank, never invented.

## Activity log conventions

- Append only — never edit or delete existing entries
- Format: `[YYYY-MM-DD] — [action taken] — [agent name if applicable]`
- Research brief forward reference: `[YYYY-MM-DD] — Research brief created: RESEARCH-[slug]-[YYYYMMDD].md`
- Card update record: `[YYYY-MM-DD] — Card updated: [changed fields] — [agent name]`
