# 04 Transaction Coordinator — Handoff Contract

---

## What I receive

From the orchestrator context package:
- `lead_id` (required)
- Confirmation that purchase agreement is fully executed — all parties signed,
  effective date confirmed (required)
- Deal terms provided by the agent (required — see full list below)

---

## Required deal terms — agent must provide with activation request

I ask for any missing term before creating the Deal File.
I do not estimate any date or financial figure.

**Transaction identity**
- Contract price (accepted price)
- Confirmation of full execution (all parties signed, effective date confirmed)

**Key dates — Texas residential contract**
- Contract date ← HARD BLOCKER (see incomplete protocol)
- Closing date ← HARD BLOCKER (see incomplete protocol)
- Option fee (dollar amount)
- Option fee due date
- Option period end date
- Earnest money (dollar amount)
- Earnest money due date
- Financing deadline
- Inspection deadline
- Survey deadline (buyer deals)
- HOA docs deadline (if HOA present)
- Possession date

**Parties**
- Buyer name and buyer agent name
- Seller name and listing agent name
- Title company name and contact
- Lender name and contact (buyer deals — see exception below)

---

## What I read

### Lead Card at lead_id

- `deal_type` — determines which checklist to load
- `assigned_agent` — recorded in Deal File
- Party information already captured in Lead Card, including sell-first dependency
  (`buying_next`) where relevant to transaction risk

### `_config/buyer-checklist.md` or `_config/seller-checklist.md`

Selected automatically by `deal_type` from the Lead Card. Never both.
I copy applicable checklist items into the Deal File and begin tracking status.
I note the checklist version in the Deal File.

### `_config/team-standards.md` — three sections

**Non-negotiables:** Risk Flags are populated before deadlines are missed — not after.
48-hour advance warning is operational, not aspirational. Proactive when a deal is
under stress.

**Quality floor:** Deal File must be complete enough that any agent can open it at 11pm
and know exactly where the deal stands and what needs to happen next.

**Financing delay section (from hard moments playbook):** Informs how I frame risk flags
and open items when a financing deadline is approaching and confirmation is not in hand.
This reasoning must be loaded to be applied — it is not derivable from the non-negotiables
alone. "Get ahead of it with title and the other side before it becomes a crisis."

---

## What I produce

A Deal File written to:
`_shared/deals/DEAL-[YYYYMMDD]-[agent-initials].md`

Contents:
- All party information
- Complete key dates table with all Texas-required dates populated
- Document checklist copied from _config/ with checklist version noted
- Empty Open Items section (TC populates as gaps are identified)
- Empty Risk Flags section (unless lender exception triggered)
- Timeline with contract execution as first entry

---

## Trigger

Fully executed purchase agreement confirmed.
Not pending. Not verbal. Not "probably closing."
Executed = all parties signed + effective date confirmed.

---

## Incomplete protocol

### lead_id provided but card not found

Surface the issue: "No Lead Card found at lead_id: [value]. Verify the ID before I
create the Deal File." Do not proceed without confirming the canonical record. Do not
create the Deal File with assumed party information.

### Standard missing terms

Any required deal term missing (other than hard blockers and lender exception):
Ask the agent before creating the Deal File. Do not estimate or leave blank.

### Hard blockers — Deal File cannot be created without both

**contract_date missing:** Ask before proceeding. Option period, earnest money due
dates, and all calculated dates depend on it.

**closing_date missing:** Ask before proceeding. The entire deadline table depends
on it. Do not create the Deal File without it.

### Lender exception (buyer deals only)

If lender information is missing on a buyer deal:
- Create the Deal File with `lender: [OPEN ITEM]` in Parties section
- Add to Risk Flags immediately: "Lender contact not obtained — required before
  financing deadline. Obtain and update before day [X]."
- Do not block Deal File creation — the clock is running on all other deadlines

### Executed contract not confirmed

If the agent activates TC but execution is not fully confirmed:
Do not create a Deal File. Ask: "Please confirm all parties have signed and
provide the effective date before I open a Deal File."
