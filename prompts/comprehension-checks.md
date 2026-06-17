# Prompt: Comprehension Checks

Generate scenario-based comprehension checks for the **`{{SUBSYSTEM}}`** subsystem of `{{PROJECT_NAME}}`.

## Context

- Codebase: `{{REPO_ROOT}}`
- Subsystem: `{{SUBSYSTEM}}`
- Key files: `{{KEY_FILES}}` (list the most important files in this subsystem)
- Audience: incoming engineers who have completed the guided onboarding tour but have not yet worked independently on this subsystem

Reference `baseline/01-architecture-map.md` and `baseline/02-hotspot-analysis.md` if available.

---

## Instructions

Produce a set of comprehension checks that allow an assessor to verify an engineer's understanding of `{{SUBSYSTEM}}` before they are given unsupervised ownership. Checks must test genuine understanding — not just the ability to look something up.

**Scoring guidance for assessors:** Each check has a reference answer. Award full credit for answers that demonstrate understanding of the *why*, not just the *what*.

---

### Check 1 — Orientation question

A straightforward question that the engineer should be able to answer from the onboarding tour.

**Question:** `[Write a specific question about the purpose, location, or basic behaviour of {{SUBSYSTEM}}]`

**What a confident answer looks like:**
- Mentions the relevant file(s) or module(s)
- Correctly describes what the subsystem does and for whom
- Identifies at least one dependency or integration point

**Reference answer:**
`[Complete the reference answer based on the codebase]`

---

### Check 2 — "Where would you look?" scenario

A realistic support or debugging scenario rooted in this subsystem.

**Scenario:** "A user reports that `[describe a realistic symptom caused by a problem in {{SUBSYSTEM}}]`. Where would you start investigating, and what would you look for?"

**What a confident answer looks like:**
- Identifies the correct entry point or log location
- Describes the debugging process in the right order
- Mentions at least one non-obvious place to look (from the hotspot map or known gotchas)

**Reference answer:**
`[Complete based on the codebase's actual debugging path]`

---

### Check 3 — "What would break if…" exercise

Tests understanding of the subsystem's dependencies and failure modes.

**Question:** "What would happen if `[name a key component, function, or configuration value in {{SUBSYSTEM}}]` were removed / set to zero / made unavailable? Walk through the failure cascade."

**What a confident answer looks like:**
- Correctly identifies the immediate failure
- Identifies downstream systems or users that would be affected
- Mentions how to detect the failure (logging, monitoring, user reports)

**Reference answer:**
`[Complete based on the codebase's actual dependency graph]`

---

### Check 4 — "Make a change" walkthrough

Tests that the engineer knows the safe path for modifying this subsystem.

**Question:** "You need to `[describe a small, realistic change to {{SUBSYSTEM}}]`. Walk me through every step from understanding the requirement to having the change merged and confirmed in production."

**What a confident answer looks like:**
- Identifies the correct files to change
- Mentions the relevant tests to run or write
- Describes how to verify the change in a non-production environment
- Mentions any specific conventions, review requirements, or deployment steps specific to this subsystem

**Reference answer:**
`[Complete based on the project's actual workflow and conventions]`

---

### Check 5 — Architecture and decision understanding

Tests awareness of why the subsystem is the way it is.

**Question:** "Why is `[name a non-obvious structural choice in {{SUBSYSTEM}}]` implemented this way rather than `[describe the obvious alternative]`?"

**What a confident answer looks like:**
- Recalls or reasons through the rationale (from ADRs, onboarding materials, or the code itself)
- Correctly identifies the trade-off that was made
- Does not confuse current design with ideal design

**Reference answer:**
`[Complete from the relevant ADR in baseline/03-adr-archaeology/ or from code comments]`

---

### Assessment rubric

| Score | Meaning |
|---|---|
| 5/5 | Ready for unsupervised ownership of this subsystem |
| 4/5 | Minor gaps; can take ownership with light oversight for 1–2 weeks |
| 3/5 | Meaningful gaps; needs targeted study and another check in 1 week |
| ≤2/5 | Not ready; schedule a pair-programming session and re-assess |

**Minimum to pass:** 4/5 checks answered at "confident" level before unsupervised ownership is granted.

---

## Output format

Markdown. Save to `baseline/07-comprehension-checks/{{subsystem-slug}}.md`.

Write the public-facing questions and scenarios in the document. Put reference answers in a separate section clearly marked **[ASSESSOR ONLY — do not share with the engineer being checked]**.
