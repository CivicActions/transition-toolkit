# Prompt: Technical Debt Inventory

Produce a technical debt inventory for `{{PROJECT_NAME}}` at `{{REPO_ROOT}}`.

## Tech stack context

- Languages: `{{TECH_STACK}}`
- Package manager(s): `{{PACKAGE_MANAGER}}`
- CI/CD platform: `{{CI_PLATFORM}}`

## Instructions

Work through each category below. For each item, provide: a description, the file(s) affected, an estimated remediation effort (Hours / Days / Weeks), and a severity rating.

**Severity ratings:**
- **Critical** — actively poses security, data loss, or compliance risk, or will block work in the near term
- **High** — significantly slows development or poses elevated risk; should be addressed within 1–2 sprints
- **Medium** — noticeable friction; address within the quarter
- **Low** — minor; address opportunistically

---

### Category 1 — Dependency audit

1. List all direct dependencies and their current vs latest versions.
2. Flag any dependency that is:
   - More than 2 major versions behind its latest release
   - End-of-life or no longer actively maintained (check for archived repos, no releases in 18+ months)
   - Listed in a public vulnerability database (CVE, npm audit, composer audit, pip-audit, etc.)
   - A transitive dependency that has been promoted to direct use without being declared

Produce:

| Dependency | Current version | Latest version | Lag | Known CVEs | Maintenance status | Severity |
|---|---|---|---|---|---|---|
| … | … | … | … | … | Active/Inactive/EOL | C/H/M/L |

---

### Category 2 — Dead code candidates

Search for:
- Exported functions, classes, or types that have no references in the codebase (use static analysis or grep)
- Feature flags that appear to have been permanently disabled (flag value is always false/off, or the flag name doesn't appear in any non-test configuration)
- Files or directories explicitly named `_old`, `_deprecated`, `_unused`, `archive`, `legacy`
- Commented-out code blocks longer than 5 lines

| Item | Path | Evidence of disuse | Recommended action | Severity |
|---|---|---|---|---|
| … | … | … | Delete / Archive / Investigate | L/M/H |

---

### Category 3 — Test coverage gaps

1. If a coverage report exists, identify the 10 modules with the lowest statement/line coverage.
2. If no coverage tool is configured, identify modules that have no test files at all.
3. Flag any external-facing interface (HTTP endpoint, public API, event handler, queue consumer) that has no integration or contract test.
4. Flag any CI pipeline that has no automated test gate.

| Module / path | Coverage % (if known) | Test file exists? | Integration test? | Severity |
|---|---|---|---|---|
| … | …% / Unknown | Yes/No | Yes/No | C/H/M/L |

---

### Category 4 — Undocumented configuration

1. List all environment variables referenced in the codebase. For each, note whether it is documented in `.env.example`, README, or any configuration documentation.
2. Identify magic numbers and hardcoded values that should be configuration (hardcoded URLs, timeouts, limits, credentials).
3. Flag any secret or credential that appears to be committed to the repository (even if rotated).

| Item | Type | Location | Documented? | Severity |
|---|---|---|---|---|
| `ENV_VAR_NAME` | Environment variable | `src/config.js:14` | Yes/No | C/H/M/L |
| `300` | Magic number (timeout?) | `src/api/client.js:87` | No | L |

---

### Category 5 — Architecture and coupling debt

Based on the architecture map, identify:
- Circular dependencies between modules
- God classes or god files (single files > 500 lines that handle multiple concerns)
- Direct database access from presentation or routing layers (bypassing business logic)
- Duplicated logic across modules that should be shared

| Item | Location | Description | Severity |
|---|---|---|---|
| … | … | … | C/H/M/L |

---

### Summary table

| Category | Critical | High | Medium | Low | Total items |
|---|---|---|---|---|---|
| Dependency audit | | | | | |
| Dead code | | | | | |
| Test coverage | | | | | |
| Undocumented config | | | | | |
| Architecture debt | | | | | |
| **Total** | | | | | |

### Must-address before handover

List any items that the incoming team must address before they can work safely on the codebase — typically any Critical items and any High items with no workaround.

---

## Output format

Markdown. Save to `baseline/04-tech-debt-inventory.md`.

## Quality reminder

This inventory is a starting point, not an audit. Flag your confidence and note any areas you could not inspect (e.g., no access to runtime metrics, no CVE database tool available).
