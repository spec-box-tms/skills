# SpecBox Create Project Intake Implementation Plan
> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.
**Goal:** Make `specbox:create` collect project context and initialize the minimum SpecBox artifacts.
**Architecture:** Update the one create-skill workflow. It requests free-form project information or the technology stack and coding rules, asks only for missing essentials, offers flat or hierarchical requirement organization, then creates missing configuration, metadata, `specs/`, and a description-only starter specification.
**Tech Stack:** Markdown skill instructions and standard shell validation.
## Global Constraints
- Preserve existing project files and conventions.
- Do not add `assert` or `propose` to the starter specification.
- Do not add scripts or dependencies.
- Create `trees` and supporting attributes only when the user selects a hierarchy.
---
### Task 1: Update and validate the create workflow
**Files:**
- Modify: `plugins/specbox/skills/create/SKILL.md`
- Test: a fresh-agent project-initialization scenario and YAML/frontmatter parsing
**Interfaces:**
- Consumes: free-form project description, `.tms.json`, `.spec-box-meta.yml`, and existing conventions.
- Produces: instructions to create missing `.tms.json`, `.spec-box-meta.yml`, `specs/`, and a description-only initial specification.
- [x] **Step 1: Run a baseline scenario without the revised instructions**
Ask a fresh agent how it would initialize SpecBox after receiving only a project description. Record whether it invents requirements or omits metadata and the initial specification.
- [x] **Step 2: Update the skill**
Require this opening prompt: `Хотите подробно описать проект или стек используемых технологий, уточнить правила кодирования требований?`
Require follow-up questions only for missing project name, description, stack, or requirement-coding rules. Offer flat or hierarchical organization; for a hierarchy, collect its title and grouping attributes and define `.spec-box-meta.yml` `attributes` and `trees`. Require creation of absent `.tms.json`, `.spec-box-meta.yml`, `specs/`, and a first specification containing only the project description.
- [x] **Step 3: Run the same scenario with the revised skill**
Verify that the agent collects missing context, preserves existing artifacts, and creates no `assert` or `propose` entries.
- [x] **Step 4: Validate the skill file**
Run: `node -e "const fs=require('fs'); const s=fs.readFileSync('plugins/specbox/skills/create/SKILL.md','utf8'); if (!/^---\\nname: create\\ndescription: Use when/.test(s) || !s.includes('.spec-box-meta.yml') || !s.includes('specs/')) process.exit(1)"`
Expected: exit code 0.
- [x] **Step 5: Commit**
Run: `git add plugins/specbox/skills/create/SKILL.md docs/superpowers/plans/2026-08-02-create-project-intake.md && git commit -m "feat: initialize SpecBox project artifacts"`
