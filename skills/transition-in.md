# Skill: Transition In (Phase 1 — AI-Accelerated Onboarding)

## Description

Build a comprehensive codebase intelligence baseline and project knowledge base for an incoming team. This skill operationalises Phase 1 of the AI-accelerated team transition methodology: architecture maps, git hotspot analysis, ADR decision archaeology, technical debt inventory, domain glossary, role-specific onboarding paths, starter-ticket recommendations, comprehension checks, and an incumbent knowledge-capture kit.

Use this skill during the first one to two weeks of a new engagement before the full team arrives.

---

## Instructions

You are a senior technical lead executing Phase 1 of an AI-accelerated team transition. Your goal is to systematically analyse the target codebase and produce a validated, human-reviewable intelligence baseline that every incoming engineer can use from day one.

**All outputs are drafts. Every generated artifact must be flagged for senior-engineer review before publication.**

Work through the following steps in order. For each step, use the corresponding prompt from `prompts/` as your detailed guide. Do not skip steps — partial baselines create false confidence.

---

### Step 1 — Scope and access inventory

Before analysing anything, establish what you have access to:

1. List every repository, service, and infrastructure component in scope.
2. Identify what you do NOT have access to (databases, third-party APIs, staging environments, tickets) and record these as explicit gaps — they become risk items.
3. Confirm the tech stack: languages, frameworks, package managers, CI/CD tooling, deployment targets.
4. Record the output in a `baseline/00-scope.md` file.

---

### Step 2 — Architecture map

Traverse the codebase and produce a module-by-module architecture summary.

Use prompt: `prompts/architecture-map.md`

Produce:
- A top-level overview describing what the system does and its primary user-facing capabilities
- A module/service inventory table (name, purpose, primary language, entry points, external dependencies)
- A dependency graph in Mermaid or PlantUML (whichever is simpler given the codebase)
- Identification of any orphaned, deprecated, or undocumented modules
- Confidence rating (High / Medium / Low) and a list of open questions for incumbent review

Save to `baseline/01-architecture-map.md`.

---

### Step 3 — Change hotspot analysis

Analyse the version control history to identify risk concentration.

Use prompt: `prompts/hotspot-analysis.md`

Produce:
- A ranked table of the 20 most frequently changed files over the last 18 months
- Files with the highest defect-to-change correlation (look for fix/bug commit messages near the same files)
- Modules with the most contributors (high bus-factor risk if contributor count is low)
- A short narrative on what the hotspot pattern tells you about where the system is fragile
- Recommended early-attention areas for the incoming team

Save to `baseline/02-hotspot-analysis.md`.

---

### Step 4 — ADR archaeology

Mine architectural decisions from the codebase history.

Use prompt: `prompts/adr-archaeology.md`

Produce:
- A draft ADR for each significant decision you can reconstruct (target: the 5–10 most impactful)
- Each ADR must follow the standard format: Title, Status, Context, Decision, Consequences, Source evidence (commit hashes, PR numbers, or ticket IDs)
- A list of decisions that appear to have been made but whose rationale cannot be reconstructed — these are explicit knowledge gaps
- Flag every ADR as DRAFT and note that it requires validation by an incumbent team member

Save to `baseline/03-adr-archaeology/` (one file per ADR, named `NNNN-short-title.md`).

---

### Step 5 — Technical debt inventory

Audit the codebase for risk-bearing technical debt.

Use prompt: `prompts/tech-debt-inventory.md`

Produce:
- Dependency audit: outdated packages, known CVEs, packages with no upstream activity
- Dead code candidates: unreferenced exports, disabled feature flags, commented-out blocks
- Test coverage gaps: untested modules, missing integration tests, absence of contract or e2e tests
- Undocumented configuration: environment variables with no documentation, magic numbers, hardcoded values
- A severity table (Critical / High / Medium / Low) with estimated remediation effort
- Items that must be addressed before the incoming team can work safely

Save to `baseline/04-tech-debt-inventory.md`.

---

### Step 6 — Domain glossary

Extract the project's domain vocabulary.

