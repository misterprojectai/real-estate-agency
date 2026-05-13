# Agency System — Operations Manual

**Diana's Boutique Real Estate Team | Austin, TX**

---

## What this system is

This system externalizes Diana. Every folder holds a piece of what Diana knows, how Diana thinks, and what her team stands for — her routing judgment, her client standards, her eight years of situational reasoning. A new agent who opens this system at 10:45pm finds Diana's answer before she has to ask Diana the question. The system is five specialist folders organized around a shared canonical store. Every request enters through the orchestrator, which routes to the right specialist. Specialists do not call each other — they read from and write to `_shared/`. Nothing requires installation. Nothing requires a developer. The folder structure is the system.

---

## Quick start

If you have completed team setup (Section 3 below), here is how you use the system:

1. Open Claude Code in the `agency-system/` folder
2. Describe your request in plain language: "I have a new buyer referral" or "Need to prep for a showing on a Mueller property" or "Client asking about the inspection finding"
3. The orchestrator routes to the right specialist and produces the output

If you have not completed team setup, start at Section 3.

---

## System map

```
                    ┌─────────────────────────────────────┐
                    │          00 Orchestrator             │
                    │   Conflict check + routing only      │
                    │   Reads every request first          │
                    └──────────────┬──────────────────────┘
                                   │ routes to one specialist
          ┌────────────────────────┼────────────────────────────┐
          │                        │                            │
  ┌───────▼──────┐     ┌───────────▼──────┐    ┌───────────────▼────────┐   ┌──────────────────────┐
  │  01 Lead     │     │  02 Property     │    │  03 Client             │   │  04 Transaction      │
  │  Qualifier   │     │  Research        │    │  Communication         │   │  Coordinator         │
  │              │     │                  │    │                        │   │                      │
  │ Creates and  │     │ Produces         │    │ Drafts all client      │   │ Opens and maintains  │
  │ updates Lead │     │ Research Briefs  │    │ communications using   │   │ Deal Files from      │
  │ Cards        │     │ scoped to client │    │ voice profile +        │   │ contract to close    │
  └───────┬──────┘     └───────────┬──────┘    │ team standards         │   └──────────┬───────────┘
          │                        │           └───────────────┬────────┘              │
          └────────────────────────┼───────────────────────────┘                       │
                                   │ reads from / writes to                             │
                    ┌──────────────▼───────────────────────────────────────────────────┘
                    │                      _shared/                                     │
                    │  leads/       → Lead Cards (one per prospect)                     │
                    │  research/    → Research Briefs (one per property/analysis)       │
                    │  deals/       → Deal Files (one per active transaction)           │
                    │  voices/      → Agent voice profiles (one per agent)              │
                    └──────────────────────────────────────────────────────────────────┘
                    ┌──────────────────────────────────────────────────────────────────┐
                    │                      _config/                                     │
                    │  team-standards.md       ← loaded by ALL specialists, every run  │
                    │  buyer-checklist.md  ┐                                            │
                    │  seller-checklist.md ┘  ← loaded by TC only, per deal type       │
                    └──────────────────────────────────────────────────────────────────┘
```

**How to read this map:**
- Every request enters through the Orchestrator — there is no path that bypasses it
- The Orchestrator routes to one specialist at a time
- All four specialists read from `_shared/` using artifact IDs (no specialist calls another directly)
- `team-standards.md` is loaded by every specialist on every run — it is Diana's standard, always present
- The TX checklists are loaded by TC only, selected by deal type

---

## Section 3 — Before you start (team setup)

**This section must be completed before any agent uses the system.** The system cannot produce useful output without it. Setup takes 2–4 hours total, most of which is Diana's time.

---

### 3.1 — Diana: Complete `_config/team-standards.md`

**This is the most important file in the system.** Every specialist loads it on every run. The quality of this file is the quality ceiling for everything the system produces. Generic content here produces generic outputs everywhere.

