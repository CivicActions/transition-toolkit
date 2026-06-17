# Prompt: PR Documentation Update

Draft documentation updates triggered by a pull request that changes observable behaviour in `{{PROJECT_NAME}}`.

## PR context

- PR number / URL: `{{PR_REF}}`
- Author: `{{PR_AUTHOR}}`
- Title: `{{PR_TITLE}}`
- Linked ticket: `{{TICKET_REF}}`
- Changed files: `{{CHANGED_FILES}}` (paste the diff stat or file list)

---

## Instructions

Review the PR diff and the project's existing `baseline/` documentation. Produce two outputs: (1) documentation update drafts and (2) a convention compliance report.

---

### Output 1 — Documentation update drafts

#### Step 1 — Classify the change

Determine which of the following the PR does (select all that apply):

- [ ] Adds or removes a user-facing capability
- [ ] Changes the interface of a module (function signatures, API endpoints, event schemas)
- [ ] Adds, removes, or modifies a configuration option or environment variable
- [ ] Changes how a module integrates with an external service
- [ ] Resolves a known tech debt item
- [ ] Introduces a new tech debt item or workaround
- [ ] Changes a domain concept or term
- [ ] Changes an operational procedure (deployment, recovery, rollback)

If none of the above apply (pure refactor, style change, test-only change with no behaviour change), output: "No documentation update required. Reason: `{{REASON}}`" and stop.

#### Step 2 — Draft updates for each impacted artifact

For each impacted artifact, produce a **diff-style draft** showing what should change:

---

**`baseline/01-architecture-map.md`** (if the PR changes module structure, dependencies, or system capabilities)

```diff
- [Current text that is now wrong or incomplete]
+ [Updated text reflecting the PR change]
```

Provenance: PR #{{PR_REF}} by {{PR_AUTHOR}} — {{DATE}}

---

**`baseline/04-tech-debt-inventory.md`** (if the PR resolves or introduces a debt item)

```diff
- [Remove or update the resolved item]
+ [Add or update with the new/modified item]
```

---

**`baseline/05-domain-glossary.md`** (if a domain term is introduced, changed, or removed)

```diff
- [Old term or definition]
+ [New term or definition]
```

---

**Runbook: `{{RUNBOOK_PATH}}`** (if the PR changes an operational procedure)

```diff
- [Old step or section]
+ [New step or section]
```

---

**Configuration documentation** (if an environment variable or config option changed)

| Variable | Change | Old behaviour | New behaviour | Required? | Default |
|---|---|---|---|---|---|
| `{{VAR_NAME}}` | Added/Changed/Removed | … | … | Yes/No | … |

---

### Output 2 — Convention compliance report

Check the PR diff against the project's established conventions. Report violations only — do not comment on style that isn't a documented convention.

Sources for conventions:
- `baseline/01-architecture-map.md` (module boundary rules, naming patterns)
- `.github/copilot-instructions.md`
- Any linting or style configuration in the repository

For each violation:

| Severity | File | Line | Convention | Violation | Recommended fix |
|---|---|---|---|---|---|
| Must Fix | … | … | … | … | … |
| Should Fix | … | … | … | … | … |
| Consider | … | … | … | … | … |

**Severity guide:**
- **Must Fix** — breaks a documented security rule, architectural boundary, or causes test failures
- **Should Fix** — deviates from a documented convention in a way that will create inconsistency or maintenance friction
- **Consider** — a pattern that works but differs from the codebase norm; flag for discussion, not blocking

If no violations are found: "No convention violations detected."

---

## Output format

Attach both outputs as a PR review comment or save to `pr-reviews/{{PR_REF}}-doc-update.md`.

All documentation drafts are flagged **DRAFT** until approved by the PR reviewer or a designated tech lead. Include the PR number and date as provenance on every drafted change.
