# Form Field Requirements

Use this checklist for a field with independent behavior. Apply the same facts
to an inline field when they are relevant, without creating a separate feature.

## Establish

Determine the semantic value type, label, placeholder, explanatory text, input
behavior, and whether the user can change or clear the value. Determine every
established validation rule, when validation is evaluated, and the message or
other observable result of an invalid value.

When validation is not fully defined, offer validators relevant to the value
type instead of selecting them:

- text: required value, length, character set, or a format such as email or
  URL;
- numeric: integer or decimal format, range, precision, or step;
- date and time: allowed interval, past or future rule, or relation to another
  date;
- choice: allowed values or number of selected values;
- file: permitted type, size, or number of files;
- consent: whether an affirmative value is required.

For a field dependent on another field, determine the source condition and
link the dependent requirement to the source field. Do not add a backlink from
a field to its parent form.

## Quality criteria

The field's purpose and value semantics are understandable from its
requirements. Display text, input behavior, and validation outcome are
observable when specified. A validation rule identifies the value or condition
it evaluates and its user-visible result. Dependencies identify the source
field and do not rely on an implicit parent-form link.

## Standard groups

- `Presentation` for label, placeholder, and explanatory text.
- `Input` for value semantics and input behavior.
- `Validation` for validation rules, timing, and results.
- `Dependencies` for rules controlled by another field.
