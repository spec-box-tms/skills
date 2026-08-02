# Frontend Requirements References Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add frontend functional-requirement references and connect them to the
`extract`, `propose`, and `review` skills.

**Architecture:** A single `frontend.md` reference contains cross-cutting
selection, evidence, state/error, and traceability rules. Eight focused
references provide the applicable facts, questions, quality criteria, and
standard `specs-unit` groups. The three relevant skills dispatch to the main
reference only for confirmed frontend behavior.

**Tech Stack:** Markdown, Codex skills, SpecBoxTMS YAML conventions.

## Global Constraints

- Do not prescribe visual design, internal frontend models, YAML templates, or
  canonical requirement wording.
- Ask only for facts absent from the request, existing specifications, code,
  and tests; never record absence of behavior as a requirement.
- Keep loading, empty, error, progress, and completion behavior in the feature
  where it occurs.
- Do not add dependencies, scripts, new YAML fields, names, or directories.
- A separate field feature is linked from its form; dependent fields link to
  their source fields; monorepo frontend API links appear once in `description`.

---

## File structure

- Create `plugins/specbox/references/frontend.md` — cross-cutting frontend
  selection, evidence, skill-mode, state/error, link, and group rules.
- Create `plugins/specbox/references/frontend-navigation.md` — navigation and
  entry checklist.
- Create `plugins/specbox/references/frontend-data-presentation.md` — data
  presentation checklist.
- Create `plugins/specbox/references/frontend-selection-filtering.md` — search,
  filtering, sorting, pagination, and selection checklist.
- Create `plugins/specbox/references/frontend-forms.md` — form checklist.
- Create `plugins/specbox/references/frontend-form-fields.md` — field checklist
  and type-driven validation choices.
- Create `plugins/specbox/references/frontend-actions.md` — consequential
  actions checklist.
- Create `plugins/specbox/references/frontend-access.md` — availability and
  access restrictions checklist.
- Create `plugins/specbox/references/frontend-accessible-interaction.md` —
  keyboard, focus, and dynamic-state announcement checklist.
- Modify `plugins/specbox/skills/extract/SKILL.md` — read the frontend main
  reference for frontend behavior.
- Modify `plugins/specbox/skills/propose/SKILL.md` — read the frontend main
  reference for frontend behavior.
- Modify `plugins/specbox/skills/review/SKILL.md` — read the frontend main
  reference for frontend behavior.

### Task 1: Add the frontend main reference

**Files:**
- Create: `plugins/specbox/references/frontend.md`

**Produces:** The common entry point for frontend requirement work. Its child
reference names are the eight files created in later tasks.

- [ ] **Step 1: Write the main reference**

Include these sections: scope; feature-boundary selection; source precedence;
the separate behavior of `extract`, `propose`, and `review`; common quality
criteria; state/error rules; API, form, and field links; child-reference
selection; and rules for standard versus proposed `specs-unit` groups.

- [ ] **Step 2: Verify the reference is self-contained**

Run:

```sh
rg -n '^#|^##|frontend-(navigation|data-presentation|selection-filtering|forms|form-fields|actions|access|accessible-interaction)' plugins/specbox/references/frontend.md
```

Expected: the main sections and all eight child-reference names are present.

- [ ] **Step 3: Commit the main reference**

```sh
git add plugins/specbox/references/frontend.md
git commit -m "docs: add frontend requirements reference"
```

### Task 2: Add navigation, data, and selection checklists

**Files:**
- Create: `plugins/specbox/references/frontend-navigation.md`
- Create: `plugins/specbox/references/frontend-data-presentation.md`
- Create: `plugins/specbox/references/frontend-selection-filtering.md`

**Consumes:** The shared rules in `frontend.md`.

**Produces:** Three checklists with their own standard groups and questions.

- [ ] **Step 1: Write the navigation checklist**

Cover entry, transitions, return/history, applicable states, and error handling.
Require the agent to establish the initiator, origin, destination, preserved
context, route parameters when functional, and browser-history behavior only
when the feature uses it. Set standard groups to `Entry`, `Transitions`,
`Return and history`, `States`, and `Error handling`.

- [ ] **Step 2: Write the data-presentation checklist**

Cover the information users must receive, functional grouping and ordering,
when it refreshes, relevant states, and recovery from failed retrieval. Set
standard groups to `Presentation`, `Data refresh`, `States`, and `Error
handling`. Do not prescribe a visual component.

- [ ] **Step 3: Write the selection-and-filtering checklist**

Cover search terms, filter criteria, sorting, pagination, single or multiple
selection, selection persistence, and reset behavior. Set standard groups to
`Search`, `Filtering`, `Sorting`, `Pagination`, `Selection`, `Reset
conditions`, `States`, and `Error handling`. Leave actions on selected items to
the consequential-actions checklist.

- [ ] **Step 4: Verify group vocabularies and scope**

Run:

```sh
rg -n 'Entry|Transitions|Presentation|Data refresh|Search|Filtering|Selection|Error handling' plugins/specbox/references/frontend-navigation.md plugins/specbox/references/frontend-data-presentation.md plugins/specbox/references/frontend-selection-filtering.md
git diff --check
```

Expected: all named groups are present and the diff has no whitespace errors.

- [ ] **Step 5: Commit the three checklists**

```sh
git add plugins/specbox/references/frontend-navigation.md plugins/specbox/references/frontend-data-presentation.md plugins/specbox/references/frontend-selection-filtering.md
git commit -m "docs: add frontend navigation and data checklists"
```

### Task 3: Add form and field checklists

**Files:**
- Create: `plugins/specbox/references/frontend-forms.md`
- Create: `plugins/specbox/references/frontend-form-fields.md`

**Consumes:** The form/field linking and no-template constraints in
`frontend.md`.

