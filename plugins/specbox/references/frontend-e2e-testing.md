# Frontend E2E Testing

## Test boundary

Test one user scenario: user actions and their observable results. Locate UI by
accessible role and name, or by an existing project test contract such as a
`data-test-id` attribute. Do not assert
components, DOM structure, CSS, internal calls, HTTP contracts, or backend
models. Assert only behavior stated in the selected requirement; do not test
visual design or invent product behavior.

## Runner and controlled state

Use the existing E2E runner. If none exists, offer a choice and recommend
Playwright without installing it. Run against the project's
controlled backend and fixtures; if either is absent, report that blocker rather
than adding an ad-hoc replacement.

## Requirement traceability

Write one test for each selected frontend `assert`. A `propose` has no test;
convert it to `assert` when accepting it for implementation. Configure the test
identifier through `.tms.json`. Shared setup may prepare the scenario, but it
may not own the requirement's assertion.

## Observable checks

- Navigation: the user reaches the expected visible destination or context.
- Presentation: the user sees the required information or state.
- Selection/filtering: the selected, searched, filtered, sorted, or paged result
  is visible.
- Forms/fields: entered values, validation, save, cancel, and resulting state
  are observable.
- Actions/access: allowed actions produce their result; restricted functions
  have the specified user-visible behavior.
- Accessible interaction: keyboard actions, focus changes, and announcements
  have their specified observable outcome.

## Stability

Do not use a sleep, arbitrary network waits, retries that mask flakes, or data
created by another test. Each test controls its required state through the
project fixtures and waits only for its observable user-visible result.

## Requirement lifecycle

A newly accepted `assert` test is RED before its behavior is implemented and
GREEN before the workflow is completed. A test added for existing behavior is
regression coverage and need not be forced to fail. Test status never changes a
requirement status automatically, and `completed` is not written to YAML.
