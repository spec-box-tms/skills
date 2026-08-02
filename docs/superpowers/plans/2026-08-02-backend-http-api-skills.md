# Backend HTTP API Skills Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add one reusable HTTP API reference and the backend behavior for `specbox:extract`, `specbox:propose`, and `specbox:review`.

**Architecture:** The plugin root remains this repository. A single Markdown reference defines the backend HTTP API convention. Each of the three autonomous skills loads that reference only for a backend HTTP API task and applies its own evidence, writing, or read-only workflow. No scripts, new YAML fields, runtime core, or marketplace entry are added.

**Tech Stack:** Codex plugin manifest, Markdown `SKILL.md`, Markdown reference, SpecBoxTMS YAML, `python3` skill validator.

## Global Constraints

- One backend YAML file represents exactly one HTTP method plus path template.
- `description` is Markdown and holds TypeScript request and response models.
- `specs-unit` groups requirements by HTTP response status.
- `assert` and `propose` use identical quality criteria; only implementation status differs.
- An external model used in the TypeScript block has a `$<feature-code>` link immediately below that block.
- Authorization belongs to its own feature; protected endpoints state their `403 Forbidden` behavior and link to it.
- Preserve project-local paths, feature-code conventions, and unrelated changes.
- `review` never edits files; `propose` never edits application code.
- Do not add frontend rules, background jobs, queues, integrations, scripts, or a marketplace entry in this plan.

---

## Planned file structure

| File | Responsibility |
| --- | --- |
| `.codex-plugin/plugin.json` | Makes the repository a `specbox` plugin and exposes `./skills`. |
| `skills/references/backend-http-api.md` | Single source of backend HTTP API contract and quality rules. |
| `skills/extract/SKILL.md` | Extracts proven HTTP API behavior as `assert`. |
| `skills/propose/SKILL.md` | Writes requested HTTP API changes as `propose`. |
| `skills/review/SKILL.md` | Reviews HTTP API requirements read-only. |

The existing design calls for four additional skills. They are intentionally absent from this implementation slice; do not create empty directories or placeholder skills.

### Task 1: Create the minimal plugin shell and common reference

**Files:**

- Create: `.codex-plugin/plugin.json`
- Create: `skills/references/backend-http-api.md`

**Consumes:** [backend HTTP API design](../specs/2026-08-02-backend-http-api-design.md).

**Produces:** A valid plugin manifest and a reference reachable from the three skill folders at `../references/backend-http-api.md`.

- [ ] **Step 1: Check the precondition for the plugin manifest**

Run: `test ! -e .codex-plugin/plugin.json`

Expected: exit code `0`. The root currently has no manifest, so the task creates one rather than replacing a user-managed manifest.

- [ ] **Step 2: Create the failing validation case**

Create the minimal manifest with an intentionally invalid `"version": "0"`, then run:

```bash
python3 /Users/sr480/.codex/skills/.system/plugin-creator/scripts/validate_plugin.py .
```

Expected: FAIL because `0` is not strict semantic versioning.

- [ ] **Step 3: Replace it with the minimal valid manifest and shared reference**

Write this manifest, omitting marketplace, hooks, MCP, apps, and asset fields:

```json
{
  "name": "specbox",
  "version": "0.1.0",
  "description": "Codex skills for SpecBoxTMS functional requirements.",
  "author": { "name": "SpecBoxTMS" },
  "skills": "./skills",
  "interface": {
    "displayName": "SpecBox",
    "shortDescription": "Work with SpecBoxTMS requirements",
    "longDescription": "Create, extract, review, and apply SpecBoxTMS requirements.",
    "developerName": "SpecBoxTMS",
    "category": "Productivity",
    "capabilities": ["Write"],
    "defaultPrompt": ["Extract backend HTTP API requirements with SpecBox."]
  }
}
```

In `skills/references/backend-http-api.md`, write the agreed rules from the design verbatim in six compact sections: file boundary, `description` TypeScript contract, status groups, `assert`/`propose` scenario shape, shared quality criteria, and authorization/model links. Include the `GET /orders/{orderId}` example from the design.

- [ ] **Step 4: Verify the shell and reference**

Run:

```bash
python3 /Users/sr480/.codex/skills/.system/plugin-creator/scripts/validate_plugin.py .
rg -n 'HTTP method|description|specs-unit|assert|propose|403 Forbidden|\$<feature-code>' skills/references/backend-http-api.md
```

Expected: manifest validation passes; the search returns every required rule heading or term.

- [ ] **Step 5: Commit the shell and reference**

