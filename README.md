# Diana's Agency System

> AI operating system for a boutique real estate team. Five specialists. Explicit handoffs. Diana's judgment, available to every agent, at any hour.

**Status:** Infrastructure complete. Content in progress.

---

## What this system is

[Phase 7 — write after all specialist files are complete and tested]

---

## System map

```
00_orchestrator/          ← every request enters here
├── 01_lead_qualifier/    ← new prospects → Lead Card
├── 02_property_research/ ← property/market analysis → Research Brief
├── 03_client_communication/ ← client drafts in agent voice
└── 04_transaction_coordinator/ ← active deals → Deal File

_shared/                  ← canonical artifacts (leads/, deals/, research/, voices/)
_config/                  ← team-standards.md (all agents) + TX checklists (TC only)
```

---

## Before you start — team setup required

### Step 1 — Complete team-standards.md

Open `_config/team-standards.md`. This file contains a draft built from Diana's brief. Diana reviews, refines, and approves every section before the system goes live. The quality of this file is the quality ceiling for every output the system produces.

Pay particular attention to:
- Quality floor: confirm the response time standard `[Diana confirms]`
- Hard moments playbook: replace generic language with how Diana actually thinks

### Step 2 — Create voice profiles

Open `_shared/voices/`. Four stub files exist — one per agent. Fill in each file before that agent's communications can be drafted.

Diana's file: `diana.md` — fill this first, it is the fallback for all other agents.
Other agents: rename `agent-2-name.md`, `agent-3-name.md`, `agent-4-name.md` to the actual agent first names.

Each voice profile needs: tone descriptors, sentence patterns, characteristic phrases, phrases to avoid, hard conversation style, and sample communications. The more real the samples, the better the drafts.

### Step 3 — Verify TX checklists

Open `_config/buyer-checklist.md` and `_config/seller-checklist.md`. These contain Texas residential contract requirements current as of the last_updated date. If requirements have changed, update and increment the version number.

---

## How a request flows

[Phase 7 — write with real worked examples after testing]

---

## Common scenarios — where to send what

[Phase 7 — cover Diana's specific pain points from the brief]

---

## Onboarding a new agent

[Phase 7 — write so a new agent can be operational in one day without calling Diana]

---

## FAQ

[Phase 7 — cover the questions Diana's newest agent actually asks at 11pm]

---

## System files

| File | Purpose | Built in |
|------|---------|---------|
| `_config/team-standards.md` | Diana's judgment, quality floor, hard moments playbook | Phase 2 |
| `_config/buyer-checklist.md` | TX buyer transaction documents | Phase 2 |
| `_config/seller-checklist.md` | TX seller transaction documents | Phase 2 |
| `_shared/leads/LEAD-TEMPLATE.md` | Lead Card schema | Phase 1 |
| `_shared/research/RESEARCH-TEMPLATE.md` | Research Brief schema | Phase 1 |
| `_shared/deals/DEAL-TEMPLATE.md` | Deal File schema | Phase 1 |
| `_shared/voices/diana.md` | Diana's voice profile | Phase 1 |
| `00_orchestrator/handoff.md` | Triage tree + context package format | Phase 3 |
| `01_lead_qualifier/handoff.md` | Lead Card create + update contracts | Phase 3 |
| `02_property_research/handoff.md` | Research Brief contract | Phase 3 |
| `03_client_communication/handoff.md` | Communication draft contract | Phase 3 |
| `04_transaction_coordinator/handoff.md` | Deal File contract | Phase 3 |

---

*Built for Week 4 of the ICM competition. Architecture specification: `agency-system-architecture-spec.md`*
