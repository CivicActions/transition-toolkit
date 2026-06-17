# Prompt: Incident Postmortem

Draft a postmortem for a production incident affecting `{{PROJECT_NAME}}`.

## Incident context

- Incident ID / name: `{{INCIDENT_ID}}`
- Date and time of detection: `{{DETECTED_AT}}`
- Date and time of resolution: `{{RESOLVED_AT}}`
- Severity: `{{SEVERITY}}` (P1/P2/P3 or Critical/High/Medium)
- Incident commander: `{{INCIDENT_COMMANDER}}`
- Responders: `{{RESPONDERS}}`

## Input materials

Paste one or more of the following:
- Incident channel transcript: `{{TRANSCRIPT}}`
- On-call notes or timeline: `{{TIMELINE_NOTES}}`
- Monitoring alert details: `{{ALERT_DETAILS}}`
- Any existing rough notes: `{{ROUGH_NOTES}}`

---

## Instructions

Produce a structured postmortem draft. Every section is required. Where the input materials don't provide enough information, insert `[NEEDS INPUT: <question>]` so the incident commander knows exactly what to add.

---

### 1. Incident summary

Write 2–3 sentences covering: what happened, when, who was affected, and what the business impact was. This section should be readable by a non-technical stakeholder.

---

### 2. Timeline

Produce a chronological timeline from first signal to full resolution. Use the input materials to reconstruct it. Each entry:

| Time (UTC) | Event | Who |
|---|---|---|
| HH:MM | Alert fired / user report received | Monitoring system |
| HH:MM | On-call engineer paged | PagerDuty / {{ALERTING_TOOL}} |
| HH:MM | … | … |
| HH:MM | Root cause identified | {{PERSON}} |
| HH:MM | Mitigation applied | {{PERSON}} |
| HH:MM | Service restored | {{PERSON}} |
| HH:MM | All clear declared | {{INCIDENT_COMMANDER}} |

Note any gaps in the timeline that need to be filled in by the responders.

---

### 3. Root cause analysis

**Immediate cause:** The specific technical failure that directly caused the incident (e.g., "a database query missing an index caused response times to exceed the timeout threshold").

**Contributing factors:** The conditions that allowed the immediate cause to have impact:
- Was this a known risk that wasn't mitigated?
- Was there a missing test, alert, or runbook step?
- Was there a recent deployment or configuration change that introduced or exposed the issue?
- Were there process or communication factors that delayed detection or response?

**Five Whys** (trace the root cause back to its origin):
1. Why did the incident occur? → …
2. Why did that happen? → …
3. Why did that happen? → …
4. Why did that happen? → …
5. Why did that happen? → …

---

### 4. Impact

| Dimension | Detail |
|---|---|
| Users affected | `{{COUNT_OR_ESTIMATE}}` |
| Duration of impact | `{{DURATION}}` |
| Data integrity | No impact / {{DESCRIBE_IMPACT}} |
| SLA breach | Yes / No — `{{DETAIL}}` |
| Financial impact | `{{ESTIMATE_IF_KNOWN}}` |
| Reputational impact | `{{DESCRIBE_IF_ANY}}` |

---

### 5. What went well

List 3–5 things that worked as intended during the incident response. This is not a blame-avoidance exercise — it captures what should be preserved and reinforced.

---

### 6. Action items

Each action item must have an owner and a due date before the postmortem is published.

| # | Action | Owner | Due date | Ticket | Status |
|---|---|---|---|---|---|
| 1 | `{{ACTION}}` | `{{OWNER}}` | `{{DATE}}` | `{{TICKET}}` | Open |

Classify each action:
- **Prevent** — stops this specific failure from recurring
- **Detect** — improves detection speed or accuracy
- **Respond** — improves response time or effectiveness
- **Document** — fills a runbook or knowledge gap exposed by this incident

---

### 7. Runbook updates required

Based on the incident, identify any runbook gaps:

| Gap | Current state | Required update | Owner |
|---|---|---|---|
| `{{PROCEDURE}}` | Missing / Incomplete / Incorrect | `{{WHAT_TO_ADD_OR_FIX}}` | `{{OWNER}}` |

If no runbook gaps were identified: "No runbook updates required."

---

### 8. Knowledge base updates

- **Hotspot map update:** If the incident originated in a specific file or module, note it for `baseline/02-hotspot-analysis.md` (increment incident count for that file).
- **Tech debt update:** If the root cause was a known debt item, update its severity in `baseline/04-tech-debt-inventory.md`. If it was unknown, add it.

---

## Output format

Markdown. Save to `postmortems/{{YYYY-MM-DD}}-{{incident-slug}}.md`.

The draft must be reviewed and approved by the incident commander before publication. Mark the document **DRAFT** until approved. The goal is to publish within 48 hours of incident resolution.

**Blameless principle:** This postmortem is about systems and processes, not individual performance. Remove any language that assigns personal blame.
