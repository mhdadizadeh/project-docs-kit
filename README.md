# Project Docs Kit

For a practical, human-facing walkthrough (add it to a project, use it day to day, check for and apply updates), see [USAGE.md](USAGE.md) — written in Persian for this team. This README is the technical reference; `instructions/*.md` are what an AI agent reads and follows.

A small, replaceable documentation layer for individual projects that are built with AI coding assistants (Claude Code, Codex, etc.) and that feed into a shared, central body of documentation.

This is not a software project template. It defines only:

- how a single project records its own knowledge and decisions,
- how a project surfaces findings worth promoting into the organization's central documentation.

It intentionally does not define source folders, build tooling, or coding conventions — those belong to the project itself.

## Relationship to the central documentation

Every project installing this kit is assumed to sit under one shared, central documentation system (for this team: the "Domain Expert" project documentation). This kit does not replace that central system. It is the local layer that:

1. lets a project record its own knowledge without waiting for a central review, and
2. sends the whole of `project-knowledge/current.md` to that central system on request.

There is no local curation step and no evidence-gated candidate table — the whole document goes, every time, and the central documentation's own review process decides how (or whether) any of it enters the aggregated documentation. Sending is never automatic. See [instructions/send-protocol.md](instructions/send-protocol.md).

## Structure this kit expects in a consumer project

```
AGENTS.md                # (or a section within it) points to project-knowledge/kit-reference.md
project-knowledge/
  kit-reference.md        # which kit repository and version this project follows, and the central docs repository
  current.md              # consolidated current state: goal, status, facts, tools, open questions
  events/                 # append-only, timestamped: what happened and why
```

`project-knowledge/` is local to the project and is never overwritten by an update to this kit.

## Alignment with AGENTS.md

[AGENTS.md](https://agents.md/) is the open, widely-adopted convention many coding-agent tools (Codex, Cursor, GitHub Copilot, and others) already read automatically at the start of a session, without needing to be told to. This kit does not compete with it or replace it — it plugs into it.

A project installing this kit adds a short, stable section to its own `AGENTS.md` (creating one if it doesn't exist yet, or appending to an existing one that already covers build/test/coding conventions) pointing at `project-knowledge/kit-reference.md`. See `templates/AGENTS.snippet.md` for the exact text.

This means: on any tool that already auto-reads `AGENTS.md`, this kit's bootstrap happens automatically, with no explicit "apply" command needed. The explicit commands in [instructions/commands.md](instructions/commands.md) remain as the fallback for tools that don't read `AGENTS.md` on their own, and as a way to force a re-read mid-session.

The snippet itself never changes as the kit's protocol evolves — it only points elsewhere — so adding it to a project's `AGENTS.md` is a one-time step, not something the update protocol needs to touch.

## This kit is static; projects only read it

This repository is the single, authoritative copy of the protocol. It is never copied, forked, or vendored into a consumer project. A project that duplicated it would drift from it the moment either side changed — ten projects would mean ten silently diverging copies of "the protocol." Instead, a consumer project keeps only:

1. its own `project-knowledge/` (its data — goal, facts, events), tracked in its own git repository, and
2. one small pointer file recording which version of this kit it follows.

An agent working in the project reads the pointer, fetches this kit's instructions from the pinned version (clone, fetch, or however the environment reaches this repo), follows them, and writes only into `project-knowledge/`. Nothing from `instructions/` or `templates/` is ever committed into the consumer project.

## Install

```bash
mkdir -p project-knowledge/events
```

Create `project-knowledge/kit-reference.md`:

```markdown
# Project Docs Kit reference

Kit repository: https://github.com/mhdadizadeh/project-docs-kit
Pinned version: 2026.09.28.5   # see this kit's OS_VERSION at that commit
Last checked: <date>            # last time an update check ran, applied or not
Last updated: <date>            # last time the pinned version actually changed

Central docs repository: <url, or "not set">   # where this project's knowledge is sent; see instructions/send-protocol.md
Last sent: <date, or "never">
```

Then create `project-knowledge/current.md` from this kit's `templates/project-knowledge/current.md` — either by fetching that template at the pinned version, or by hand, matching the structure `instructions/logging-protocol.md` defines.

Add the contents of `templates/AGENTS.snippet.md` to the project's `AGENTS.md` (create the file if the project has none; append as its own section if one already exists for other purposes — never overwrite existing content).

Commit `project-knowledge/` and `AGENTS.md` into the project's own repository, the same as any other project file.

Agent entrypoint at the start of any session: whichever tool the project uses either reads `AGENTS.md` automatically (most current tools do) and follows the pointer to `project-knowledge/kit-reference.md`, or is told explicitly to (see [instructions/commands.md](instructions/commands.md)). Either path leads to [instructions/bootstrap.md](instructions/bootstrap.md) at the pinned version.

## Documents

- [instructions/bootstrap.md](instructions/bootstrap.md) — what an agent reads before starting work in a project
- [instructions/logging-protocol.md](instructions/logging-protocol.md) — how to record events, current state, and facts with evidence
- [instructions/send-protocol.md](instructions/send-protocol.md) — how the whole of a project's current knowledge reaches the central documentation
- [instructions/update-protocol.md](instructions/update-protocol.md) — how a project checks for and applies a newer kit version
- [instructions/commands.md](instructions/commands.md) — canonical install / apply / update commands for giving to an agent directly, as plain text
- [templates/AGENTS.snippet.md](templates/AGENTS.snippet.md) — the section to add to a project's `AGENTS.md` so AGENTS.md-aware tools bootstrap this kit automatically

## Version and updates

Current kit version: see [OS_VERSION](OS_VERSION). Every version bump is explained in [CHANGELOG.md](CHANGELOG.md) — what changed and why, not just a number.

Because the kit is never vendored, updating touches exactly `project-knowledge/kit-reference.md` in the consumer project (the pinned version and the update timestamp), committed as an ordinary change. `project-knowledge/current.md` and `events/` are never touched by a kit update.

An update is never automatic. From inside any project, ask an agent to check for or apply a kit update (any clear phrasing works) and it follows [instructions/update-protocol.md](instructions/update-protocol.md): fetch the current `OS_VERSION` and `CHANGELOG.md` from this repository, show what changed since the pinned version, and apply it only on explicit confirmation.
