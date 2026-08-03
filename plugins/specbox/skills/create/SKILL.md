---
name: create
description: Use when initializing SpecBoxTMS in a new or existing project, or safely creating or amending its .tms.json configuration.
---

# Connecting SpecBoxTMS

## Start the Intake

First extract project context from the user's request and the repository. Use
the user's language and ask only for missing information that materially affects
initialization; never repeat a question already answered by the request or
project. Project name, description, stack, and requirement-coding rules may be
derived from existing files when unambiguous.

If organization is unspecified, offer a flat specification layout or a
hierarchy. Use the minimal flat layout when the user leaves the choice to you.
For a hierarchy, ask only for its title and grouping attributes.

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

1. `.tms.json` with only the minimum confirmed configuration. If no project
   configuration convention exists, point its YAML files at `specs/**/*.yml`.
   Add test mappings only when confirmed. Never overwrite unknown keys or
   unrelated changes in an existing file.
2. `.spec-box-meta.yml`. For a flat layout, create only the minimum required
   metadata and include neither `attributes` nor `trees`. Create those keys
   only after the user selects a hierarchy; then define the selected grouping
   `attributes` and a corresponding `trees` entry in this file. Do not create
   a separate tree file. Put hierarchy attributes and tree definitions
   exclusively in `.spec-box-meta.yml`.
3. `specs/`. If no existing convention names a specification directory, use
   `specs/` exactly; do not create `requirements/` or another directory.
4. The first YAML specification inside `specs/`, not metadata or taxonomy. It
   may contain only the feature identity required by the format and the
   collected project description. Never add `assert`, `propose`, requirement
   groups, attributes, or trees.

If a required format or command cannot be confirmed, do not guess or overwrite
anything: report the discrepancy and ask the user to decide.

## Result

Report the discovered conventions and command; the missing artifacts created
or existing artifacts preserved; and confirmation that the initial
specification contains only the feature identity and project description, with
no `assert`, `propose`, requirement groups, attributes, or trees.
