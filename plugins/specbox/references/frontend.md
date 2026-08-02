# Frontend Functional Requirements

Use this reference for frontend behavior. It applies to requirements for a
screen, a standalone UI element, or a complete user scenario. Do not use it
to prescribe visual design, application-internal models, components, or
implementation technology.

## Select features and checklists

First inspect the request, existing specifications, code, and tests. Reuse
facts established there and ask the user only for missing facts that are needed
to describe the requested behavior. Do not record an absent behavior as a
requirement and do not infer it from silence.

When a request contains independent units of behavior, propose separate,
linked features. A feature may use more than one checklist; read only the
documents matching its behavior:

- `frontend-navigation.md` for entry and transitions;
- `frontend-data-presentation.md` for showing data;
- `frontend-selection-filtering.md` for search, filters, sorting, pages, or
  selection;
- `frontend-forms.md` for form behavior;
- `frontend-form-fields.md` for fields with independent behavior;
- `frontend-actions.md` for actions with observable consequences;
- `frontend-access.md` for access and feature availability;
- `frontend-accessible-interaction.md` for keyboard, focus, and dynamic-state
  announcements.

For a behavior outside these checklists, propose meaningful `specs-unit` group
names before writing requirements. Do not create a new reference document by
default.

## Apply this reference by skill

- `specbox:extract` creates `assert` only for behavior evidenced by code,
  tests, or existing specifications. Leave unsupported behavior unresolved.
- `specbox:propose` identifies missing product decisions with the applicable
  checklists, asks focused questions, and offers concise options before writing
  `propose`.
- `specbox:review` is read-only. For each missing or ambiguous fact, report the
  feature, violated quality criterion, the exact question to resolve, and
  concise options when apparent.

## Common quality criteria

Each entry describes an observable user-facing outcome and is complete,
correct, feasible, necessary, unambiguous, and verifiable. A selected feature
set must be consistent, modifiable, and traceable. Use existing priority
mechanisms only when the project already provides one.

Create a standard `specs-unit` group only when the feature has requirements in
that group. Requirements for loading, empty, error, progress, and completion
remain in the feature where that behavior occurs. Use the relevant checklist's
`States` or `Error handling` group rather than creating a standalone state or
error feature.

## Links

Do not duplicate frontend data models. If the project is a monorepo and has
backend specifications, list the API features used by a frontend feature once
in its Markdown `description`. Do not invent links for external APIs or for
backend specifications that are not present.

A form feature links to each separate field feature in a requirement that says
the form contains the field. A field does not link back to its parent form. A
field whose rule depends on another field links to the source field in the
dependent requirement.
