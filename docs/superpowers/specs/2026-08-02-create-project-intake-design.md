# Project intake for `specbox:create`

`specbox:create` asks first: «Хотите подробно описать проект или стек
используемых технологий, уточнить правила кодирования требований?»

It accepts free-form project information. When that information leaves the
project name, short description, technology stack, or requirement-coding rules
unclear, it asks only the missing follow-up questions. It then creates missing
`.tms.json`, `.spec-box-meta.yml`, `specs/`, and an initial YAML specification.
The initial specification records the project description only; it contains no
`assert` or `propose` entries. Existing files and conventions are preserved.
