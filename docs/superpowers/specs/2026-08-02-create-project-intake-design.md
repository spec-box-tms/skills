# Project intake for `specbox:create`

`specbox:create` first extracts project context from the request and repository,
then asks only for information that materially affects initialization. It uses
the user's language and never repeats a question already answered by the request
or project.

If organization is unspecified, it offers a flat specification layout or a
hierarchy grouped by project-defined attributes. It uses the minimal flat layout
when the user delegates the choice. For a hierarchy, it asks for its name and
grouping attributes, then defines them and a `trees` entry in
`.spec-box-meta.yml`.

It creates missing `.tms.json`, `.spec-box-meta.yml`, `specs/`, and an initial
YAML specification. The initial specification records the project description
only; it contains no `assert` or `propose` entries. Existing files and
conventions are preserved.
