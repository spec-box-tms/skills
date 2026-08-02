# SpecBox Skills Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Publish the `specbox` Codex plugin with seven independent skills for the SpecBoxTMS specification lifecycle.

**Architecture:** The plugin has a single manifest at the repository root and one self-contained `SKILL.md` per contract in `skills/`. Skills use only the project filesystem, Git, the existing test runner, and `npx spec-box`; no shared runtime, scripts, or naming convention is introduced. Each workflow treats `assert` and `propose` as structurally equivalent, with implementation status independent from test coverage.

**Tech Stack:** Codex plugin manifest JSON, Agent Skills Markdown, `npx spec-box`, Python structural validators.

## Global Constraints

- Plugin namespace is `specbox:`; directory names remain `create`, `extract`, `validate`, `write-tests`, `review`, `propose`, and `apply`.
- Do not add a runtime core, orchestrator, dependencies, mandatory YAML fields, or file-naming convention.
- Inspect local source, existing specs, tests, and conventions before any write; preserve unrelated user changes.
- Ask the user when frontend/backend ownership cannot be determined from project context.
- `assert` is implemented behavior; `propose` is planned behavior; test coverage never changes either status.
- `propose` compatibility is external to this repository: report unsupported SpecBoxTMS versions rather than modifying SpecBoxTMS.
- `review` is read-only; `propose` does not change application code.
- Uncovered `assert` is informational and must not make structural validation fail.

---

### Task 1: Create and validate the plugin shell

**Files:**
- Create: `.codex-plugin/plugin.json`
- Create: `skills/`

**Interfaces:**
- Produces: plugin `specbox` with `skills` mapped to `./skills/`.

- [x] **Step 1: Record a failing manifest preflight**

Run: `python3 /Users/sr480/.codex/skills/.system/plugin-creator/scripts/validate_plugin.py .`

Expected: FAIL because `.codex-plugin/plugin.json` does not yet exist.

- [x] **Step 2: Create the minimal manifest**

```json
{
  "name": "specbox",
  "version": "0.1.0",
  "description": "Skills for managing SpecBoxTMS requirements alongside application code.",
  "author": { "name": "SpecBoxTMS" },
  "skills": "./skills/",
  "interface": {
    "displayName": "SpecBoxTMS",
    "shortDescription": "Manage SpecBoxTMS requirements",
    "longDescription": "Create, validate, review, propose, test, and implement SpecBoxTMS requirements.",
    "developerName": "SpecBoxTMS",
    "category": "Productivity",
    "capabilities": ["Write"],
    "defaultPrompt": [
      "Initialize SpecBoxTMS in this project.",
      "Review these SpecBoxTMS requirements.",
      "Implement this SpecBoxTMS proposal."
    ]
  }
}
```

- [x] **Step 3: Verify the manifest**

Run: `python3 /Users/sr480/.codex/skills/.system/plugin-creator/scripts/validate_plugin.py .`

Expected: PASS.

### Task 2: Add `specbox:create`

**Files:**
- Create: `skills/create/SKILL.md`

**Interfaces:**
- Consumes: project source, existing specs/tests, and an explicit task source.
- Produces: minimally configured `.tms.json`, only if safe to add or amend.

- [ ] **Step 1: Run a baseline scenario without the new skill**

Scenario: an existing project has `.tms.json`, frontend and backend tests, and a task only asking to initialise SpecBox. Record whether the agent preserves the config and avoids inventing requirements.

- [ ] **Step 2: Write the compact workflow**

Document the discovery order, minimal config rule, conflict handling, no-invented-requirements rule, and expected report. Include `npx spec-box` only after identifying the compatible project command.

- [ ] **Step 3: Validate its structure**

Run: `python3 /Users/sr480/.codex/skills/.system/skill-creator/scripts/quick_validate.py skills/create`

Expected: PASS.

### Task 3: Add `specbox:extract`

**Files:**
- Create: `skills/extract/SKILL.md`

**Interfaces:**
- Consumes: existing source, tests, specifications, and repository conventions.
- Produces: only evidence-backed `assert` entries in established frontend/backend YAML locations.

- [ ] **Step 1: Run a baseline scenario without the new skill**

Scenario: a repository contains mixed UI and HTTP behavior, existing YAML files, and an untested endpoint. Record whether the agent mistakes desired behavior for implemented behavior or forces a naming convention.

- [ ] **Step 2: Write the compact workflow**

Require inspection of code, tests, and YAML before writing; create `assert` only from observable implementation; preserve local placement; request a decision on genuinely ambiguous layer ownership.

- [ ] **Step 3: Validate its structure**

Run: `python3 /Users/sr480/.codex/skills/.system/skill-creator/scripts/quick_validate.py skills/extract`

Expected: PASS.

### Task 4: Add `specbox:validate`

**Files:**
- Create: `skills/validate/SKILL.md`

**Interfaces:**
- Consumes: YAML specs, `.tms.json`, and available Jest/JUnit reports.
- Produces: separate structural errors, test-mapping facts, and non-blocking uncovered-`assert` information.

