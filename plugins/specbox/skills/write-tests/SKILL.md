---
name: write-tests
description: Use when adding or updating tests for SpecBoxTMS assert requirements in an existing project test stack.
---

# Writing Tests for Accepted Requirements

1. Select one `assert`. Read `.tms.json`, nearby tests, project commands, and
   the frontend E2E reference when the requirement is frontend:
   `{SKILL_DIR}/../../references/frontend-e2e-testing.md`.
2. Use the existing runner and its style. For frontend work, follow the
   reference; do not add a framework or implementation code in this skill.
3. Link the test identifier exactly as `.tms.json` configures it and run the
   targeted test. For an `assert` newly accepted from `propose`, verify that it
   fails because behavior is absent (RED). For existing behavior, add regression
   coverage and report whether the test passes; do not manufacture a failure.
4. Report test execution and `specbox:validate` separately. Do not change
   requirement status or implement application behavior in this skill.
