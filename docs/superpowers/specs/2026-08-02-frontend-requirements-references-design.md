# Frontend requirements references: design

- Status: approved
- Date: 2026-08-02

## Goal

Create a main frontend reference and narrow, reusable reference documents for
writing, extracting, and reviewing functional UI requirements in SpecBoxTMS.
The references define what facts must be established and what quality criteria
the resulting requirements must meet. They do not prescribe visual design,
application-internal data models, components, or implementation details.

## Reference structure

The main frontend reference selects the applicable checklist documents for a
feature and contains cross-cutting rules. The checklist documents cover:

1. Navigation and entry.
2. Data presentation.
3. Selection, search, and filtering.
4. Forms.
5. Form fields.
6. Consequential actions.
7. Access and feature availability.
8. Accessible interaction.

The set is intentionally narrow. A feature uses only the checklist documents
whose behavior it contains.

## Feature boundaries and sources

A frontend feature can represent a screen, a standalone UI element, or a
complete user scenario, according to the user's intent. When a request
contains independent units of behavior, the agent proposes splitting it into
related features.

The agent first studies the request, existing specifications, code, and tests.
It asks the user only for facts that cannot be established from those sources.
Requirements never record the absence of behavior or make assumptions beyond
the request and evidence.

## Skill-specific use

- `specbox:extract` creates only evidenced `assert` entries from code, tests,
  and existing specifications.
- `specbox:propose` uses the checklists to find missing product decisions and
  offers options before creating `propose` entries.
- `specbox:review` is read-only. For each gap it identifies the feature and
  criterion, gives the exact unanswered question, and offers concise options
  when they are apparent.

## Checklist contents

Each checklist document contains:

- its applicability;
- facts to establish and record in requirements;
- questions and typical options for unresolved facts;
- quality criteria;
- its standard `specs-unit` groups;
- traceability rules.

The documents do not contain YAML templates or canonical requirement wording.

## Standard groups

Each checklist defines its own vocabulary. A feature creates a group only when
it has requirements for that group.

| Checklist | Standard groups |
| --- | --- |
| Navigation and entry | Entry, Transitions, Return and history, States, Error handling |
| Data presentation | Presentation, Data refresh, States, Error handling |
| Selection, search, and filtering | Search, Filtering, Sorting, Pagination, Selection, Reset conditions, States, Error handling |
| Forms | Composition, Initialization, Save, Cancel, States, Error handling |
| Form fields | Presentation, Input, Validation, Dependencies |
| Consequential actions | Initiation, Confirmation, Execution, Result, Error handling |
| Access and feature availability | Availability, Restrictions |
| Accessible interaction | Keyboard control, Focus, State announcements |

For a behavior that does not fit a standard checklist, the agent may propose
new meaningful groups without creating a new checklist document by default.

## Form and field requirements

A simple field without independent behavior may be described inline in the
form feature. A field gets its own feature when it has independent behavior,
such as validation, conditional visibility or availability, a dependency on
another field, an asynchronous check, or value transformation.

The form feature links to every separate field feature, for example by stating
that it contains that field and linking `$<field-code>`. A field does not link
back to its parent form. A dependent field links to the field on which its rule
depends.

The form-field checklist records the label, placeholder, explanatory text,
input behavior, validation, and dependencies. When validation is not fully
defined, the agent offers validators that match the semantic value type, such
as text format or length, numeric range or precision, date/time constraints,
allowed selections, file type or size, and explicit consent. The user decides
which rules apply; the agent does not add validators by assumption.

## States, errors, and API links

Loading, empty, error, progress, and completion behavior remains in the
feature where it occurs. The main frontend reference gives the shared quality
criteria; the relevant checklist places the requirements in its own State or
Error handling group.

Frontend requirements do not reproduce internal data models. If the project
is a monorepo and contains backend specifications, a frontend feature links to
the API features it uses once in its Markdown `description`. No link is
invented for external APIs or unavailable backend specifications.
