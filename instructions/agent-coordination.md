# Agent Coordination

Status: Active

Last updated: 2026-09-28

Defines how multiple agents (or people, or the same person across sessions) working on the same project stay coordinated, without being active at the same time.

This is carried over from the source repo's multi-agent v1 protocol largely unchanged — it was the strongest part of that design.

## Model

Shift-based, not live debate: agents are not assumed to be active at the same time, but each must be aware of the others' work, state, and open decisions. The user makes the final call on anything contested.

## Identity

Each agent uses a stable identity tied to its session, e.g. `codex:<session-id>`, `claude-code:<session-id>`. This identity is used for ownership, handoff history, and decision responsibility.

## Storage

- `project-knowledge/agents/current.md` — the authoritative current coordination state.
- `project-knowledge/agents/handoffs/` — append-only, timestamped, human-readable handoff files.

## Read-before-work rule

Before doing any work, an agent must read:

1. `project-knowledge/agents/current.md`;
2. the latest relevant handoff it references, if any.

This applies even if the latest status was written by the same agent in an earlier session. If neither exists, fall back to `project-knowledge/current.md`, recent events, and recent commits.

## Task claiming

Before starting a task, claim it in `project-knowledge/agents/current.md`. Each task has exactly one active owner. If another agent already owns a task, do not continue on it unless the user explicitly reassigns it. If ownership is ambiguous or stale enough to be unclear, ask the user rather than guessing.

## Write-after-work rule

Write a handoff note:

1. after finishing a task;
2. when blocked;
3. when work is paused or abandoned without finishing;
4. at commit time.

A handoff file records: timestamp, agent identity, task identifier, status, a summary of what was done, the current decision state, and what the next agent should know or do.

After writing a handoff, update `project-knowledge/agents/current.md` (task id, title, status, active owner, last handoff reference, last-updated timestamp) so it stays authoritative.

## Commit attribution

Include agent identity and task identifier in commit messages, e.g.:

```
<agent-id> | <task-id> | <summary>
```
