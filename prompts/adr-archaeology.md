# Prompt: ADR Archaeology

Mine architectural decisions from the version control and ticket history of `{{PROJECT_NAME}}` at `{{REPO_ROOT}}` and draft them as Architecture Decision Records (ADRs).

## Parameters

- Ticket system: `{{TICKET_SYSTEM}}` (GitHub Issues / Jira / Linear / none)
- Timeframe: `{{TIMEFRAME}}`
- Number of ADRs to target: 5–10 most impactful decisions

## Instructions

### Phase 1 — Decision signal mining

Search the following sources for evidence of significant architectural decisions:

**Git commit messages:**
```
git log {{TIMEFRAME}} --pretty=format:"%H %s" | grep -iE "refactor|migrate|replace|switch|adopt|introduce|remove|deprecate|breaking|architecture|design|decision|chose|approach"
```

**Pull request titles and bodies** (if accessible via `{{TICKET_SYSTEM}}`): look for RFCs, design docs, "why we chose" language, and ADR-tagged items.

**Code comments:** search for `TODO`, `FIXME`, `HACK`, `NOTE`, `WHY`, `because`, `workaround`, `legacy` in source files.

**Configuration and infrastructure files:** unusual configuration choices (non-default ports, custom middleware, non-standard directory layouts) are often the result of undocumented decisions.

### Phase 2 — Decision classification

For each signal found, classify it:

| Signal | Source | Decision type | Confidence that a deliberate decision was made |
|---|---|---|---|
| … | commit SHA / PR # / file:line | Technology choice / Architecture / Process / Security | High/Med/Low |

Exclude trivial decisions (minor refactors, typo fixes). Focus on:
- Technology or framework choices ("why are we using X instead of Y?")
- Structural decisions ("why is this module separate from that one?")
- Data model choices ("why is this denormalised?")
- Security or compliance constraints ("why do we handle X this way?")
- Known workarounds with a documented reason ("this is a hack because…")

### Phase 3 — ADR drafting

For each decision with Medium or High confidence, draft an ADR using this template:

---

```markdown
# ADR-NNNN: {{TITLE}}

**Status:** DRAFT — awaiting incumbent validation  
**Date:** {{DATE_OF_EARLIEST_EVIDENCE}}  
**Participants:** {{NAMES_IF_DETERMINABLE}} (inferred from git/PR history)

## Context

{{Describe the situation and forces that made this decision necessary. What problem was being solved? What constraints existed? What alternatives were available?}}

## Decision

{{State the decision that was made, as specifically as possible.}}

## Consequences

**Positive:**
- {{What becomes easier or better as a result?}}

**Negative:**
- {{What becomes harder or worse? What is the cost of this decision?}}

**Neutral / open:**
- {{What is left undecided or deferred?}}

## Source evidence

| Type | Reference | Excerpt |
|---|---|---|
| Commit | {{SHA}} | "{{commit message}}" |
| PR | {{URL or #number}} | "{{relevant quote}}" |
| Code comment | {{file:line}} | "{{comment text}}" |

## Validation needed

- [ ] Incumbent review: Is the reconstructed rationale accurate?
- [ ] Are there additional considerations not captured here?
- [ ] Is the status current (was this decision later reversed)?
```

---

### Phase 4 — Gap register

For decisions you found evidence of but could not reconstruct with enough confidence to draft an ADR, produce a gap register:

| Signal | Source | What is missing | Who might know |
|---|---|---|---|
| … | … | The rationale for… | Likely: the author of commit {{SHA}} |

---

## Output format

- One ADR per file: `baseline/03-adr-archaeology/NNNN-short-title.md`
- Gap register: `baseline/03-adr-archaeology/00-gap-register.md`
- ADR index: `baseline/03-adr-archaeology/README.md` listing all ADRs with one-line summaries

## Quality reminder

Every ADR is a **DRAFT** until validated by a person who was involved in the original decision. The goal of archaeology is to create a starting point that makes validation fast — not to assert history that may be wrong.
