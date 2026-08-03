---
name: propose
description: Use when turning a requested change into planned SpecBoxTMS propose requirements without changing application code.
---

# Proposing a Change

Before writing, inspect the request, affected code and YAML, test placement,
and local conventions. Separate frontend from backend only by confirmed
architectural boundaries; if the boundary is unclear, ask the user one
question and do not guess the file.

For backend HTTP API behavior, first read
`../../references/backend-http-api.md`.
For frontend behavior, first read `../../references/frontend.md`.

Write planned behavior as `propose` in the same YAML format and style as
`assert`. Do not add metadata, file names, or directories. Before writing,
check every entry for completeness, correctness, feasibility, necessity,
unambiguity, and verifiability; use an existing priority mechanism only when
one already exists.

Change only the explicitly selected affected YAML files. Before writing, list
those files and the behavior assigned to each; if any placement is ambiguous,
ask the user rather than guessing. Do not change the application, tests,
unrelated YAML, or other requirement statuses.

List the created proposals, files, sources for decisions, and unresolved
questions.