**Produces:** A form checklist and a reusable field checklist.

- [ ] **Step 1: Write the form checklist**

Cover the feature purpose, create/edit modes, inline versus separate fields,
initial values, save, cancel, states, and error handling. State that a form
links to every separate field feature while simple fields may remain inline.
Set standard groups to `Composition`, `Initialization`, `Save`, `Cancel`,
`States`, and `Error handling`.

- [ ] **Step 2: Write the field checklist**

Cover label, placeholder, help text, input interaction, value semantics,
validation, validation timing and message, and dependencies. Set standard
groups to `Presentation`, `Input`, `Validation`, and `Dependencies`. Require
the agent to offer appropriate optional validator categories for text, numeric,
date/time, choice, file, and consent values, without inventing a validator.
Require a dependent field to link to its source field and prohibit a backlink
to its parent form.

- [ ] **Step 3: Verify field/form relationship rules**

Run:

```sh
rg -n 'inline|separate field|link|label|placeholder|Validation|Dependencies|text|numeric|date|file|consent' plugins/specbox/references/frontend-forms.md plugins/specbox/references/frontend-form-fields.md
git diff --check
```

Expected: the form-to-field and type-driven validation rules are present with
no whitespace errors.

- [ ] **Step 4: Commit the form references**

```sh
git add plugins/specbox/references/frontend-forms.md plugins/specbox/references/frontend-form-fields.md
git commit -m "docs: add frontend form requirement checklists"
```

### Task 4: Add action, access, and accessible-interaction checklists

**Files:**
- Create: `plugins/specbox/references/frontend-actions.md`
- Create: `plugins/specbox/references/frontend-access.md`
- Create: `plugins/specbox/references/frontend-accessible-interaction.md`

**Consumes:** The common state/error and traceability rules in `frontend.md`.

**Produces:** Checklists for consequential behavior, authorization, and
accessible functional control.

- [ ] **Step 1: Write the consequential-actions checklist**

Cover the initiator, preconditions, target scope (including selected items),
confirmation, cancellation, progress, observable effect, result, and failure
recovery. Set standard groups to `Initiation`, `Confirmation`, `Execution`,
`Result`, and `Error handling`.

- [ ] **Step 2: Write the access checklist**

Cover which roles or conditions make a feature available, how restrictions
affect visibility or invocation, and what the user receives when a restricted
operation is attempted. Set standard groups to `Availability` and
`Restrictions`.

- [ ] **Step 3: Write the accessible-interaction checklist**

Cover keyboard activation and movement, focus placement and return, and
announcements of meaningful dynamic changes. Set standard groups to `Keyboard
control`, `Focus`, and `State announcements`. Keep this about observable
interaction rather than visual styling or implementation technology.

- [ ] **Step 4: Verify the three scopes do not overlap**

Run:

```sh
rg -n 'Initiation|Confirmation|Availability|Restrictions|Keyboard control|Focus|State announcements' plugins/specbox/references/frontend-actions.md plugins/specbox/references/frontend-access.md plugins/specbox/references/frontend-accessible-interaction.md
git diff --check
```

Expected: every standard group is present and the diff has no whitespace
errors.

- [ ] **Step 5: Commit the checklists**

```sh
git add plugins/specbox/references/frontend-actions.md plugins/specbox/references/frontend-access.md plugins/specbox/references/frontend-accessible-interaction.md
git commit -m "docs: add frontend action and access checklists"
```

### Task 5: Connect the frontend reference to the three skills

**Files:**
- Modify: `plugins/specbox/skills/extract/SKILL.md`
- Modify: `plugins/specbox/skills/propose/SKILL.md`
- Modify: `plugins/specbox/skills/review/SKILL.md`

**Consumes:** `plugins/specbox/references/frontend.md`.

**Produces:** Frontend behavior dispatch in each relevant skill without
changing their backend behavior or scope.

- [ ] **Step 1: Update `extract`**

Add a frontend counterpart to its backend-reference instruction. It must read
`../../references/frontend.md` before extracting frontend behavior and retain
the rule that only evidenced behavior becomes `assert`.

- [ ] **Step 2: Update `propose`**

Add a frontend counterpart to its backend-reference instruction. It must read
`../../references/frontend.md` before proposing frontend behavior and retain
the rule that user decisions are not invented.

- [ ] **Step 3: Update `review`**

Add a frontend counterpart to its backend-reference instruction. It must read
`../../references/frontend.md` before reviewing frontend behavior and report
concrete unanswered questions with concise options when apparent.

- [ ] **Step 4: Run the documentation integration checks**

Run:

```sh
rg -n 'references/frontend.md' plugins/specbox/skills/extract/SKILL.md plugins/specbox/skills/propose/SKILL.md plugins/specbox/skills/review/SKILL.md
rg -n '^#|^##' plugins/specbox/references/frontend*.md
git diff --check
git status --short
```

Expected: all three skills reference the frontend entry point, all nine
references have headings, there are no whitespace errors, and only intended
files are changed.

- [ ] **Step 5: Commit the integration**

```sh
git add plugins/specbox/skills/extract/SKILL.md plugins/specbox/skills/propose/SKILL.md plugins/specbox/skills/review/SKILL.md
git commit -m "feat: apply frontend requirement references"
```

## Plan self-review

- Spec coverage: Tasks 1-4 implement the main reference and every approved
  checklist, including their standard groups, form-field behavior, states,
  errors, traceability, and type-driven validation. Task 5 connects all three
  required skills.
- Placeholder scan: no incomplete task markers or deferred implementation
  notes are present.
- Consistency: all child-reference paths are named in Task 1 and match the
  files created in Tasks 2-4; all three skill paths match the existing plugin
  structure.
