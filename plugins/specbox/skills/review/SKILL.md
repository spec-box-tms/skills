---
name: review
description: Use when performing a read-only quality review of selected SpecBoxTMS requirement files or entries.
---

# Reviewing Requirements

Work read-only: do not edit YAML, configuration, or code.

For backend HTTP API requirements, first read
`{SKILL_DIR}/../../references/backend-http-api.md`.
For frontend requirements, first read
`{SKILL_DIR}/../../references/frontend.md`.

For every selected requirement, check completeness, correctness, feasibility,
necessity, unambiguity, and verifiability. Check priority only if the project
already has a way to express it. For a requirements set, check completeness,
consistency, modifiability, and traceability.

Write every finding as:

`<code or location> — <Wiegers criterion>: <explanation>. Minimum: <recommendation>.`

For a frontend gap, the recommendation names the exact unresolved question and
offers concise options when they are apparent.

Do not add fields merely to satisfy the model formally, and do not call a
missing automated test a structural error. If there are no findings, state the
review scope and criteria checked explicitly.
