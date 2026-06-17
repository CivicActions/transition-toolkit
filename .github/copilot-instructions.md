# Copilot Instructions — AI Team Transition Toolkit

This repository is a **reusable AI-accelerated team transition toolkit**. It contains skills and prompt templates that operationalise the three-phase transition methodology described in `transition.txt`.

## Repository layout

| Path | Purpose |
|---|---|
| `skills/` | Copilot skill definitions — invoke with the `skill` tool |
| `prompts/` | Atomic, parameterised prompt templates for individual transition activities |
| `transition.txt` | Source white paper (the full methodology rationale) |
| `d8-lincs.ed.gov/` | Example project — used to validate and illustrate the toolkit only |

## Three-phase model

| Phase | Skill | When to use |
|---|---|---|
| Phase 1 — Transition In | `skills/transition-in.md` | First 1–10 weeks; incoming team onboarding |
| Phase 2 — Steady State | `skills/steady-state.md` | Throughout delivery; keep knowledge base current |
| Phase 3 — Transition Out | `skills/transition-out.md` | Final 6–10 weeks; successor team handover |

## How to use the skills

Point Copilot at a target project codebase and invoke the relevant skill:

```
Run the transition-in skill against this codebase.
```

Each skill orchestrates a sequence of atomic prompts from `prompts/`. You can also run individual prompts directly by referencing them.

## Adapting to a project

Every prompt template uses `{{DOUBLE_BRACE}}` placeholders. Before invoking, supply:

- `{{PROJECT_NAME}}` — the project or product name
- `{{REPO_ROOT}}` — path to the codebase being analysed
- `{{TECH_STACK}}` — primary languages, frameworks, and infrastructure
- `{{ROLE}}` — the engineer role receiving an onboarding path (Phase 1 only)
- `{{SUBSYSTEM}}` — a specific module or service (where scope-limited prompts apply)

## Output conventions

- All generated artifacts are **drafts for human review** — never treat AI output as ground truth.
- Every claim in generated documentation should cite the source file, commit, or ticket it came from.
- Artifacts are saved as Markdown by default; use the `prompts/` templates to adjust format.
- Human approver names must be recorded on every published document and architectural decision.

## Security and IP

- Do not send client code or data to external services without confirming zero-retention enterprise agreements are in place.
- All generated knowledge-base artifacts belong to the client; deliver in open, portable formats.
- AI-assisted review supplements human review — never replaces it.