```bash
git add .codex-plugin/plugin.json skills/references/backend-http-api.md
git commit -m "feat: add backend HTTP API reference"
```

### Task 2: Implement and forward-test `specbox:extract`

**Files:**

- Create: `skills/extract/SKILL.md`

**Consumes:** `skills/references/backend-http-api.md`, existing code/routes/tests/specifications in the target project.

**Produces:** One endpoint YAML file per proven method/path, containing only `assert` entries.

- [ ] **Step 1: Run a baseline scenario without the skill**

In a fresh task that cannot load `skills/extract/SKILL.md`, provide this request and record the full response in the task transcript:

> Analyze an HTTP route `GET /orders/{orderId}`. Existing code returns `200` with `Order` for an existing record, `403` without authorization, and `404` when no record exists. `Order` is described by the existing `$order-model` feature. Create SpecBox requirements; do not describe unimplemented behavior.

Expected baseline failure: the agent has no instruction that forces endpoint-per-file grouping, TypeScript contract documentation, status groups, or an explicit `$order-model` link beneath the code block.

- [ ] **Step 2: Write the minimal skill**

Create frontmatter with `name: extract` and a description that triggers for extracting verified behavior from source code and tests into SpecBox requirements. In the body:

1. Inspect repository structure, existing YAML, routes, handlers, models, and tests before selecting a file.
2. If the behavior is backend HTTP API, read `../references/backend-http-api.md`; otherwise follow the generic extract contract from `docs/design.md`.
3. Create or update one feature file per method/path using the target project's path and code conventions.
4. Put TypeScript contract models in `description`, status groups in `specs-unit`, and only evidenced `assert` scenarios in the groups.
5. Link reused models below the code block; link authorization from the `403 Forbidden` scenario.
6. Ask the user to decide only when frontend/backend ownership cannot be established from the project.
7. Report written files, proof sources, and any behavior deliberately omitted for lack of evidence.

- [ ] **Step 3: Run the same scenario with the skill**

Use a fresh task with the same prompt, explicitly loading `skills/extract/SKILL.md`.

Expected: one `GET /orders/{orderId}` feature; TypeScript contract in `description`; groups `200 OK`, `403 Forbidden`, and `404 Not Found`; only `assert` keys; `$order-model` link outside the code block; no inferred status or field.

- [ ] **Step 4: Validate the skill structure**

Run:

```bash
python3 /Users/sr480/.codex/skills/.system/skill-creator/scripts/quick_validate.py skills/extract
```

Expected: validation passes with frontmatter name `extract` and a nonempty description.

- [ ] **Step 5: Commit the validated skill**

```bash
git add skills/extract/SKILL.md
git commit -m "feat: add specbox extract skill"
```

### Task 3: Implement and forward-test `specbox:propose`

**Files:**

- Create: `skills/propose/SKILL.md`

**Consumes:** `skills/references/backend-http-api.md`, change request, existing specifications and project conventions.

**Produces:** Endpoint YAML changes containing only planned `propose` scenarios; no application-code edit.

- [ ] **Step 1: Run a baseline scenario without the skill**

In a fresh task that cannot load `skills/propose/SKILL.md`, provide this request and record the full response:

> Propose a change to `POST /orders`: valid input must return `201` with `Order`; a duplicate client request identifier must return `409` with `ApiError`. `Order` belongs to `$order-model`. Do not change application code.

Expected baseline failure: the agent can mix `assert` with `propose`, omit the contract in `description`, group by outcome text rather than status, or make a code change.

- [ ] **Step 2: Write the minimal skill**

Create frontmatter with `name: propose` and a description that triggers for recording requested behavior changes as planned SpecBox requirements. In the body:

1. Inspect existing YAML and project conventions, and determine backend/frontend ownership before writing.
2. For backend HTTP API, read `../references/backend-http-api.md` and use one feature file per method/path.
3. Verify whether the installed SpecBoxTMS CLI accepts `propose`; if it does not, report the incompatible platform version and do not attempt to alter the CLI, API, storage, or UI.
4. Write or update the TypeScript contract in `description` and status groups in `specs-unit`.
5. Add only `propose` keys for the change request; do not recast existing behavior as `assert` and do not modify application code.
6. Check every proposal against the shared criteria before writing; name uncertainty and ask the user when it blocks a precise contract.
7. Preserve unrelated YAML and report changed specs plus open decisions.

- [ ] **Step 3: Run the same scenario with the skill**

Use a fresh task with the same prompt, explicitly loading `skills/propose/SKILL.md`.

Expected: a `POST /orders` feature with request and response models in `description`, a visible `$order-model` link below the TypeScript block, `201 Created` and `409 Conflict` groups, only `propose` entries, and no source-code change.

