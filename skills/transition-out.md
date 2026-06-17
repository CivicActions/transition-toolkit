# Skill: Transition Out (Phase 3 — AI-Enabled Handover)

## Description

Assemble the complete transition package for a successor team and manage the outbound handover. This skill operationalises Phase 3 of the AI-accelerated team transition methodology: packaging the living knowledge base, generating the risk and hotspot map, defining objectively measurable exit criteria, producing the successor team's onboarding pack, and preparing the tooling transfer guide.

Because Phase 2 ran continuously, this skill is a **verification and packaging exercise** — not a documentation sprint. Most artifacts already exist; this skill validates their currency, fills gaps, and wraps everything for handover.

---

## Instructions

You are a senior technical lead managing the outbound transition of a software project. Your goal is to ensure the successor team inherits a project that explains itself, with a verified knowledge base, measurable exit criteria, and all tooling transferred intact.

Work through the following steps in order. For each gap you find, generate a remediation task and flag it as blocking the handover.

---

### Step 1 — Knowledge base currency audit

Before packaging anything, audit the existing `baseline/` knowledge base for staleness.

For each artifact in `baseline/`:

1. Check the last-modified date against the git log for the files it covers.
2. Flag any artifact where the codebase has changed significantly since it was last updated.
3. For each flagged artifact, either:
   - Update it using the appropriate Phase 2 trigger (re-run the relevant steady-state step), or
   - Mark it as a known gap in the gap register with a severity rating

Produce a **currency audit table**:

| Artifact | Last updated | Last relevant code change | Status | Action required |
|---|---|---|---|---|
| `01-architecture-map.md` | … | … | Current / Stale / Gap | … |
| … | | | | |

Save to `handover/00-currency-audit.md`.

**Handover blocker:** Any Critical or High severity gap must be resolved before the transition package is delivered.

---

### Step 2 — Transition package assembly

Use prompt: `prompts/transition-package.md`

Compile the full transition package from the validated `baseline/` artifacts:

1. **Knowledge base** — confirm each of the following is current and validated:
   - `baseline/01-architecture-map.md`
   - `baseline/03-adr-archaeology/` (all ADRs)
   - Runbooks (wherever they live in the project)
   - `baseline/05-domain-glossary.md`
   - `baseline/06-onboarding-paths/` (all role paths)

2. **Risk and hotspot map** — generate a current version from:
   - `baseline/02-hotspot-analysis.md` (re-run `prompts/hotspot-analysis.md` against recent git history if more than 4 weeks old)
   - `baseline/04-tech-debt-inventory.md`
   - Postmortem history in `postmortems/`
   
   Produce a single, ranked table of subsystems by risk level with a brief rationale for each rating.

3. **Operational runbooks** — list every operational procedure that exists and every one that is missing. Missing runbooks for Critical or High risk subsystems are handover blockers.

4. **AI assistant configuration** — document how the project AI assistant is configured, what corpus it uses, and the steps to transfer it to the successor team's environment.

5. **Tooling and workflow guide** — document the AI-augmented workflow configuration: which tools are in use, how they are wired into CI/CD and code review, and how the successor team can operate them independently.

Save the package index to `handover/01-transition-package-index.md`.

---

### Step 3 — Exit criteria definition

Use prompt: `prompts/exit-criteria.md`

Define objectively measurable exit criteria for the handover. These become the contractual or agreed milestones that determine when the transition is complete.