Open `_config/team-standards.md`. The file has placeholder notes from Diana's brief — it is a starting point, not the finished product. Diana must review and rewrite each section in her own words before the system goes live.

**Five sections Diana must complete:**

| Section | What it contains | Why it matters |
|---|---|---|
| Quality floor | Response time commitments, 48-hour deadline rule | Governs every specialist's standard |
| Non-negotiables | What this team always does / never does | Orchestrator checks these before every routing decision |
| Client philosophy | Why the team is small, what advocacy means | Shapes every client communication draft |
| Hard moments playbook | Competing offers, inspection issues, financing delays, client hesitation, deal falling apart | Direct reference for the three hardest communication types |
| Version header | `last_updated` date + version number | Tracks when Diana's thinking evolves |

**How to update it over time:** When Diana's philosophy evolves — after a hard deal, when a new agent joins, when the team learns something — open the file, update the relevant section, increment the version number, update `last_updated`. The system reads the current version on every run.

**What happens if it has generic content:** The system produces outputs that could belong to any real estate team. The Diana-specificity test: could this output be lifted unchanged into a competitor's system? If yes, it fails. Diana's willingness to put her actual thinking into this file is the only thing that prevents that.

---

### 3.2 — Diana: Complete `_shared/voices/diana.md`

Diana's voice profile is the fallback for all other agents. When a voice file is missing for an assigned agent, the system uses Diana's. Diana fills this first.

Open `_shared/voices/diana.md`. The stub has section headers — fill each one with honest, specific content:

- **Tone descriptors:** How Diana sounds. Two or three words is not enough — be specific. "Direct but never cold. Gets to the point without feeling rushed."
- **Sentence patterns:** Does she write in short punchy sentences or longer explanatory ones? Does she use contractions?
- **Phrases she uses:** Real phrases from real emails Diana has sent.
- **Phrases she never uses:** What sounds wrong coming from Diana.
- **Hard situation guidance:** How Diana's voice changes when delivering bad news, when pushing back, when a client is emotional.
- **Sample text:** Paste 2–3 actual emails Diana has sent. This is the highest-value input — the system anchors to real examples.

**The more real the sample communications, the better every draft.** A voice profile with three real emails produces noticeably better output than one with only description.

---

### 3.3 — Each agent: Complete your voice profile

Open `_shared/voices/`. You will see stubs named `agent-2-name.md`, `agent-3-name.md`, `agent-4-name.md`.

**Step 1:** Rename the file to your first name. `sara.md`, `marcus.md`, `priya.md`. The filename must match how you appear in `assigned_agent` fields in Lead Cards.

**Step 2:** Fill the profile using the same sections as Diana's. Paste real emails you have sent as sample text. Be honest about your voice — the system uses it to produce drafts in your name.

**Step 3:** Diana reviews and confirms the profile sounds right before you start using the system.

A voice profile does not need to be perfect to be useful. A first draft with real sample text is better than a polished description with no examples.

---

## Section 4 — How a request flows

Every request passes through the Orchestrator's triage tree. Here is the tree in plain language, with examples.

```
Does the request conflict with a team non-negotiable?
  YES → Orchestrator flags it in one sentence, then routes anyway. Agent decides.

Is this a new person with no Lead Card?
  YES → 01 Lead Qualifier (create new card)

Did an existing lead's situation change significantly?
  YES → 01 Lead Qualifier (update existing card — pass the lead_id)

Does the request name a specific property, address, or neighborhood for analysis?
  YES → 02 Property Research

Does the request need a communication drafted or sent to a client?
  YES → 03 Client Communication

Is there a fully executed purchase agreement?
  YES → 04 Transaction Coordinator

Does the request span more than one specialist?
  YES → Orchestrator routes to the first one. Tells you to submit the second separately.

Still unclear?
  → Orchestrator asks one clarifying question, then routes.
```

**Worked examples:**