- [ ] **Step 1: Run a baseline scenario without the new skill**

Scenario: YAML has a duplicate code and one valid but uncovered `assert`; a report also contains a mapped test. Record whether the agent reports the duplicate separately and keeps lack of coverage out of the error exit condition.

- [ ] **Step 2: Write the compact workflow**

Require the installed CLI/version check, normal SpecBox validation, validation of `propose` with the same structural rules, configured Jest/JUnit mapping, and a three-part result. State that unsupported `propose` is a compatibility report, not a locally implemented platform feature.

- [ ] **Step 3: Validate its structure**

Run: `python3 /Users/sr480/.codex/skills/.system/skill-creator/scripts/quick_validate.py skills/validate`

Expected: PASS.

### Task 5: Add `specbox:write-tests`

**Files:**
- Create: `skills/write-tests/SKILL.md`

**Interfaces:**
- Consumes: selected implemented `assert`, `.tms.json`, source, and the existing test suite.
- Produces: test changes using the existing runner and identifiers compatible with configured Jest/JUnit mapping.

- [ ] **Step 1: Run a baseline scenario without the new skill**

Scenario: a project already uses pytest/JUnit mapping and has an uncovered `assert`. Record whether the agent adds a second framework or fails to link the test identifier to configured mapping.

- [ ] **Step 2: Write the compact workflow**

Require reading `.tms.json` and nearby tests, TDD with the existing runner, traceable identifiers, and separate test/validation reporting. Do not turn an `assert` into `propose` if a test is unavailable.

- [ ] **Step 3: Validate its structure**

Run: `python3 /Users/sr480/.codex/skills/.system/skill-creator/scripts/quick_validate.py skills/write-tests`

Expected: PASS.

### Task 6: Add `specbox:review`

**Files:**
- Create: `skills/review/SKILL.md`

**Interfaces:**
- Consumes: selected YAML requirements or files.
- Produces: read-only findings with requirement, Wiegers criterion, explanation, and minimal recommendation.

- [ ] **Step 1: Run a baseline scenario without the new skill**

Scenario: a requirement says “fast and convenient”, has no acceptance condition, and is stored with related requirements. Record whether the agent edits YAML, offers vague criticism, or confuses missing test coverage with a structural defect.

- [ ] **Step 2: Write the compact workflow**

Cover individual completeness, correctness, feasibility, necessity, existing priority expression, unambiguity, and verifiability; cover collection completeness, consistency, modifiability, and traceability; prohibit adding metadata only to satisfy a rubric.

- [ ] **Step 3: Validate its structure**

Run: `python3 /Users/sr480/.codex/skills/.system/skill-creator/scripts/quick_validate.py skills/review`

Expected: PASS.

### Task 7: Add `specbox:propose`

**Files:**
- Create: `skills/propose/SKILL.md`

**Interfaces:**
- Consumes: change request plus project/specification context.
- Produces: quality-checked `propose` YAML entries, with no application-code changes.

- [ ] **Step 1: Run a baseline scenario without the new skill**

Scenario: a change affects both a web form and an HTTP API, but only one existing YAML location is known. Record whether the agent changes app code, adds arbitrary fields, or guesses the layer/file boundary.

- [ ] **Step 2: Write the compact workflow**

Require source and convention discovery, decomposition by evidenced frontend/backend ownership, one user question for unresolved ownership, Wiegers review before write, preserved YAML style, and compatibility reporting for unsupported `propose`.

- [ ] **Step 3: Validate its structure**

Run: `python3 /Users/sr480/.codex/skills/.system/skill-creator/scripts/quick_validate.py skills/propose`

Expected: PASS.

### Task 8: Add `specbox:apply` and complete plugin validation

**Files:**
- Create: `skills/apply/SKILL.md`
- Modify: `README.md`

**Interfaces:**
- Consumes: selected `propose`, application code, tests, and local conventions.
- Produces: implemented behavior, optional compatible tests, and a converted `assert` only after implementation.

- [ ] **Step 1: Run a baseline scenario without the new skill**

Scenario: a selected `propose` is implemented but no automated test is necessary for the project. Record whether the agent leaves it as `propose`, changes it based on validation failure, or conflates test status with implementation status.

- [ ] **Step 2: Write the compact workflow**

Require selecting the exact proposal, examining all affected callers and conventions, applying minimal code with tests when appropriate, converting only actually implemented behavior to `assert`, and reporting tests and validation independently without rollback.

- [ ] **Step 3: Add the short installation/use README section**

Document the completed plugin layout and the seven available names; do not claim a custom runtime or prescribe paths for consumers.

- [ ] **Step 4: Validate the skill, all skills, and plugin**

Run:

```bash
for skill in skills/*; do
  python3 /Users/sr480/.codex/skills/.system/skill-creator/scripts/quick_validate.py "$skill" || exit 1
done
python3 /Users/sr480/.codex/skills/.system/plugin-creator/scripts/validate_plugin.py .
git diff --check
```

Expected: all commands PASS with no whitespace errors.
