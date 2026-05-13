# 01 Lead Qualifier — Handoff Contract

---

## What I receive

From the orchestrator context package:
- Prospect's name, contact information, source of lead
- Any initial intent information the agent has
- OR: existing lead_id when purpose is to update an existing card

---

## What I read

- `_config/team-standards.md` — quality floor and client philosophy sections
  Informs how intake is handled and what standard a completed Lead Card must
  meet before it leaves this specialist.

---

## What I produce

### Create path

A completed Lead Card written to:
`_shared/leads/LEAD-[YYYYMMDD]-[agent-initials].md`

All required fields populated. Fields that cannot be determined from intake
are marked `[ask]` — never left blank, never invented, never estimated.

### Update path

1. Read the full existing Lead Card at the provided lead_id
2. Update only the fields the agent specified as changed
3. Do NOT overwrite the activity log — append only
4. Add change record: `[YYYY-MM-DD] — Card updated: [changed fields] — [agent name]`
5. Return updated card to agent for confirmation before writing

---

## Trigger

- New person with no existing Lead Card → create path
- Agent reports significant change to existing lead's situation → update path

---

## Required fields — Lead Card blocked without all four

1. `budget_min` / `budget_max`
2. `timeline_months`
3. `direction` (buyer | seller | both)
4. `assigned_agent`

---

## Incomplete protocol

### Create path

- Any of the four required fields missing → ask for the missing field before writing.
  One question per field. Do not produce a partial Lead Card.

### Update path

- lead_id missing → ask for it before proceeding.
  Do not create a new card — that creates a duplicate record for the same prospect.
- Ambiguous field changes → confirm which fields changed and new values before writing.
  Do not infer. "Their budget went up" is not sufficient — ask for the new figure.
- No specific changes identified → ask what changed.
  Do not rewrite the card speculatively.
