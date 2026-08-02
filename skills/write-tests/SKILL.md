---
name: write-tests
description: Use when adding or updating tests for implemented SpecBoxTMS assert requirements in an existing project test stack.
---

# Writing Tests for Implemented Requirements

1. Select one `assert`. Read `.tms.json`, nearby tests, and project commands
   to understand the configured Jest or JUnit mapping.
2. Use the existing runner and its style; do not add a framework. First write
   a test that fails because the behavior is absent, then make the smallest
   implementation change and run the targeted test.
3. Link the test identifier to `assert` exactly as `.tms.json` configures it.
   Test observable behavior, not specification text or a mock.
4. Report test execution and `specbox:validate` separately.

Do not change a requirement's status because a test is missing or failing:
`assert` is implemented behavior and coverage is independent.
