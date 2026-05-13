# 03 Client Communication — Handoff Contract

---

## What I receive

From the orchestrator context package:
- `lead_id` (required)
- `situation_type` from controlled vocabulary below (required)
- `assigned_agent` name (required)
- Any specific content to include in the draft (optional)
- `research_id` if communication follows a showing or property discussion (optional)

---

## Situation type — controlled vocabulary

Use exactly one of these values. No free-form situation descriptions.

```
new-prospect-follow-up
showing-follow-up
offer-submitted
competing-offer
inspection-response
financing-delay
closing-update
missed-appointment
general-follow-up
```

---

## What I read

### Lead Card at lead_id — full document

Client context, intent, constraints, activity history.

### `_shared/voices/[assigned_agent].md` — assigned agent's file only

I NEVER load all four voice files.
I load only the file that matches the assigned_agent value from the context package.
Voice bleed between agents is architecturally prevented — not managed by prompt.

This file determines how the communication sounds.

### Research Brief at research_id — if provided

Grounds communication in specific property details.
Loaded only when orchestrator includes a research_id in the context package.

### `_config/team-standards.md` — full document

This is the primary quality reference for every draft.

Voice profile = how the communication sounds.
Team standards = what the communication stands for.
Both are required. Neither alone is sufficient.

The hard moments playbook is the direct reference for:
- `competing-offer` situations
- `inspection-response` situations
- `financing-delay` situations

---

## What I produce

A complete communication draft returned directly to the agent:
- Full draft text (complete, ready to use — not a summary or outline)
- Situation type
- Tone notes
- Recommended send time
- Suggested follow-up trigger

---

## Trigger

Agent needs to communicate with a client in any situation in the controlled vocabulary.

---

## Incomplete protocol

- `lead_id` missing → ask before drafting. Client context is required.

- `assigned_agent` missing → ask before drafting. Voice file cannot load without name.

- `situation_type` missing or not in vocabulary → ask the agent to describe the
  situation in one sentence. Map to closest vocabulary entry. Confirm before drafting.

- Voice file missing for assigned agent → notify:
  "No voice profile found for [name]. This draft will use Diana's profile as default.
  Create _shared/voices/[name].md before next use."
  Proceed with Diana's profile. Do not block the draft.
