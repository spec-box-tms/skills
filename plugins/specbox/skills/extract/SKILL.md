---
name: extract
description: Use when deriving SpecBoxTMS requirements from existing application code and tests without inventing planned behavior.
---

# Extracting Implemented Requirements

Extract only behavior confirmed by the application. A test strengthens the
evidence, but its absence does not mean the behavior is absent.

1. Before writing, inspect affected code, callers, tests, existing YAML, and
   its placement. Record the source for every conclusion.
2. Describe implemented behavior as `assert` in the existing YAML format. Do
   not write desired, assumed, or only partially understood behavior.
   For backend HTTP API behavior, first read
   `../../references/backend-http-api.md`.
3. Choose a frontend or backend file only from architectural context and local
   conventions. Do not create suffixes, directories, or fields. If the layer
   cannot be determined reliably, ask the user to decide.
4. Preserve the existing file's style, codes, and links; do not overwrite
   unrelated requirements.

List the added `assert` entries, their evidence, changed files, and unresolved
boundaries. For assumptions, offer a separate `specbox:propose` invocation.
