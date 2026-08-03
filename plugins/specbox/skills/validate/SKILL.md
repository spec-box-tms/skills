---
name: validate
description: Use when validating SpecBoxTMS YAML requirements and configured Jest or JUnit test mappings.
---

# Validating SpecBoxTMS

First read `.tms.json`, existing YAML, available reports, and project scripts.
Determine the installed version and available commands through project scripts
or `npx spec-box --help`; do not invent CLI flags.

If the command, configuration, YAML, or required report cannot be read well
enough to start validation, return one **Preflight error** section and stop. Do
not present missing validation results as success.

Use standard SpecBox tooling to validate YAML structure, required fields, code
uniqueness, and links. Apply the same structural rules to `assert` and
`propose`.

Using `.tms.json` configuration, map `assert` entries to Jest/JUnit reports. If
preflight succeeds, return exactly three sections:

1. **Structure and link errors** — the only cause of unsuccessful format
   validation.
2. **Test mapping** — discovered links and missing reports.
3. **Uncovered `assert` entries** — an informational list.

`propose` does not participate in coverage. An uncovered `assert` is not an
error and does not revert it to `propose`.