- [ ] **Step 4: Validate the skill structure**

Run:

```bash
python3 /Users/sr480/.codex/skills/.system/skill-creator/scripts/quick_validate.py skills/propose
```

Expected: validation passes.

- [ ] **Step 5: Commit the validated skill**

```bash
git add skills/propose/SKILL.md
git commit -m "feat: add specbox propose skill"
```

### Task 4: Implement and forward-test `specbox:review`

**Files:**

- Create: `skills/review/SKILL.md`

**Consumes:** `skills/references/backend-http-api.md` and selected YAML files.

**Produces:** Read-only findings with feature, status group, violated criterion, explanation, and minimum correction.

- [ ] **Step 1: Run a baseline scenario without the skill**

In a fresh task that cannot load `skills/review/SKILL.md`, provide this YAML and record the full response:

````yaml
feature: POST /orders
code: create-order
description: |
  ```ts
  type CreateOrderRequest = { body: { itemId: string } };
  type Order = { id: string };
  ```
specs-unit:
  Success:
    - propose: API usually creates the order.
  409 Conflict:
    - assert: For a duplicate request API returns 201.
````

Expected baseline failure: the response may edit the YAML, omit a criterion, or miss that `Success` is not a status group and that `409 Conflict` contradicts the asserted `201`.

- [ ] **Step 2: Write the minimal skill**

Create frontmatter with `name: review` and a description that triggers for read-only reviews of SpecBox requirements. In the body:

1. Do not modify specs, source code, configuration, or tests.
2. For backend HTTP API requirements, read `../references/backend-http-api.md` before reviewing.
3. Check individual requirements for observable input/precondition, status, output/effect, correctness, feasibility, necessity, unambiguity, and testability.
4. Check the feature for method/path boundary, TypeScript contract, status-group consistency, and explicit links for reused models/authorization.
5. Check the selected set for duplicate method/path pairs and unresolved links when the necessary files are in scope.
6. Emit one finding per issue in this exact shape: `feature — group — criterion: explanation. Minimal correction: correction.`
7. Separate actual findings from coverage information; absence of an automated test is not a format or quality error.

- [ ] **Step 3: Run the same scenario with the skill**

Use a fresh task with the same YAML, explicitly loading `skills/review/SKILL.md`.

Expected: no files change. Findings identify at least: invalid status-group title `Success`, untestable/ambiguous wording “usually”, and the `409 Conflict` versus `201` contradiction. Each finding includes all five required parts.

- [ ] **Step 4: Validate the skill structure**

Run:

```bash
python3 /Users/sr480/.codex/skills/.system/skill-creator/scripts/quick_validate.py skills/review
```

Expected: validation passes.

- [ ] **Step 5: Commit the validated skill**

```bash
git add skills/review/SKILL.md
git commit -m "feat: add specbox review skill"
```

### Task 5: Validate the integrated backend slice

**Files:**

- Verify: `.codex-plugin/plugin.json`
- Verify: `skills/references/backend-http-api.md`
- Verify: `skills/extract/SKILL.md`
- Verify: `skills/propose/SKILL.md`
- Verify: `skills/review/SKILL.md`

**Consumes:** The outputs of Tasks 1–4.

**Produces:** A plugin whose three backend skills use the same reference while retaining independent workflows.

- [ ] **Step 1: Validate every skill and the plugin**

Run:

```bash
python3 /Users/sr480/.codex/skills/.system/skill-creator/scripts/quick_validate.py skills/extract
python3 /Users/sr480/.codex/skills/.system/skill-creator/scripts/quick_validate.py skills/propose
python3 /Users/sr480/.codex/skills/.system/skill-creator/scripts/quick_validate.py skills/review
python3 /Users/sr480/.codex/skills/.system/plugin-creator/scripts/validate_plugin.py .
```

Expected: all four commands exit `0`.

- [ ] **Step 2: Check common-reference use and forbidden additions**

Run:

```bash
rg -n '\.\./references/backend-http-api\.md' skills/extract/SKILL.md skills/propose/SKILL.md skills/review/SKILL.md
test ! -e skills/create/SKILL.md
test ! -e skills/validate/SKILL.md
test ! -e skills/write-tests/SKILL.md
test ! -e skills/apply/SKILL.md
```

Expected: the first command returns one reference from each skill; each `test` exits `0` because this slice does not create unrelated skills.

- [ ] **Step 3: Inspect the committed result**

Run:

```bash
git log --oneline -4
git status --short
```

Expected: four feature commits appear after the design commit and the worktree is clean.
