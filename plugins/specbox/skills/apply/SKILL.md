---
name: apply
description: Use when accepting and implementing a selected SpecBoxTMS propose requirement.
---

# Applying a Proposal

1. Select the exact `propose`; before editing, read the requirement, affected
   code, all its callers, existing tests, and YAML conventions.
2. Accept it by converting only that entry to `assert`. Do not create a
   separate completion status.
3. **REQUIRED SUB-SKILL:** Use `specbox:write-tests` to add the traceable test
   first and run it. Continue only after confirming that it fails because the
   stated behavior is absent (RED), not because of a setup or syntax error.
4. Implement only the stated behavior with the smallest change, then run the
   targeted test until it passes (GREEN). Do not revert the accepted `assert`
   because a test or validation command fails; report the incomplete workflow.
5. Run standard SpecBox validation via `specbox:validate`. Report the status
   conversion, RED result, implementation, GREEN result, and validation
   separately. The workflow is completed only after GREEN; `completed` is not
   written to YAML.

Do not change other proposals, the SpecBoxTMS platform, or unrelated user
changes.
