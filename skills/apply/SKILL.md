---
name: apply
description: Use when implementing a selected SpecBoxTMS propose requirement and converting it to assert after the behavior exists.
---

# Applying a Proposal

1. Select the exact `propose`; before editing, read the requirement, affected
   code, all its callers, existing tests, and YAML conventions.
2. Implement only the stated behavior with the smallest change. Add or update
   tests when appropriate for the stack and behavior; use the existing runner
   and `.tms.json` configuration.
3. Convert the selected entry to `assert` only after the behavior actually
   exists in the application. A missing test or failed validation is not a
   reason to retain implemented behavior as `propose` or revert its status.
4. Run the relevant tests and standard SpecBox validation. Report test,
   validation, and status-conversion results on separate lines.

Do not change other proposals, the SpecBoxTMS platform, or unrelated user
changes.
