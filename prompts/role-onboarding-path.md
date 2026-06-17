# Prompt: Role-Specific Onboarding Path

Generate a personalised onboarding path for a **`{{ROLE}}`** joining `{{PROJECT_NAME}}`.

## Context

- Codebase: `{{REPO_ROOT}}`
- Tech stack: `{{TECH_STACK}}`
- Role: `{{ROLE}}` (e.g. backend engineer, frontend engineer, DevOps/SRE, QA/test engineer, tech lead/architect)
- Team size and current sprint context (optional): `{{TEAM_CONTEXT}}`

Reference the existing `baseline/` knowledge base if it is available. If not, derive from the codebase directly.

---

## Instructions

Produce a structured onboarding guide that a `{{ROLE}}` can follow independently from their first day. The goal is to get them to their first merged change within 5 working days and to independent task ownership within 3–5 weeks.

---

### Section 1 — Start here (Day 1)

The 3–5 most important things to read or run before anything else. These should give the fastest orientation and allow the engineer to get a local development environment running.

For each item:
- What it is and why it matters for a `{{ROLE}}`
- Where to find it (file path, URL, or command)
- Approximate time to complete

---

### Section 2 — Guided codebase tour (Days 1–3)

A structured reading path through the codebase, ordered from most important to least. Tailored to what a `{{ROLE}}` actually needs to understand to do their job.

For each stop on the tour:
- The file(s) or directory to read
- What to look for and understand (not just "read this" — explain what question it answers)
- Any gotchas or non-obvious patterns the engineer should notice

---

### Section 3 — The three most common tasks for this role

Identify the 3 tasks that a `{{ROLE}}` will do most frequently on this project. For each:

**Task: {{TASK_NAME}}**
- What it involves
- Where in the codebase it happens (files, modules, commands)
- The standard process or workflow
- Common mistakes and how to avoid them
- How to test and verify the change

---

### Section 4 — Pitfalls and gotchas

Things that will trip up a `{{ROLE}}` if they don't know about them. Derived from:
- High-churn and high-defect areas in `baseline/02-hotspot-analysis.md`
- Known workarounds and "why does this exist" patterns
- Non-standard conventions that differ from what you'd expect for this tech stack

List 5–10 items, each with: what the pitfall is, why it exists (if known), and how to avoid or work around it.

---

### Section 5 — Starter ticket recommendations

Suggest 3–5 tickets (or ticket types, if specific tickets aren't available) that are ideal for a new `{{ROLE}}`. Good starter tickets are:
- Well-bounded: the scope is clear and limited
- Representative: they touch the area of the codebase this role will work in most
- Low-risk: a mistake is catchable in review and won't affect production adversely
- Educational: completing them teaches something important about the project

For each recommendation:
- Ticket or task description
- Why it's a good starter for this role
- Which part of the codebase it exercises
- Estimated complexity (XS / S / M)

---

### Section 6 — Two-week comprehension check

A list of questions the engineer should be able to answer confidently after two weeks. These are drawn from `baseline/07-comprehension-checks/` where available, or generated from the codebase.

Include:
- 3–5 factual questions ("Where is X configured? What does Y do?")
- 1–2 scenario questions ("A user reports Z — where would you look first?")
- 1 "explain it back" prompt ("Describe the data flow for the most common operation in your area")

---

### Section 7 — Who to ask about what

If the team has known subject matter experts (from git blame or the bus-factor audit), list them:

| Topic / subsystem | Go-to person | How to reach them |
|---|---|---|
| … | … | … |

If not known, leave as a placeholder for the team to fill in.

---

## Output format

Markdown. Save to `baseline/06-onboarding-paths/{{role-slug}}.md` (e.g. `backend-engineer.md`).

The guide should be written directly to the engineer — second person ("you"), active voice. Avoid jargon that isn't explained in the domain glossary.