Scan the codebase, documentation, commit messages, and any available tickets for:
- Domain-specific terms that appear frequently but are not self-evident to an outsider
- Abbreviations and acronyms used in code or documentation
- Names of internal systems, services, or concepts that the team uses as shorthand

For each term, provide: the term itself, a plain-English definition, where it appears in the codebase, and any synonyms or related terms.

Save to `baseline/05-domain-glossary.md`.

---

### Step 7 — Role-specific onboarding paths

Generate a guided onboarding path for each engineer role joining the project.

Use prompt: `prompts/role-onboarding-path.md` (run once per role).

Standard roles to cover unless told otherwise:
- Backend engineer
- Frontend engineer
- DevOps / SRE
- QA / test engineer
- Tech lead / architect

Each path should include:
- "Start here" — the 3–5 files or docs that give the fastest orientation
- A guided reading order through the codebase's most important areas for that role
- The 3 most common tasks for that role and where in the codebase they happen
- Pitfalls and gotchas specific to that role's work
- Suggested first tickets (well-bounded, representative, low-risk)

Save to `baseline/06-onboarding-paths/` (one file per role).

---

### Step 8 — Comprehension checks

Generate scenario-based verification exercises.

Use prompt: `prompts/comprehension-checks.md`

Produce a set of comprehension checks for each major subsystem. Each check should include:
- A scenario question ("A user reports that X is happening — where would you look first?")
- A "what would break if…" exercise for a key component
- An architecture walkthrough prompt (describe the data flow for operation Y)
- A reference answer for the assessor (not shown to the engineer being checked)

Target: 3–5 checks per major subsystem. Save to `baseline/07-comprehension-checks/` (one file per subsystem).

---

### Step 9 — Incumbent knowledge-capture kit

Prepare materials for extracting tacit knowledge from the outgoing or incumbent team.

Use prompt: `prompts/incumbent-knowledge-capture.md` if it exists, otherwise generate the following:

Produce:
- An interview guide: 10–15 questions focused on "things the documentation doesn't tell you", fragile areas, and known workarounds
- A system walkthrough prompt: a script for a 60-minute recorded walkthrough of the riskiest subsystems
- An incident retrospective template: structured questions to extract learning from the 3 most recent significant incidents
- A "bus factor audit" template: for each subsystem, who are the 1–2 people whose departure would hurt most, and what do they know that isn't written down?

Save to `baseline/08-knowledge-capture-kit/`.

---

### Step 10 — Baseline summary and review checklist

Compile everything into an executive summary for senior-engineer and incumbent review.

Produce:
- A one-page narrative summary of the system: what it does, its main risks, the state of its documentation, and the top 5 things the incoming team needs to know before touching production
- A review checklist: every artifact generated in steps 1–9, with a column for the reviewer's name, date reviewed, and confidence rating
- A gap register: everything that could not be reconstructed and must be obtained from incumbent experts or through direct investigation
- A recommended wave schedule: suggested order for onboarding engineers given the risk and complexity map

Save to `baseline/00-summary.md` and `baseline/00-review-checklist.md`.

---

## Output structure

```
baseline/
  00-scope.md
  00-summary.md
  00-review-checklist.md
  01-architecture-map.md
  02-hotspot-analysis.md
  03-adr-archaeology/
    0001-*.md
    0002-*.md
    ...
  04-tech-debt-inventory.md
  05-domain-glossary.md
  06-onboarding-paths/
    backend-engineer.md
    frontend-engineer.md
    devops-sre.md
    qa-test-engineer.md
    tech-lead-architect.md
  07-comprehension-checks/
    <subsystem-name>.md
    ...
  08-knowledge-capture-kit/
    interview-guide.md
    walkthrough-script.md
    incident-retrospective-template.md
    bus-factor-audit-template.md
```

---

## Quality gates

Before handing the baseline to the incoming team:

- [ ] Every artifact has been reviewed by at least one senior engineer
- [ ] At least one incumbent team member has validated or annotated the architecture map and ADRs
- [ ] The gap register has been triaged — each gap is either accepted as a known risk or assigned for follow-up
- [ ] Comprehension checks have been piloted with at least one incoming engineer
- [ ] All DRAFT flags remain on unvalidated artifacts
