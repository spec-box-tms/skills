# Backend HTTP API Skills Implementation Plan

**Goal:** Extend the existing `plugins/specbox` plugin with one backend HTTP API reference used by `extract`, `propose`, and `review`.

**Architecture:** Keep the existing seven skills and marketplace layout. Place the reusable rules at `plugins/specbox/references/backend-http-api.md`; each of the three relevant skills reads it only for backend HTTP API requirements. Do not add a core skill, scripts, dependencies, YAML fields, or file-name rules beyond the agreed endpoint boundary.

## Files

| File | Change |
| --- | --- |
| `plugins/specbox/.codex-plugin/plugin.json` | Bump `0.1.0` to `0.2.0`. |
| `plugins/specbox/references/backend-http-api.md` | Add the shared backend HTTP API rules. |
| `plugins/specbox/skills/extract/SKILL.md` | Read the reference before extracting backend API `assert` requirements. |
| `plugins/specbox/skills/propose/SKILL.md` | Read the reference before writing backend API `propose` requirements. |
| `plugins/specbox/skills/review/SKILL.md` | Read the reference before read-only backend API review. |

## Task 1: Add the backend reference

- [ ] Confirm `plugins/specbox/references/backend-http-api.md` is absent.
- [ ] Write rules for one YAML per HTTP method and path template; Markdown `description` with TypeScript request/response models; status-based `specs-unit` groups; and one scenario per `assert` or `propose`.
- [ ] Require an explicit `$<feature-code>` link below a TypeScript block when it uses another feature's model.
- [ ] Require authorization to remain a separate feature and a protected endpoint to state its `403 Forbidden` behavior with a link to that feature.
- [ ] Define the shared individual and collection quality criteria used by `extract`, `propose`, and `review`.

## Task 2: Connect the existing skills

- [ ] Add one conditional instruction to each of `extract`, `propose`, and `review`: for backend HTTP API work, read `../../references/backend-http-api.md` before performing its existing workflow.
- [ ] Preserve `extract` as evidence-only `assert`, `propose` as application-code-free `propose`, and `review` as read-only.
- [ ] Do not add the reference to `create`, `validate`, `write-tests`, or `apply`; their contracts do not need endpoint-authoring rules.

## Task 3: Validate and publish the change

- [ ] Set the plugin manifest version to `0.2.0`.
- [ ] Run `quick_validate.py` for `extract`, `propose`, and `review`.
- [ ] Run `validate_plugin.py plugins/specbox` and `git diff --check`.
- [ ] Confirm the reference path occurs once in each of the three skills and nowhere else.
- [ ] Commit the six changed files with `feat: add backend HTTP API requirements reference`.
