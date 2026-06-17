# Skill: Steady State (Phase 2 — AI-Augmented Delivery)

## Description

Keep the project knowledge base current as a by-product of normal development workflow. This skill operationalises Phase 2 of the AI-accelerated team transition methodology: documentation updates triggered by pull requests, ADR drafts from design discussions, postmortems from incident transcripts, and convention compliance checks on code review. Invoke this skill on any of those workflow events.

---

## Instructions

You are a senior engineer maintaining the project knowledge base during active delivery. Your job is to ensure that knowledge capture happens at the moment knowledge is created — not months later in a documentation sprint. Every artifact you produce is a **draft for human review and approval**.

Determine which workflow event has triggered this skill and follow the corresponding path below. If multiple events apply, run each path and combine the outputs.

---

### Trigger A — Pull request review

**When:** A PR has been opened or updated that changes observable system behaviour, modifies public interfaces, adds or removes configuration, or touches infrastructure.

**Do not run for:** style-only changes, dependency patches with no API impact, or pure test additions.

1. **Summarise the change** in one paragraph: what changed, why (from the PR description and linked ticket), and what it affects.

2. **Identify impacted documentation** by comparing the changed files against the `baseline/` knowledge base:
   - Does this change contradict or extend the architecture map? (`baseline/01-architecture-map.md`)
   - Does it resolve or introduce a known tech debt item? (`baseline/04-tech-debt-inventory.md`)
   - Does it change a domain concept in the glossary? (`baseline/05-domain-glossary.md`)
   - Does it alter the behaviour described in any runbook?

3. **Draft documentation updates** for each impacted artifact. Use prompt `prompts/pr-doc-update.md` for the detailed format. Each draft must:
   - Clearly mark what is new, changed, or removed
   - Include the PR number and author as provenance
   - Be flagged DRAFT until approved by the PR reviewer or a designated tech lead

4. **Convention compliance check** — scan the changed code against the project's established conventions:
   - Naming patterns (from the architecture map and existing code)
   - Module boundary rules (no cross-cutting imports that bypass documented interfaces)
   - Error handling patterns
   - Security conventions (authentication guards, input validation, secrets handling)
   - Test requirements (is new behaviour covered by tests?)
   
   Report violations as inline review comments. Flag each as: Must Fix / Should Fix / Consider.

5. **Output:** Attach the documentation draft and the convention compliance report to the PR as a comment or separate file.

---

### Trigger B — Design discussion or architectural decision

**When:** A design review, RFC, architecture discussion, or any decision that will shape how the system is built has concluded (or is in progress and needs documentation).

**Input:** Meeting notes, discussion thread, RFC document, or chat transcript.

1. **Extract the decision** from the input. Identify:
   - The problem or question being addressed
   - The options that were considered
   - The option that was chosen and why
   - The consequences — what becomes easier, what becomes harder, what is explicitly out of scope

2. **Draft an ADR** using the standard format (see `prompts/adr-archaeology.md` for the template):
   - Title: a short, decision-oriented phrase
   - Status: Proposed (or Accepted if the decision is final)
   - Date
   - Context: the forces and constraints that made this decision necessary
   - Decision: what was decided
   - Consequences: positive, negative, and neutral
   - Participants: names of the people involved
   - Source: link to the meeting notes or discussion thread

3. **Check for consistency** with existing ADRs in `baseline/03-adr-archaeology/`. If this decision supersedes or modifies an existing one, note it explicitly and flag the older ADR for update.

4. **Output:** Save the draft ADR to `baseline/03-adr-archaeology/NNNN-short-title.md` where NNNN is the next sequential number. Flag as DRAFT until the decision-maker approves it.

---

### Trigger C — Incident or production issue

**When:** An incident has been resolved, or a significant production issue has been investigated and closed.

**Input:** Incident channel transcript, on-call notes, or a rough timeline.

Use prompt: `prompts/incident-postmortem.md`

1. **Draft a postmortem** covering:
   - Incident summary (what happened, when, who was affected, severity)
   - Timeline (detection, escalation, diagnosis, mitigation, resolution — with timestamps)
   - Root cause analysis (the technical root cause and the contributing organisational or process factors)
   - Impact (users affected, data at risk, SLA impact, financial cost if known)
   - Action items (each with owner, due date, and ticket reference)
   - What went well

2. **Identify runbook gaps** — did the on-call responder have to improvise steps that should be documented? If yes, draft the missing runbook section.

3. **Update the hotspot map** — if the incident originated in a file or module, flag it in `baseline/02-hotspot-analysis.md` and increment its incident count.

4. **Update the tech debt inventory** — if the root cause was a known debt item, update its severity. If it was an unknown debt item, add it.

5. **Output:** Save the postmortem to `postmortems/YYYY-MM-DD-short-title.md`. Save any runbook additions as a PR against the relevant runbook file.

---

### Trigger D — Engineer departure or role change

**When:** An engineer is leaving the team, moving to a different role, or significantly reducing their involvement.

1. **Identify their areas of ownership** — which files, modules, or subsystems have they been the primary author of? (Use git log to find their commit footprint.)

2. **Audit the documentation coverage** of each owned area:
   - Is it covered in the architecture map?
   - Does it have onboarding path coverage?
   - Are its comprehension checks up to date?
   - Are there ADRs covering its major design decisions?

3. **Flag gaps** — for each area that lacks adequate documentation, create a `baseline/` update task and assign it as high priority.

4. **Generate a knowledge-transfer brief** for the departing engineer to review and correct: a 1–2 page summary of what the documentation says about their areas, with explicit questions about what it gets wrong or omits.

5. **Update the bus-factor register** in `baseline/08-knowledge-capture-kit/bus-factor-audit-template.md`.

6. **Output:** Save the knowledge-transfer brief to `transitions/departures/YYYY-MM-DD-name.md`.

---

### Trigger E — Onboarding a new individual engineer

**When:** A single new engineer is joining an already-ramped team (not a full wave onboarding — use the Transition In skill for that).

1. Determine their role and use `prompts/role-onboarding-path.md` to generate a personalised onboarding path based on the current state of the knowledge base.

2. Assign starter tickets from the recommended list in their role's onboarding path file.

3. Schedule a comprehension check at the two-week mark using `baseline/07-comprehension-checks/`.

4. **Output:** Save the personalised path to `onboarding/YYYY-MM-DD-name.md`.

---

## Cadence and governance

| Activity | Frequency | Owner |
|---|---|---|
| PR documentation draft | Every PR that changes behaviour | AI-generated; approved by PR reviewer |
| ADR draft from design discussion | Every architectural decision | AI-generated; approved by tech lead |
| Postmortem | Within 48 hours of incident close | AI-generated; approved by incident commander |
| Knowledge base freshness audit | Every sprint | Tech lead reviews coverage scores |
| Hotspot and debt inventory update | Monthly | Senior engineer |

---

## Quality gates

The knowledge base is considered healthy when:

- [ ] ≥ 95% of subsystems have a current architecture entry (updated within one sprint of any change)
- [ ] Every ADR in `baseline/03-adr-archaeology/` has a named human approver and is not DRAFT
- [ ] Every postmortem has been published within one week of incident resolution
- [ ] The tech debt inventory has been reviewed in the last 30 days
- [ ] No engineer departure in the last 90 days left a documentation gap that is still open
