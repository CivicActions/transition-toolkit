# AI Team Transition Toolkit

A reusable collection of AI skills and prompt templates for de-risking large-team onboarding and handover on established software projects. Based on the three-phase methodology described in [`transition.txt`](transition.txt).

## Quick start

Point Copilot at a target codebase and invoke a phase skill:

```
# Bring a new team onto a project
Run the transition-in skill against this codebase.

# Keep documentation current during delivery
Run the steady-state skill for this pull request / incident / design decision.

# Hand over to a successor team
Run the transition-out skill and produce the handover package.
```

Or run individual prompt templates from `prompts/` for specific activities.

---

## The three-phase model

### Phase 1 — Transition In (`skills/transition-in.md`)

Weeks 1–10. Before the full team arrives, a small advance group uses AI to build a **codebase intelligence baseline** so every incoming engineer has an AI assistant that has effectively already read the whole project.

Produces:
- Architecture map (module summaries, dependency graph)
- Change hotspot analysis (high-churn / high-risk files from git history)
- ADR archaeology (decisions mined from commits, PRs, and tickets)
- Technical debt inventory (deps, dead code, coverage gaps, undocumented config)
- Domain glossary
- Role-specific onboarding paths
- Starter-ticket recommendations
- Comprehension checks (scenario questions, "what would break if…" exercises)
- Incumbent knowledge-capture kit (interview guides, walkthrough prompts)

### Phase 2 — Steady State (`skills/steady-state.md`)

Throughout delivery. Knowledge maintenance is a **by-product of normal work**, not a separate chore.

Produces (triggered by normal workflow events):
- PR description → documentation diff draft
- Design discussion notes → ADR draft
- Incident channel transcript → postmortem + runbook update draft
- Code review → convention compliance check

### Phase 3 — Transition Out (`skills/transition-out.md`)

Final 6–10 weeks. Because Phase 2 ran continuously, the outbound handover is a **verification exercise**, not a reconstruction project.

Produces:
- Living transition package (knowledge base, ADRs, runbooks, glossary, onboarding paths — all current)
- Quantified risk and hotspot map
- Objectively measurable exit criteria
- Successor team onboarding pack (mirrors Phase 1)
- Tooling transfer guide

---

## Repository layout

```
.github/
  copilot-instructions.md   # Toolkit-level Copilot context
skills/
  transition-in.md          # Phase 1 skill
  steady-state.md           # Phase 2 skill
  transition-out.md         # Phase 3 skill
prompts/
  architecture-map.md       # Module-by-module architecture summary
  hotspot-analysis.md       # High-churn / high-risk file analysis
  adr-archaeology.md        # Mine decisions from git/PR/ticket history
  tech-debt-inventory.md    # Dependency audit, dead code, coverage gaps
  role-onboarding-path.md   # Role-specific guided tour of the codebase
  comprehension-checks.md   # Scenario questions and verification exercises
  pr-doc-update.md          # Draft documentation changes from a PR
  incident-postmortem.md    # Draft postmortem from incident transcript
  transition-package.md     # Assemble the full outbound handover package
  exit-criteria.md          # Define measurable handover exit criteria
transition.txt              # Source white paper
d8-lincs.ed.gov/            # Example project (illustration only)
```

---

## Using prompt templates

Every prompt in `prompts/` uses `{{DOUBLE_BRACE}}` placeholders. Substitute before use:

| Placeholder | Meaning |
|---|---|
| `{{PROJECT_NAME}}` | Name of the project being analysed |
| `{{REPO_ROOT}}` | Path or URL to the codebase |
| `{{TECH_STACK}}` | Primary languages, frameworks, infrastructure |
| `{{ROLE}}` | Engineer role (e.g. backend, frontend, SRE, data) |
| `{{SUBSYSTEM}}` | A specific module or service |
| `{{TICKET_SYSTEM}}` | Jira, GitHub Issues, Linear, etc. |
| `{{TIMEFRAME}}` | Git log range (e.g. `--since="18 months ago"`) |

---

## Key principles

1. **AI output is always a draft.** Every generated artifact must be reviewed by a senior engineer and, where possible, validated by the incumbent team before it is published.
2. **Cite sources.** Every factual claim in generated documentation must link back to the file, commit, line, or ticket it came from.
3. **Measure comprehension, don't assume it.** Use the comprehension-check prompts to verify understanding objectively — gaps are visible in weeks, not discovered in production.
4. **Human accountability.** Every published document and architectural decision carries a named human approver.
5. **Portability.** All artifacts are delivered in open formats. There is no proprietary lock-in.

---

## Success metrics

| Metric | Target |
|---|---|
| Time to first merged change | < 5 working days per engineer |
| Time to independent delivery | 3–5 weeks |
| Comprehension-check pass rate | ≥ 90% before unsupervised ownership |
| Change failure rate | At or below pre-transition baseline |
| Knowledge base coverage | ≥ 95% of subsystems with current, validated docs |
| Expert interrupt rate | Declining week-over-week; near zero by week 10 |
