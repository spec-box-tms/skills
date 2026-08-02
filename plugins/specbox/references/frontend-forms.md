# Form Requirements

Use this checklist when a feature collects or changes user data as one coherent
submission flow.

## Establish

Determine the form purpose, supported modes such as create or edit, and the
fields it contains. A simple field without independent behavior may be
described inline. A field with its own validation, conditional visibility or
availability, dependency, asynchronous check, or value transformation gets a
separate feature. The form requirement links to every separate field feature.

Determine initial values, how the user saves or cancels, and the observable
result of either choice. When saving can wait or fail, determine the applicable
state, error, and recovery behavior. For unresolved choices, ask focused
questions and offer options grounded in existing project conventions.

## Quality criteria

The feature makes its purpose and modes observable. Each field is either
described inline or linked as a separate feature. Save and cancel requirements
state their initiator, resulting data or destination when relevant, and
observable outcome. Do not assume automatic saving, discard behavior, or a
confirmation when it is not established.

## Standard groups

- `Composition` for the form purpose and included fields.
- `Initialization` for supported modes and initial values.
- `Save` for submission and successful persistence.
- `Cancel` for cancellation and its result.
- `States` for applicable form and save states.
- `Error handling` for submission failures and recovery.
