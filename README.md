# Project Docs Kit

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

## Install

```bash
git clone <this-repo-url> .project-docs-kit
mkdir -p project-knowledge/events project-knowledge/agents/handoffs
cp .project-docs-kit/templates/project-knowledge/current.md project-knowledge/current.md
cp .project-docs-kit/templates/project-knowledge/agents/current.md project-knowledge/agents/current.md
```

Agent entrypoint after installation: [instructions/bootstrap.md](instructions/bootstrap.md)

## Documents

- [instructions/bootstrap.md](instructions/bootstrap.md) — what an agent reads before starting work in a project
- [instructions/logging-protocol.md](instructions/logging-protocol.md) — how to record events, current state, and facts with evidence
- [instructions/agent-coordination.md](instructions/agent-coordination.md) — task ownership and handoffs across sessions/agents
- [instructions/promotion-protocol.md](instructions/promotion-protocol.md) — how project findings reach the central documentation

## Version

Current kit version: see [OS_VERSION](OS_VERSION). Update model is replacement-based, same as the shared OS this kit was distilled from: fetch a newer version, replace the kit files, never touch `project-knowledge/`.

## Provenance

This kit started as a stripped-down variant of [mhdadizadeh/engineering-os](https://github.com/mhdadizadeh/engineering-os), keeping its event-log + current-state model and its multi-agent handoff structure, and dropping its mandatory two-stage confirmation protocol and mandatory-English rule as too heavy for day-to-day engineering work. It adds a promotion layer that the source repo did not have.
