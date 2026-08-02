---
name: create
description: Use when initializing SpecBoxTMS in a new or existing project, or safely creating or amending its .tms.json configuration.
---

# Connecting SpecBoxTMS

## Read First

Before writing, inspect the explicit task source, project structure and stack,
existing specifications, `.tms.json`, tests, and their commands. Preserve
established conventions.

## Actions

1. Determine the project-compatible SpecBox command from manifests, scripts,
   lockfiles, and local documentation. Only then run the required `npx
   spec-box …` command; never guess its arguments.
2. If `.tms.json` is absent, add only the minimum confirmed configuration. If
   it exists, change only the necessary, understood addition; do not overwrite
   unknown keys or unrelated changes.
3. If the task conflicts with the configuration, the command is unclear, or
   the change is unsafe, do not write the file: report the discrepancy and ask
   the user to decide.
4. Do not create YAML requirements or metadata without a source in the task,
   code, or an explicit user decision.

## Scope and Result

Only write `.tms.json` when it can be safely created or amended precisely. Do
not change application code, tests, or specifications.

Report the discovered conventions and command, created or changed keys (or why
no write occurred), and the command result or blocker.
