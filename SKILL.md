---
name: new-project-harness
description: >-
  Bootstrap a new or existing software project for reliable coding-agent work. Use when starting
  a project, creating or improving its agent instructions or continuity files, or when asked to
  set up AGENTS.md, feature-list.json, init.sh, progress.md, or session-handoff.md. Inspects the
  repository, asks about important unknown requirements or architecture choices, then adapts the
  bundled Walking Labs harness templates without overwriting user work.
license: MIT
---

# New Project Harness

Create a small, project-specific agent harness. Use the bundled files in `templates/` as the
starting point for these five root-level files:

- `AGENTS.md` (template: `templates/agents.md`)
- `feature-list.json`
- `init.sh`
- `progress.md`
- `session-handoff.md`

The templates are based on the MIT-licensed [Walking Labs harness-creator templates](https://github.com/walkinglabs/learn-harness-engineering/tree/main/skills/harness-creator/templates).
Keep the five harness concerns coherent: instructions, current state, verification, scope, and
session continuity.

## Workflow

1. **Inspect before editing.** Confirm the repository root. Read existing `AGENTS.md` files,
   README and project/product/architecture docs, manifests and lockfiles, CI workflows, tests,
   and existing setup/verification scripts. Check git status and whether this is already a Git
   repository. Prefer Git for project change tracking: if this is a new project without Git, run
   `git init` unless the user or project policy says not to. Never reinitialize an existing repo.
   Use evidence from the repository; do not infer that a blank or incomplete project has a
   particular product design.
2. **Protect existing work.** If any target file exists, read it and preserve useful content.
   Never replace or truncate an existing file. Add missing guidance or merge only after explaining
   the proposed change. Ask before making a change that would remove or materially rewrite existing
   instructions/state. Keep unrelated uncommitted edits intact.
3. **Resolve key unknowns.** Ask concise questions when an answer affects product requirements,
   architecture, platform/runtime, data/security boundaries, or what counts as done. Offer a small
   set of viable choices where useful. Do not ask questions that repository evidence can answer.
   If the user asks to proceed without answers, make conservative choices, label assumptions in
   the artifacts, and leave unresolved decisions as explicit questions. Never present an agent
   preference as a user decision.
4. **Adapt the templates.** Replace placeholders with facts and runnable commands found in the
   repository. Tailor startup steps, verification gates, project purpose, and feature entries.
   Keep `AGENTS.md` short and actionable. For a truly blank project, use useful placeholders and
   ask the user to confirm the product scope; do not invent a roadmap and call it agreed scope.
5. **Record these user preferences in every applicable `AGENTS.md`:**
   - Use `mise` to manage language runtimes and project tools when it is applicable and available
     or appropriate for the project. Respect an existing toolchain if the project documents a
     different required manager; ask before changing an established toolchain. Do not create a
     `mise.toml` without a project need or user agreement.
   - Write user-facing prose in **ASD-STE100 Simplified Technical English** by default, unless the
     user specifically asks for the agent's opinion. In that case, give the requested opinion
     clearly as an opinion, not as fact. Keep code identifiers and necessary technical terms intact.
6. **Create/update the five files.** Use `feature-list.json` as valid JSON. Give each feature a
   unique ID, clear observable outcome, dependencies where needed, a status, and verification
   evidence. Keep only one feature in progress. Keep evidence empty until checks have actually
   passed. In `init.sh`, use the repository's real install and verification commands; prefer
   lockfile-respecting/frozen installs, include only checks that exist, and fail clearly if required
   tools are absent. Do not make initialization destructive or silently start a long-running server.
   Make it executable (`chmod +x init.sh`). Do not add dependencies or alter toolchain config just
   to make the harness look complete. If this is a new project and not yet a Git repository, use
   `git init` as described above, then track the harness files.
7. **Validate.** Parse `feature-list.json`; run `bash -n init.sh`; inspect the diff and verify that
   commands and paths exist. Do not run dependency installation, migrations, or other side-effecting
   initialization unless the user asks or confirms. If safe and useful, run only non-destructive
   checks. Do not claim tests passed if they were not run.
8. **Track and commit.** Keep project changes in Git. After applicable tests and verification
   pass, prefer committing the changes with a clear, scoped message. Stage only files for this
   task; do not include unrelated user changes. Do not commit if checks fail, were not run, or the
   work is incomplete. Report the checks and commit outcome. If no tests or checks exist, do not
   claim they passed; explain this and ask before making a commit based only on other validation.
9. **Handoff.** Summarize files created or updated, assumptions and questions, validation run, and
   the next action. Explain that the user should replace any explicitly marked feature placeholders.

## Project-specific adaptation

- Detect the actual stack from manifests and lockfiles. Use the existing package manager/runtime
  and CI commands; do not assume Node.js or copy example commands that do not apply.
- If project goals or architecture are unclear, ask before encoding them. Separate confirmed
  requirements, inferred facts, and open choices in `AGENTS.md` or `progress.md`.
- Keep the feature list focused on independently verifiable user-visible behavior. Avoid generic
  filler features such as "documentation" or "cleanup" unless they are real project requirements.
- `init.sh` is the reproducible startup/verification entry point, not a place for hidden changes.
  State clearly if it needs network access, credentials, services, or user confirmation.
- Update `progress.md` and `session-handoff.md` with the actual initial state and next step. Do not
  imply implementation work has started when only the harness was created.
- If the repo uses a different instruction-file convention, ask whether to create `AGENTS.md`, use
  the established file, or maintain both. The requested default is `AGENTS.md`.

## Template references

Read the needed template before creating each file. Preserve its useful structure while adapting it:

- `templates/agents.md`
- `templates/feature-list.json`
- `templates/init.sh`
- `templates/progress.md`
- `templates/session-handoff.md`