| Your request | Where it routes | Why |
|---|---|---|
| "Got a new buyer referral from Jennifer" | 01 Lead Qualifier | New person, no Lead Card |
| "The Garcias moved their budget up to $715k" | 01 Lead Qualifier | Existing lead, situation changed |
| "Need to prep for a showing at 4815 Mueller Blvd" | 02 Property Research | Named property for analysis |
| "Follow up with Maria and David after yesterday's showing" | 03 Client Communication | Client communication needed |
| "Contract executed on the Hyde Park property — need to open the deal" | 04 Transaction Coordinator | Fully executed purchase agreement |
| "Draft a message to my clients telling them they need to decide now or lose the house" | 03 Client Communication + conflict flag | Routes to comms AND flags urgency manufacturing |

**Multi-part requests:** "Got a new referral and want to know what Mueller looks like" — the orchestrator routes to Lead Qualifier first, then tells you to submit the market analysis separately after the Lead Card is created. Never both in one pass.

---

## Section 5 — Common scenarios

**Scenario 1: New lead just called or texted**
Say: "I have a new [buyer/seller] lead — [name], [brief context]."
Orchestrator routes to Lead Qualifier. You answer a few intake questions. Lead Card created and filed.

**Scenario 2: Preparing for a showing**
Say: "I need to prep for a showing at [address] for [client name or lead_id]."
Orchestrator routes to Property Research. Research Brief produced and scoped to client's constraints if a Lead Card exists.

**Scenario 3: Deal just went under contract**
Say: "Contract executed on [address] — [client name] deal. Here are the terms: [list all deal terms]."
Orchestrator routes to Transaction Coordinator. Deal File created with all TX deadlines and document checklist.

**Scenario 4: 11pm — agent needs to know what document is still missing**
Open the Deal File in `_shared/deals/`. The Document Checklist, Open Items, and Risk Flags sections tell you exactly what is missing and what needs to happen next. No call to Diana required.

**Scenario 5: Client communication needed**
Say: "I need to [follow up with / respond to / update] [client name] about [situation]."
Orchestrator maps the situation to the vocabulary, routes to Client Communication. Draft produced in your voice, applying team standards.

**Scenario 6: Deadline approaching on an active deal**
Any deadline within 48 hours that is not fully resolved appears in Risk Flags in the Deal File with a recommended action. Check the Deal File before assuming everything is on track.

**Scenario 7: Existing client's situation changed**
Say: "Update on [client name] — [what changed]. Here is the new information."
Orchestrator fires the re-qualification path (Node 2) and routes to Lead Qualifier to update the existing card. The Lead Card is updated before any downstream specialist reads stale data.

---

## Section 6 — Onboarding a new agent

Complete these steps in order. A new agent should be operational by end of day one.

**Before the agent's first day:**
- [ ] Diana completes `_config/team-standards.md` (if not already done)
- [ ] Diana's voice profile (`diana.md`) is complete and reviewed
- [ ] A stub voice file exists for the new agent (copy `agent-N-name.md`, rename to their first name)

**Day 1 — Morning (1–2 hours):**
- [ ] New agent reads `_config/team-standards.md` in full — this is how Diana's team operates
- [ ] New agent reads all five `examples.md` files — one per specialist. Start with `00_orchestrator/examples.md`. These function as training material independent of the AI system. A new agent who reads them before her first transaction will be more prepared than one who has not, whether or not she ever opens the AI system.
- [ ] New agent fills her voice profile (`_shared/voices/[name].md`) using real sample emails
- [ ] Diana reviews and confirms the voice profile

**Day 1 — Afternoon (first use):**
- [ ] New agent's first real request: enter a lead she is working on. Lead Qualifier walks the intake.
- [ ] New agent reviews the completed Lead Card. Does it look right?
- [ ] If a deal is active: open the Deal File. Review the key dates and document checklist.
- [ ] New agent reads `handoff.md` for the specialists she will use most (Lead Qualifier, Client Communication at minimum).

**What a new agent can do on day 1 without calling Diana:**
- Qualify a new lead
- Request property research for a showing
- Draft a client communication in her own voice
- Open a Deal File on an executed contract
- Know what every active deadline is and whether any are at risk

