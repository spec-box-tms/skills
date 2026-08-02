# Consequential Action Requirements

Use this checklist when a user action creates, changes, removes, submits, or
otherwise produces an observable consequence.

## Establish

Determine the action initiator, preconditions, affected target, and scope. For
an action on selected data, establish the selection scope through
`frontend-selection-filtering.md` and describe the action here. Determine
whether a confirmation, cancellation path, progress state, or recovery is
required only when supported by the request or existing behavior.

Determine the observable result, including changed data, resulting navigation
when relevant, and failure behavior. For unresolved decisions, offer the
smallest relevant options, such as immediate execution or explicit
confirmation, while retaining existing project conventions where present.

## Quality criteria

Each action identifies its user initiator, preconditions, target scope, and
observable outcome. A confirmation identifies the consequence it confirms and
the outcome of cancellation. Execution and recovery behavior is verifiable
when an action is delayed or fails. Do not assume that an action is reversible
or irreversible.

## Standard groups

- `Initiation` for triggers, preconditions, and targets.
- `Confirmation` for confirmation and cancellation behavior.
- `Execution` for progress and delayed execution.
- `Result` for successful observable outcomes.
- `Error handling` for failures and recovery.
