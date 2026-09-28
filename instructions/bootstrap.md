# Bootstrap

Status: Active

Last updated: 2026-09-28

This is the entrypoint an AI coding assistant reads before starting work in a project that follows this kit.

## Required startup sequence

1. Read `project-knowledge/kit-reference.md` in the project — it names this kit's repository and the pinned version the project follows. If it does not exist, this project has not been set up yet; go to "First run" below.
2. Fetch this kit's instructions at that pinned version (clone or read directly) — do not assume an older reading of the instructions from earlier in the session still matches; if the pinned version changed, re-read.
3. Read [README.md](../README.md) to understand what this kit is and is not.
4. Read `project-knowledge/current.md` — the consolidated current state of the project.
5. Read `project-knowledge/agents/current.md` — who owns which task right now, and whether the task you are about to touch already has an owner.
6. If `agents/current.md` points at a recent handoff, read that handoff file under `project-knowledge/agents/handoffs/`.
7. Follow [instructions/logging-protocol.md](logging-protocol.md) and [instructions/agent-coordination.md](agent-coordination.md) during the session.

## First run (no `project-knowledge/` yet)

If the project has no `project-knowledge/kit-reference.md`, this kit has not been set up. Create `project-knowledge/` following the README's Install section, using this kit's current version as the pinned version. Reconstruct any existing understanding of the project from recent commits and existing documentation before writing the first `current.md`, rather than starting from nothing when prior context exists.

## Where this lives

This kit itself is never copied into the project. Only `project-knowledge/` (the project's own data) and `kit-reference.md` (a one-line pointer to this kit's repository and pinned version) are committed into the project's own git repository. Everything under `instructions/` and `templates/` stays here, in this kit's repository, read but never duplicated.

## Operating rule

Treat `project-knowledge/current.md` as the authoritative working state of the project — not chat history, not memory, not a previous session's assumptions. If something in the current session contradicts it, that is worth a knowledge event (see logging-protocol.md), not a silent overwrite.

## What this is not

This is not a request-confirmation gate. Read the current state, then do the work. Ask only when a request is genuinely ambiguous or a decision would be expensive to undo.

## Version check

Read [OS_VERSION](../OS_VERSION) at the start of a session. If it differs from the version last loaded, treat this as a fresh kit load and re-read the instruction files before relying on them.
