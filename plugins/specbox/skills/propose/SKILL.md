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

Write planned behavior as `propose` in the same YAML format and style as
`assert`. Do not add metadata, file names, or directories. Before writing,
check every entry for completeness, correctness, feasibility, necessity,
unambiguity, and verifiability; use an existing priority mechanism only when
one already exists.

Only the selected YAML may be changed. Do not change the application, tests,
or other requirement statuses. If the SpecBoxTMS version does not support
`propose`, report it as an external blocker rather than implementing platform
support in this repository.

List the created proposals, files, sources for decisions, and unresolved
questions.
