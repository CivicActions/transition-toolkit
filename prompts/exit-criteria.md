# Prompt: Exit Criteria

Define objectively measurable handover exit criteria for `{{PROJECT_NAME}}`.

## Context

- Project: `{{PROJECT_NAME}}`
- Outgoing team lead: `{{OUTGOING_LEAD}}`
- Successor team lead: `{{SUCCESSOR_LEAD}}`
- Pre-transition baseline metrics (if known):
  - Change failure rate: `{{BASELINE_CHANGE_FAILURE_RATE}}`
  - Mean time to recovery: `{{BASELINE_MTTR}}`
  - Deployment frequency: `{{BASELINE_DEPLOY_FREQ}}`

---

## Instructions

Produce a set of exit criteria that convert the handover from a calendar event into an engineering milestone. Each criterion must be:
- **Objectively measurable** — both teams can independently verify the result
- **Evidence-based** — pass/fail is determined by data, not gut feel
- **Agreed upfront** — both team leads sign off on the criteria before the transition overlap period begins

---

### Standard exit criteria

Adapt the thresholds to match the project's pre-transition baseline. Where no baseline exists, use the targets below as a starting point and document the assumption.

#### 1. Comprehension verification

| Criterion | Measurement method | Target | Evidence required |
|---|---|---|---|
| Comprehension-check pass rate per subsystem | AI-generated checks scored by outgoing senior engineer | ≥ 90% of checks passed (4/5 or 5/5) | Completed check sheets in `baseline/07-comprehension-checks/` with assessor signatures |
| No subsystem with zero coverage | All subsystems in the risk map have at least one assessed engineer | 100% | Check sheet index |

#### 2. Independent delivery

| Criterion | Measurement method | Target | Evidence required |
|---|---|---|---|
| First independent production change | A change shipped to production by the successor team without outgoing team involvement | ≥ 1 per Critical subsystem | PR merged and deployed by successor team member; outgoing team not a reviewer or approver |
| End-to-end feature delivery | A complete feature (spec → deploy → verify) owned by the successor team | ≥ 1 feature | PR history and deployment record |

#### 3. Operational readiness

| Criterion | Measurement method | Target | Evidence required |
|---|---|---|---|
| Incident response drill | Successor team responds to a real or simulated incident without assistance | ≥ 1 per Critical subsystem | Incident log or drill report showing successor team as sole responders |
| Change failure rate | Failed deployments / total deployments over the overlap period | ≤ pre-transition baseline (`{{BASELINE_CHANGE_FAILURE_RATE}}`) | CI/CD deployment records |
| Mean time to recovery | Time from incident detection to resolution for incidents during the overlap period | ≤ pre-transition baseline (`{{BASELINE_MTTR}}`) | Incident log with timestamps |

#### 4. Knowledge base

| Criterion | Measurement method | Target | Evidence required |
|---|---|---|---|
| Knowledge base coverage | Currency audit: % of subsystems with documentation updated within one sprint of last code change | ≥ 95% | `handover/00-currency-audit.md` |
| No unreviewed DRAFT ADRs | All ADRs in `baseline/03-adr-archaeology/` have a named human approver | 100% | ADR index with approver names |
| Runbook completeness | All Critical and High risk operational procedures have a tested runbook | 100% of Critical / ≥ 80% of High | Runbook completeness table in transition package |

#### 5. Tooling independence

| Criterion | Measurement method | Target | Evidence required |
|---|---|---|---|
| AI workflow operated unaided | Successor team has run the full AI-augmented workflow (PR doc draft, convention check, postmortem draft) without outgoing team support | ≥ 1 complete sprint | Sprint retrospective note from successor team lead |
| AI assistant transferred | Project AI assistant is running in the successor team's environment | Pass/fail | Successor team lead confirms in writing |

#### 6. Access and credential hygiene

| Criterion | Measurement method | Target | Evidence required |
|---|---|---|---|
| Outgoing team access revoked | All outgoing team members removed from production systems, CI/CD, and secret stores | 100% | Access audit from IAM / cloud console |
| Credentials rotated | All secrets that outgoing team members had access to have been rotated | 100% | Rotation log or ticket |

---

### Project-specific criteria

Add any project-specific criteria here. These might include:
- Compliance requirements (e.g., a specific security control must be demonstrated by the successor team)
- Contractual SLAs that must be met during the overlap period
- Regulatory milestones
- Client or stakeholder sign-off requirements

| Criterion | Measurement method | Target | Evidence required |
|---|---|---|---|
| `{{CUSTOM_CRITERION}}` | … | … | … |

---

### Sign-off process

Exit criteria are considered **met** when:

1. All evidence listed above has been collected and reviewed by both team leads.
2. Any criteria marked as exceptions (met with conditions) have been formally accepted by both team leads with a written rationale.
3. Both team leads sign the sign-off checklist in `handover/05-sign-off-checklist.md`.

**Dispute resolution:** If the two team leads disagree on whether a criterion is met, the evidence is reviewed by a neutral third party (e.g., the client technical lead or a programme manager) whose decision is final.

---

## Output format

Markdown. Save to `handover/02-exit-criteria.md`.

Add a status column to each table that will be updated as criteria are met:

| Status values | Meaning |
|---|---|
| Not started | Work hasn't begun |
| In progress | Evidence is being collected |
| Pass | Criterion met; evidence verified |
| Exception | Criterion not fully met; accepted with conditions |
| Fail | Criterion not met; handover blocked |