Produce a table with the following criteria (adjust thresholds to match the project's pre-transition baseline):

| Criterion | Measurement method | Target threshold | Owner | Status |
|---|---|---|---|---|
| Comprehension-check pass rate | AI-generated checks; human assessor scores | ≥ 90% per subsystem | Outgoing tech lead | Not started |
| Change failure rate | CI/CD deployment records; incident log | ≤ pre-transition baseline | Successor tech lead | Not started |
| Incident response executed end-to-end | Successor team handles a real or simulated incident without assistance | ≥ 1 per critical subsystem | Successor on-call lead | Not started |
| Knowledge base coverage | Currency audit (Step 1) | ≥ 95% subsystems current | Outgoing tech lead | Not started |
| Tooling operated unaided | Successor team runs AI workflow without outgoing team support for ≥ 1 sprint | Pass/fail | Successor tech lead | Not started |
| First independent feature delivered | End-to-end delivery without outgoing team involvement | 1 feature in production | Successor tech lead | Not started |

Save to `handover/02-exit-criteria.md`.

---

### Step 4 — Successor team onboarding pack

The successor team onboards through the same Phase 1 machinery as the original team. Prepare their onboarding pack now, using the current knowledge base.

1. **Generate role-specific onboarding paths** for the successor team's expected roles using `prompts/role-onboarding-path.md`. Update the paths in `baseline/06-onboarding-paths/` to reflect the current state of the codebase.

2. **Select starter tickets** — identify 3–5 well-bounded, representative tickets per role that serve as guided tours with a deliverable. Prefer tickets in subsystems that appear in the hotspot map so the successor team gains early familiarity with the riskiest areas.

3. **Prepare comprehension checks** for the overlap period — update `baseline/07-comprehension-checks/` to reflect any subsystems that have changed since Phase 1.

4. **Prepare the knowledge-capture kit** for reverse use: the outgoing team's remaining experts should complete the interview guide and walkthrough script in `baseline/08-knowledge-capture-kit/` before their last day.

5. **Schedule overlap activities:**
   - Week 1–2: Successor team setup; outgoing team delivers knowledge-capture sessions
   - Week 3–4: Successor team makes first production changes under outgoing team review
   - Week 5–6: Outgoing team reviews successor team's comprehension check results; targeted remediation
   - Week 7–8: Successor team operates independently; outgoing team is available for questions only
   - Week 9–10: Exit criteria verified; formal handover signed off

Save to `handover/03-successor-onboarding-pack.md`.

---

### Step 5 — Gap register and risk acceptance

Compile every gap identified in Steps 1–4 into a single register:

| Gap | Severity | Subsystem | Description | Remediation | Owner | Due | Status |
|---|---|---|---|---|---|---|---|
| … | Critical / High / Medium / Low | … | … | … | … | … | Open / Closed |

For each open gap:
- If it can be closed before handover, assign it.
- If it cannot be closed, it must be formally accepted as a known risk by both the outgoing and successor team leads, with a mitigation plan.

**Handover blocker:** All Critical gaps must be closed. All High gaps must be either closed or formally accepted with a mitigation plan.

Save to `handover/04-gap-register.md`.

---

### Step 6 — Handover sign-off checklist

Produce the final sign-off checklist. The transition is complete when every item is checked.

```
TRANSITION OUT — SIGN-OFF CHECKLIST
Project: {{PROJECT_NAME}}
Handover date: {{DATE}}
Outgoing team lead: {{OUTGOING_LEAD}}
Successor team lead: {{SUCCESSOR_LEAD}}

KNOWLEDGE BASE
[ ] Currency audit complete — all Critical/High gaps resolved or formally accepted
[ ] Architecture map reviewed and signed off by outgoing tech lead
[ ] All ADRs have named human approvers (no unreviewed DRAFTs)
[ ] Runbooks complete and tested for all Critical/High risk subsystems
[ ] Domain glossary current
[ ] Role-specific onboarding paths updated for current codebase
[ ] Comprehension checks updated

OPERATIONS
[ ] Risk and hotspot map current (git analysis run within last 2 weeks)
[ ] Tech debt inventory reviewed; Critical items have remediation tickets
[ ] All postmortems published

SUCCESSOR TEAM READINESS
[ ] Comprehension check pass rate ≥ 90% for each subsystem
[ ] Successor team has made at least one production change in each Critical subsystem
[ ] Incident response drill completed for at least one Critical subsystem
[ ] Successor team has operated AI workflow unaided for ≥ 1 sprint

TOOLING TRANSFER
[ ] AI assistant configuration documented and transferred
[ ] AI-augmented workflow running in successor team's environment
[ ] Access and credentials rotated; outgoing team access revoked

FORMAL SIGN-OFF
[ ] All Critical and High gaps closed or formally risk-accepted
[ ] Exit criteria in handover/02-exit-criteria.md: all rows marked Pass
[ ] Both team leads have signed below

Signed: _________________________ (Outgoing lead)   Date: _________
Signed: _________________________ (Successor lead)  Date: _________
```

Save to `handover/05-sign-off-checklist.md`.

---

## Output structure

```
handover/
  00-currency-audit.md
  01-transition-package-index.md
  02-exit-criteria.md
  03-successor-onboarding-pack.md
  04-gap-register.md
  05-sign-off-checklist.md
```

---

## Timeline guidance

| Week | Activity |
|---|---|
| -8 to -6 | Currency audit; close gaps; update knowledge base |
| -6 to -4 | Assemble transition package; define exit criteria; prepare successor onboarding pack |
| -4 to -2 | Successor team onboards (Phase 1 machinery); knowledge-capture sessions with outgoing experts |
| -2 to 0 | Successor team makes first production changes; comprehension checks; gap remediation |
| 0 | Exit criteria verification; formal sign-off |
