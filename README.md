# Project Docs Kit

For a practical, human-facing walkthrough (add it to a project, use it day to day, check for and apply updates), see [USAGE.md](USAGE.md) — written in Persian for this team. This README is the technical reference; `instructions/*.md` are what an AI agent reads and follows.

A small, replaceable documentation-and-coordination layer for individual projects that are built with AI coding assistants (Claude Code, Codex, etc.) and that feed into a shared, central body of documentation.

This is not a software project template. It defines only:

- how a single project records its own knowledge and decisions,
- how multiple agents (or people) working the same project stay coordinated across sessions,
- how a project surfaces findings worth promoting into the organization's central documentation.

It intentionally does not define source folders, build tooling, or coding conventions — those belong to the project itself.

## Relationship to the central documentation

Every project installing this kit is assumed to sit under one shared, central documentation system (for this team: the "Domain Expert" project documentation). This kit does not replace that central system. It is the local layer that:

1. lets a project record its own knowledge without waiting for a central review, and
2. produces a small, explicit set of **promotion candidates** — findings, decisions, or tool evaluations that the project owner believes are worth the central documentation's attention.

Promotion into the central docs is never automatic. See [instructions/promotion-protocol.md](instructions/promotion-protocol.md).

## What this kit deliberately does not do

- It does not require a two-stage confirm-before-acting protocol on every request. Agents ask when a request is genuinely ambiguous or a decision is expensive to undo; otherwise they proceed and say what they did.
- It does not mandate a documentation language. Write in whichever language the project team actually works in. (This team works in Persian; nothing here requires English.)
- It does not require the whole knowledge base to be re-read on every turn. It requires reading the **current state**, not the full history, before starting work (see below).

## Structure this kit expects in a consumer project

```
project-knowledge/
  current.md            # consolidated current state: goal, status, facts, promotion candidates
  events/                # append-only, timestamped: what happened and why
  agents/
    current.md           # who owns which task right now
    handoffs/             # append-only handoff notes between sessions/agents
```

`project-knowledge/` is local to the project and is never overwritten by an update to this kit.

## This kit is static; projects only read it

This repository is the single, authoritative copy of the protocol. It is never copied, forked, or vendored into a consumer project. A project that duplicated it would drift from it the moment either side changed — ten projects would mean ten silently diverging copies of "the protocol." Instead, a consumer project keeps only:

1. its own `project-knowledge/` (its data — goal, facts, events, agent coordination), tracked in its own git repository, and
2. one small pointer file recording which version of this kit it follows.

An agent working in the project reads the pointer, fetches this kit's instructions from the pinned version (clone, fetch, or however the environment reaches this repo), follows them, and writes only into `project-knowledge/`. Nothing from `instructions/` or `templates/` is ever committed into the consumer project.

## Install

```bash
mkdir -p project-knowledge/events project-knowledge/agents/handoffs
```

Create `project-knowledge/kit-reference.md`:

```markdown
# Project Docs Kit reference

Kit repository: <this-repo-url>
Pinned version: 2026.09.28.1   # see this kit's OS_VERSION at that commit
Last checked: <date>            # last time an update check ran, applied or not
Last updated: <date>            # last time the pinned version actually changed
```

Then create `project-knowledge/current.md` and `project-knowledge/agents/current.md` from this kit's `templates/project-knowledge/` — either by fetching those two template files at the pinned version, or by hand, matching the structure `instructions/logging-protocol.md` and `instructions/agent-coordination.md` define.

Commit `project-knowledge/` (including `kit-reference.md`) into the project's own repository, the same as any other project file.

Agent entrypoint at the start of any session: [instructions/bootstrap.md](instructions/bootstrap.md) — an agent reads `project-knowledge/kit-reference.md` first to know which version of this kit to fetch and follow.

## Documents

- [instructions/bootstrap.md](instructions/bootstrap.md) — what an agent reads before starting work in a project
- [instructions/logging-protocol.md](instructions/logging-protocol.md) — how to record events, current state, and facts with evidence
- [instructions/agent-coordination.md](instructions/agent-coordination.md) — task ownership and handoffs across sessions/agents
- [instructions/promotion-protocol.md](instructions/promotion-protocol.md) — how project findings reach the central documentation
- [instructions/update-protocol.md](instructions/update-protocol.md) — how a project checks for and applies a newer kit version
- [instructions/commands.md](instructions/commands.md) — canonical install / apply / update commands for giving to an agent directly, as plain text

## Version and updates

Current kit version: see [OS_VERSION](OS_VERSION). Every version bump is explained in [CHANGELOG.md](CHANGELOG.md) — what changed and why, not just a number.

Because the kit is never vendored, updating touches exactly `project-knowledge/kit-reference.md` in the consumer project (the pinned version and the update timestamp), committed as an ordinary change. `project-knowledge/current.md`, `events/`, and `agents/` are never touched by a kit update.

An update is never automatic. From inside any project, ask an agent to check for or apply a kit update (any clear phrasing works) and it follows [instructions/update-protocol.md](instructions/update-protocol.md): fetch the current `OS_VERSION` and `CHANGELOG.md` from this repository, show what changed since the pinned version, and apply it only on explicit confirmation.

## Provenance

This kit started as a stripped-down variant of [mhdadizadeh/engineering-os](https://github.com/mhdadizadeh/engineering-os), keeping its event-log + current-state model and its multi-agent handoff structure, and dropping its mandatory two-stage confirmation protocol and mandatory-English rule as too heavy for day-to-day engineering work. It adds a promotion layer that the source repo did not have.
