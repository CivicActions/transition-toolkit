# Prompt: Transition Package

Assemble the complete outbound transition package for `{{PROJECT_NAME}}`.

## Context

- Codebase: `{{REPO_ROOT}}`
- Outgoing team lead: `{{OUTGOING_LEAD}}`
- Successor team lead: `{{SUCCESSOR_LEAD}}`
- Handover target date: `{{HANDOVER_DATE}}`
- Successor team roles: `{{SUCCESSOR_ROLES}}`

---

## Instructions

Assemble, validate, and index all transition artifacts. This prompt does not generate new documentation — it validates that what exists is current and packages it for handover.

For each artifact below: verify it exists, verify it is current (last update vs. last relevant codebase change), and record its status.

---

### Part 1 — Knowledge base audit

| Artifact | Expected path | Exists? | Last updated | Current? | Gaps or issues |
|---|---|---|---|---|---|
| System overview | `baseline/01-architecture-map.md` | Y/N | … | Y/N | … |
| Hotspot analysis | `baseline/02-hotspot-analysis.md` | Y/N | … | Y/N | … |
| ADR index | `baseline/03-adr-archaeology/README.md` | Y/N | … | Y/N | … |
| Tech debt inventory | `baseline/04-tech-debt-inventory.md` | Y/N | … | Y/N | … |
| Domain glossary | `baseline/05-domain-glossary.md` | Y/N | … | Y/N | … |
| Onboarding paths | `baseline/06-onboarding-paths/` | Y/N | … | Y/N | … |
| Comprehension checks | `baseline/07-comprehension-checks/` | Y/N | … | Y/N | … |
| Runbooks | `{{RUNBOOK_PATHS}}` | Y/N | … | Y/N | … |
| Postmortems | `postmortems/` | Y/N | … | Y/N | … |
| Scope and gap register | `baseline/00-scope.md` | Y/N | … | Y/N | … |

For any artifact marked **Not current** or **Gaps**, record a remediation task:

| Task | Priority | Owner | Due before handover? |
|---|---|---|---|
| Update `01-architecture-map.md` to reflect `{{RECENT_CHANGE}}` | High | `{{OWNER}}` | Yes |

---

### Part 2 — Risk and hotspot map (current)

Generate a current risk summary from:
1. `baseline/02-hotspot-analysis.md` (re-run `prompts/hotspot-analysis.md` if more than 4 weeks old)
2. `baseline/04-tech-debt-inventory.md`
3. `postmortems/` — count incidents per subsystem

Produce a single ranked risk table:

| Rank | Subsystem | Risk level | Churn rank | Incident count | Open debt items | Why the successor team should care |
|---|---|---|---|---|---|---|
| 1 | … | Critical | … | … | … | … |

---

### Part 3 — Operational runbook completeness

List every operational procedure required to run this system in production:

| Procedure | Runbook exists? | Location | Last tested | Missing steps? |
|---|---|---|---|---|
| Deploy to production | Y/N | `{{PATH}}` | `{{DATE}}` | Y/N |
| Roll back a deployment | Y/N | … | … | Y/N |
| Respond to `{{CRITICAL_ALERT}}` | Y/N | … | … | Y/N |
| Rotate credentials / secrets | Y/N | … | … | Y/N |
| Scale up / down | Y/N | … | … | Y/N |
| Database backup and restore | Y/N | … | … | Y/N |
| `{{OTHER_PROCEDURES}}` | Y/N | … | … | Y/N |

Any missing runbook for a Critical or High risk procedure is a **handover blocker**.

---

### Part 4 — AI assistant and tooling transfer guide

Document exactly how to transfer the AI-augmented workflow to the successor team:

#### AI assistant configuration

- What corpus does the assistant use? (List sources: `baseline/`, codebase, external docs)
- Where is the assistant configuration stored?
- How is it updated when the knowledge base changes?
- What access or credentials does it need?
- Steps to transfer to the successor team's environment:
  1. …
  2. …

#### AI-augmented workflow components

For each automated component:

| Component | What it does | Where it's configured | How to operate it | Transfer steps |
|---|---|---|---|---|
| PR documentation draft | Drafts doc updates on PR | `{{CONFIG_PATH}}` | `{{OPERATION_NOTES}}` | `{{STEPS}}` |
| Convention compliance check | Reviews PRs against project conventions | … | … | … |
| Postmortem drafting | Drafts postmortems from incident transcripts | … | … | … |

#### Enablement sessions

List the sessions the outgoing team will run to enable the successor team to operate the tooling unaided:

| Session | Duration | Content | Who delivers | When |
|---|---|---|---|---|
| AI workflow orientation | 1 hour | Overview of all AI-augmented workflow components | Outgoing tech lead | Week -4 |
| Knowledge base walkthrough | 2 hours | Guided tour of `baseline/` and how to maintain it | Outgoing senior engineer | Week -4 |
| Hands-on AI workflow practice | 2 hours | Successor team runs the workflow on a real PR and incident | Facilitated by outgoing team | Week -2 |

---

### Part 5 — Package index

Produce a single-page index of every artifact in the transition package:

```
TRANSITION PACKAGE — {{PROJECT_NAME}}
Prepared by: {{OUTGOING_LEAD}}
Handover date: {{HANDOVER_DATE}}

KNOWLEDGE BASE
  baseline/00-summary.md                  — System overview and baseline narrative
  baseline/01-architecture-map.md         — Module inventory and dependency graph
  baseline/02-hotspot-analysis.md         — High-churn and high-risk file analysis
  baseline/03-adr-archaeology/            — Architecture Decision Records
  baseline/04-tech-debt-inventory.md      — Debt inventory and remediation priorities
  baseline/05-domain-glossary.md          — Domain vocabulary
  baseline/06-onboarding-paths/           — Role-specific onboarding guides
  baseline/07-comprehension-checks/       — Verification exercises by subsystem
  baseline/08-knowledge-capture-kit/      — Interview guides and walkthrough scripts

OPERATIONS
  {{RUNBOOK_PATHS}}                        — Operational runbooks
  postmortems/                             — Incident history and learning

HANDOVER ARTIFACTS
  handover/00-currency-audit.md           — Knowledge base currency audit
  handover/01-transition-package-index.md — This document
  handover/02-exit-criteria.md            — Measurable handover exit criteria
  handover/03-successor-onboarding-pack.md — Successor team onboarding
  handover/04-gap-register.md             — Open gaps and accepted risks
  handover/05-sign-off-checklist.md       — Final sign-off checklist
```

---

## Output format

Save to `handover/01-transition-package-index.md`.

All artifacts listed in the index must exist before the transition package is considered complete. Missing artifacts are **handover blockers** unless formally accepted as known risks in `handover/04-gap-register.md`.
