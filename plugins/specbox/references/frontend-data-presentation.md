# Data Presentation Requirements

Use this checklist when a feature shows application data to the user.

## Establish

Determine which information is available, the conditions under which it is
shown, the functional grouping or ordering users rely on, and when the data is
refreshed. Do not prescribe cards, tables, trees, tabs, or other visual
components unless the user requests that presentation explicitly.

When the information is delayed, absent, stale, or cannot be retrieved,
determine the relevant state, message, and recovery behavior. For unresolved
choices, offer the existing project convention or the smallest relevant options
such as manual refresh or automatic refresh at a defined event.

## Quality criteria

Requirements state the information a user can observe, the condition that makes
it available, and any meaningful grouping, ordering, or refresh trigger. State
and failure behavior is attached to this feature rather than a separate one.

## Standard groups

- `Presentation` for visible information and functional organization.
- `Data refresh` for refresh triggers and resulting updates.
- `States` for loading, empty, stale, or other applicable presentation states.
- `Error handling` for retrieval failures and recovery.
