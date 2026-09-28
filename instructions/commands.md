# Agent Commands

Status: Active

Last updated: 2026-09-28

Defines three canonical commands a project owner can give an agent, in any project, in either English or Persian. An agent should recognize the intent regardless of exact wording and map it to the matching protocol — do not require the user to phrase it exactly as shown below.

| # | Intent | Example phrasing (English) | Example phrasing (Persian) | Protocol to run |
| --- | --- | --- | --- | --- |
| 1 | Install the kit into this project | "Install project-docs-kit from `<repo-url>` into this project" | "کیت مستندسازی را از `<آدرس مخزن>` روی این پروژه نصب کن" | README.md § Install |
| 2 | Start/continue this session following the kit | "Continue this project following project-docs-kit" / "Bootstrap from project-docs-kit" | "طبق project-docs-kit روی این پروژه ادامه بده" / "کیت مستندسازی را روی این پروژه اعمال کن" | instructions/bootstrap.md |
| 3 | Check for and apply a kit update | "Check project-docs-kit for an update" / "Update project-docs-kit, apply if there's a new version" | "ببین کیت مستندسازی آپدیت دارد یا نه" / "کیت را آپدیت کن" | instructions/update-protocol.md |

## Command 1 — Install

Requires the kit's repository URL (there is nothing in the project yet to read it from). Optionally a specific version; default to the kit's current `OS_VERSION` at the given repository if none is stated.

On this command, an agent must:

1. Confirm `project-knowledge/kit-reference.md` does not already exist. If it does, this is not a fresh install — stop and ask whether the user means Command 3 (update) instead, or genuinely wants to replace the existing setup.
2. Follow README.md's Install section exactly: create `project-knowledge/{events,agents/handoffs}`, write `kit-reference.md` with the given (or default) repository URL and version, copy the two templates, fill `current.md`'s Goal and Current status from whatever the agent can learn about the project (ask if it cannot), and commit.
3. Report back the pinned version and that the project now follows the kit.

## Command 2 — Bootstrap / apply

This is the normal per-session startup, not a special action — see instructions/bootstrap.md. It is listed here because a user may explicitly ask for it (e.g. after an agent skipped it and went straight to code), in which case run the required startup sequence now rather than treating it as already done.

## Command 3 — Check / apply update

See instructions/update-protocol.md. Never skip straight to applying — always show what changed (from CHANGELOG.md) and wait for explicit confirmation, even when the user's phrasing sounded like "just update it."

## Wiring these into a specific agent tool

Where the agent tool supports reusable custom commands (for example, Claude Code's command files), a thin command file that just states the intent and points at this file is enough — it should not duplicate the protocol steps, only trigger them. See `templates/agent-commands/` for ready-made examples for Claude Code. Verify the exact command-file format against that tool's current documentation before relying on it; tool-specific conventions change independently of this kit.
