# Prompt: Hotspot Analysis

Analyse the version control history for `{{PROJECT_NAME}}` at `{{REPO_ROOT}}` to identify risk concentration.

## Parameters

- Timeframe: `{{TIMEFRAME}}` (e.g. `--since="18 months ago"`)
- Minimum change threshold for inclusion: 5 commits

## Instructions

Use `git log` to analyse commit history. Focus on identifying where risk is concentrated — not just what changed most, but what changed most *and* correlates with defects, bugs, or reverts.

### 1. High-churn file table

Run: `git log {{TIMEFRAME}} --name-only --pretty=format: | sort | uniq -c | sort -rn | head -30`

Produce a table of the top 20 most frequently changed files:

| Rank | File path | Change count | Module | Notes |
|---|---|---|---|---|
| 1 | … | … | … | … |

Exclude: lockfiles (`package-lock.json`, `composer.lock`, etc.), generated files, and migration files — note their exclusion.

### 2. Defect-correlated files

Find commits whose messages contain fix, bug, hotfix, revert, broken, incident (case-insensitive). Identify which files appear most often in those commits.

| File path | Defect-commit count | Total commit count | Defect ratio | Risk signal |
|---|---|---|---|---|
| … | … | … | …% | High/Med/Low |

### 3. Low bus-factor modules

For each module in the architecture map, identify how many distinct authors have committed to it in the timeframe:

| Module | Path | Distinct authors | Primary author commit % | Bus factor risk |
|---|---|---|---|---|
| … | … | … | …% | High/Med/Low |

Flag any module where a single author accounts for > 60% of commits — this is a knowledge concentration risk.

### 4. Churn-without-tests pattern

Identify files that changed frequently but whose corresponding test files did not change (or have no test files). These are areas where changes are being made without verification.

| File path | Code changes | Test file | Test changes | Risk |
|---|---|---|---|---|
| … | … | exists/none | … | … |

### 5. Narrative analysis

Write 2–3 paragraphs interpreting the hotspot pattern:
- What does the change concentration tell you about the architecture? (Is churn localised to a few modules, or spread evenly?)
- Which subsystems have the highest combined churn + defect + low-bus-factor risk?
- What should the incoming team prioritise learning about earliest?

### 6. Recommended early-attention areas

A ranked list of the 5 areas the incoming team should understand deeply before making unsupervised changes:

| Priority | Subsystem / file | Reason | Suggested first step |
|---|---|---|---|
| 1 | … | … | … |

---

## Output format

Markdown. Save to `baseline/02-hotspot-analysis.md`.

## Quality reminder

This analysis is based on commit metadata, not code semantics — it identifies *where* risk is concentrated, not *why*. The "why" comes from ADR archaeology and incumbent interviews.
