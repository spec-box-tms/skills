# Access and Feature Availability Requirements

Use this checklist when a user's role, authorization, account state, or other
condition controls whether a feature is available.

## Establish

Determine the condition that grants or restricts access and the functions it
affects. When a restriction has observable UI behavior, determine whether the
user sees the function, can attempt it, and receives an explanation or another
result. Offer existing project conventions first when those product decisions
are unresolved.

## Quality criteria

Availability requirements identify the actor or condition and the accessible
function. Restriction requirements identify the restricted function and its
observable behavior. Do not treat a hidden control, disabled control, or a
denied attempt as interchangeable without a stated requirement.

## Standard groups

- `Availability` for conditions under which a function is available.
- `Restrictions` for behavior when a function is unavailable or denied.
