---
name: create
description: Use when initializing SpecBoxTMS in a new or existing project, or safely creating or amending its .tms.json configuration.
---

# Connecting SpecBoxTMS

## Start the Intake

Open with exactly:

> Хотите подробно описать проект или стек используемых технологий, уточнить правила кодирования требований?

Accept free-form project information. Ask follow-up questions only when the
project name, project description, technology stack, or requirement-coding
rules are missing. Do not ask for information already supplied.

Offer a flat specification layout or a hierarchy. If the user chooses a
hierarchy, ask for its title and grouping attributes; these are the only
additional questions permitted for that choice.

## Read First

Before writing, inspect the explicit task source, project structure and stack,
existing specifications, `.tms.json`, `.spec-box-meta.yml`, tests, their
commands, and local SpecBox documentation. Preserve established conventions
and existing artifacts.

Determine the project-compatible SpecBox command from manifests, scripts,
lockfiles, and local documentation. Only then run the required `npx spec-box
…` command; never guess its arguments.

## Initialize Missing Artifacts

Create each missing artifact using the discovered project conventions and the
installed SpecBox format:

1. `.tms.json` with only the minimum confirmed configuration. Never overwrite
   unknown keys or unrelated changes in an existing file.
2. `.spec-box-meta.yml`. For a flat layout, create only the minimum required
   metadata. For a hierarchy, define the selected grouping `attributes` and a
   corresponding `trees` entry in this file; do not create a separate tree
   file.
3. `specs/`.
4. The first YAML specification in `specs/`, containing only the project
   description. Do not add `assert` or `propose` entries.

If a required format or command cannot be confirmed, do not guess or overwrite
anything: report the discrepancy and ask the user to decide.

## Result

Report the discovered conventions and command; the missing artifacts created
or existing artifacts preserved; and confirmation that the initial
specification contains only the project description with no `assert` or
`propose` entries.
