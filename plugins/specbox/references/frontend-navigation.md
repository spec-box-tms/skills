# Navigation and Entry Requirements

Use this checklist when a feature lets a user enter a scenario, move to another
scenario, or return to a prior one.

## Establish

Determine the entry initiator, origin, destination, preserved context, and
functional route parameters. When history matters, determine the required Back
or forward behavior and the destination after a completed or cancelled flow.
When a transition can wait or fail, determine the user-visible state and
recovery action.

For unresolved product choices, ask whether the transition replaces the current
location, keeps it in history, opens a separate context, or returns to a named
origin. Offer only options that fit the existing application behavior.

## Quality criteria

Each transition identifies its trigger, the resulting destination or visible
context, and any data that must survive it. History behavior must be observable
and unambiguous when specified. A failed transition states what the user sees
and how they continue or retry.

## Standard groups

- `Entry` for supported ways to enter the feature.
- `Transitions` for movement to another feature or context.
- `Return and history` for return destinations and history behavior.
- `States` for user-visible transition states.
- `Error handling` for failed transitions and recovery.
