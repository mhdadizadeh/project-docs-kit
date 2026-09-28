# Bootstrap

Status: Active

Last updated: 2026-09-28

This is the entrypoint an AI coding assistant reads before starting work in a project that follows this kit.

## How an agent gets here

Two paths lead to this file, and both are valid:

- **Automatic:** the project's `AGENTS.md` (which most current agent tools read at the start of a session without being asked) contains a section pointing at `project-knowledge/kit-reference.md` (see `templates/AGENTS.snippet.md`). A tool that reads `AGENTS.md` on its own reaches this bootstrap without any human needing to say anything.
- **Explicit:** the user directly asks the agent to continue the project following this kit (see `instructions/commands.md`, Command 2) — needed on a tool that does not auto-read `AGENTS.md`, or to force a re-read mid-session.

Either way, once here, follow the same sequence below.

## Required startup sequence

1. Read `project-knowledge/kit-reference.md` in the project — it names this kit's repository and the pinned version the project follows. If it does not exist, this project has not been set up yet; go to "First run" below.
2. Fetch this kit's instructions at that pinned version (clone or read directly) — do not assume an older reading of the instructions from earlier in the session still matches; if the pinned version changed, re-read.
3. Read [README.md](../README.md) to understand what this kit is and is not.
4. Read `project-knowledge/current.md` — the consolidated current state of the project.
5. Follow [instructions/logging-protocol.md](logging-protocol.md) during the session.

## First run (no `project-knowledge/` yet)

If the project has no `project-knowledge/kit-reference.md`, this kit has not been set up. Create `project-knowledge/` following the README's Install section, using this kit's current version as the pinned version. Reconstruct any existing understanding of the project from recent commits and existing documentation before writing the first `current.md`, rather than starting from nothing when prior context exists.

## Where this lives

This kit itself is never copied into the project. Only `project-knowledge/` (the project's own data), `kit-reference.md` (a pointer to this kit's repository and pinned version), and the small `AGENTS.md` section from `templates/AGENTS.snippet.md` are committed into the project's own git repository. Everything under `instructions/` and `templates/` stays here, in this kit's repository, read but never duplicated.

## Operating rule

Treat `project-knowledge/current.md` as the authoritative working state of the project — not chat history, not memory, not a previous session's assumptions. If something in the current session contradicts it, that is worth a knowledge event (see logging-protocol.md), not a silent overwrite.

## What this is not

This is not a request-confirmation gate. Read the current state, then do the work. Ask only when a request is genuinely ambiguous or a decision would be expensive to undo.

## Updates

Bootstrapping (step 1-2 above) reads the project's *pinned* version — it does not check whether a newer version exists. Checking for and applying a newer version only happens when the user explicitly asks for it, following [instructions/update-protocol.md](update-protocol.md). Do not run that protocol as part of ordinary bootstrap, and do not apply an update without the user's confirmation.

If `kit-reference.md`'s `Last checked` date is old (weeks, not days), it is reasonable to mention that once and offer to check — but proceed with the session on the pinned version either way unless the user asks to check now.
