# Frontend E2E testing: design

- Status: approved
- Date: 2026-08-02

## Goal

Define frontend test guidance for accepted SpecBoxTMS requirements. Tests
express user-visible behavior and must not depend on components, classes,
composition, DOM structure, CSS, or backend contracts.

## Test model

Frontend coverage is E2E-first. A test starts from controlled data, performs
user actions, and checks an observable outcome. Use the existing E2E runner;
when the project has none, offer a choice and recommend Playwright without
installing it.

Each test covers one `assert` and uses the identifier configured by SpecBoxTMS.
A `propose` has no test. Shared login, data setup, and navigation helpers may
prepare a scenario, but the test itself owns its requirement-specific action
and assertion. Select UI elements by accessible role/name or the project's
established test contract.

## Requirement lifecycle

`specbox:apply` first accepts a `propose` by converting it to `assert`, then
writes and confirms a RED E2E test, implements the behavior, and confirms
GREEN. The workflow is then completed without writing a `completed` status to
YAML. A test added for existing behavior provides regression coverage and need
not be forced to fail. Test results never change requirement status
automatically.

## Controlled environment

Tests use the project's controlled test backend and fixtures, with no
dependence on external services or data left by another test. Data preparation
uses existing project test contracts only. The UI test does not inspect HTTP
requests, status codes, or backend models.

Wait for a user-visible result rather than sleeping, timing arbitrary network
delays, or masking failures with retries and larger timeouts. If the project
has no controlled backend or fixture mechanism, report that as a blocker and
propose adding one separately.

## Observable checks

The reference maps frontend behavior to E2E observations:

| Behavior | E2E observation |
| --- | --- |
| Navigation | Entry action, destination/context, preserved state, history, or specified transition failure. |
| Presentation | Visible data and specified loading, empty, stale, or error state. |
| Search, filtering, selection | User input and the resulting data, page, selection, or reset. |
| Forms and fields | Initial values, input, validation timing/message, dependencies, save, or cancellation. |
| Consequential actions and access | Preconditions, confirmation/cancellation, progress, result/recovery, availability, or restriction. |
| Accessible interaction | Keyboard action, focus placement/return, or meaningful announced state change. |

Only behavior stated in the selected requirement is asserted. The reference
does not test visual design or add unspecified product behavior.

## Skill integration

`specbox:write-tests` reads the frontend E2E reference before testing frontend
requirements. It preserves the project's runner and style, creates no new
framework, and reports E2E execution separately from SpecBoxTMS traceability
validation.