---

## Section 7 — FAQ

**"How do I know which specialist handles my request?"**
Describe the request in plain language. The orchestrator routes it. If you want to understand the routing logic, read `00_orchestrator/handoff.md` — the full triage tree is there.

**"What if I don't know the lead_id?"**
Lead IDs follow the format `LEAD-YYYYMMDD-XXX`. Find them in `_shared/leads/` — the filename IS the lead_id. If you cannot find it, ask the orchestrator: "What is the lead_id for [client name]?" and it will tell you where to look.

**"My client's situation changed — do I create a new Lead Card?"**
No. Never create a duplicate. Describe what changed to the orchestrator: "Update on [client name] — [what changed]." The orchestrator routes to Lead Qualifier to update the existing card.

**"The system drafted an email that doesn't sound like me."**
Your voice profile needs more real sample text. Open `_shared/voices/[your name].md` and paste 2–3 actual emails you have sent. The more specific and real, the better. After updating, the next draft will be noticeably more accurate.

**"A deadline passed and it wasn't flagged."**
Open the Deal File. Check Risk Flags and the Timeline. If the deadline is there but was not surfaced at 48 hours, the Deal File may not have been reviewed in time. The system flags when reviewed — it does not run on a cron job. Build the habit of checking active Deal Files daily.

**"The system is asking me to do something that feels wrong."**
Trust that instinct. Read the non-negotiables section of `_config/team-standards.md`. If the system is producing output that conflicts with the team's values, the conflict flag mechanism should have surfaced it. If it didn't, Diana should update `team-standards.md` to make the principle explicit. The system reflects what is written in that file.

**"When should I update team-standards.md?"**
When Diana's thinking evolves. After a hard deal, if a new principle emerged. When a new agent joins and the team articulates something that was previously implicit. When a recurring situation type shows up that the current playbook doesn't cover. Update the file, increment the version number, update `last_updated`. All future runs use the new version. Deals already in progress under the old version continue on that version.

**"What if I need to do something the system doesn't handle?"**
The system handles: lead qualification, property research, client communications, and transaction coordination. It does not handle: showing scheduling, MLS management, accounting, contract drafting, or legal advice. For anything outside the five specialist domains, use your existing tools. The system supplements Diana's judgment — it does not replace professional expertise.

---

## File index

```
agency-system/
├── README.md                    ← you are here
│
├── _shared/                     ← all artifacts that cross specialist boundaries
│   ├── leads/                   ← Lead Cards — LEAD-YYYYMMDD-XXX.md
│   ├── research/                ← Research Briefs — RESEARCH-[address-slug]-YYYYMMDD.md
│   ├── deals/                   ← Deal Files — DEAL-YYYYMMDD-XXX.md
│   └── voices/                  ← Agent voice profiles — [firstname].md
│
├── _config/                     ← stable reference material, loaded every run
│   ├── team-standards.md        ← Diana's judgment, quality floor, hard moments playbook
│   ├── buyer-checklist.md       ← TX buyer transaction document requirements (versioned)
│   └── seller-checklist.md      ← TX seller transaction document requirements (versioned)
│
├── 00_orchestrator/             ← conflict check + routing — every request enters here
├── 01_lead_qualifier/           ← Lead Card creation and updates
├── 02_property_research/        ← Research Brief production
├── 03_client_communication/     ← Client communication drafts
└── 04_transaction_coordinator/  ← Deal File creation and maintenance

Each specialist folder contains:
  identity.md   ← who this specialist is, what it owns, what it does not own
  rules.md      ← behavioral rules, never/always, how it handles incomplete input
  handoff.md    ← complete contract: receive / reads / produce / trigger / incomplete protocol
  examples.md   ← judgment library: three situations, Diana's reasoning made visible
```

---

*Built with ICM — Interpretable Context Methodology (Van Clief & McDermott, arXiv:2603.16021)*
*Folder structure is the architecture. Everything a code framework manages in application logic is encoded here instead.*
