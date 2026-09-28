# Bootstrap

Status: Active

Last updated: 2026-09-28

This is the entrypoint an AI coding assistant reads before starting work in a project that has this kit installed.

## Required startup sequence

1. Read [README.md](../README.md) to understand what this kit is and is not.
2. Read `project-knowledge/current.md` — the consolidated current state of the project.
3. Read `project-knowledge/agents/current.md` — who owns which task right now, and whether the task you are about to touch already has an owner.
4. If `agents/current.md` points at a recent handoff, read that handoff file under `project-knowledge/agents/handoffs/`.
5. If none of the above exists yet (first run in this project), read recent commits and any existing project documentation to reconstruct the current state, then create `project-knowledge/current.md` and `project-knowledge/agents/current.md` from the templates in `templates/`.
6. Follow [instructions/logging-protocol.md](logging-protocol.md) and [instructions/agent-coordination.md](agent-coordination.md) during the session.

## Where this lives

This kit and `project-knowledge/` are vendored into the project's own git repository as plain files (see README's Install section) — not a nested git clone, not a separate detached store. Both are tracked, diffed, and reviewed the same way as any other part of the project.

## Operating rule

Treat `project-knowledge/current.md` as the authoritative working state of the project — not chat history, not memory, not a previous session's assumptions. If something in the current session contradicts it, that is worth a knowledge event (see logging-protocol.md), not a silent overwrite.

## What this is not

This is not a request-confirmation gate. Read the current state, then do the work. Ask only when a request is genuinely ambiguous or a decision would be expensive to undo.

## Version check

Read [OS_VERSION](../OS_VERSION) at the start of a session. If it differs from the version last loaded, treat this as a fresh kit load and re-read the instruction files before relying on them.
