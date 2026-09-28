# Logging Protocol

Status: Active

Last updated: 2026-09-28

Defines how a project records its own knowledge: what happened (history) and where things stand now (current state).

## Two artifacts, not one

- **Events** (`project-knowledge/events/*.md`): append-only, timestamped, one file per event. Never edited in place. This is the log of what was decided, tried, found, or changed, and why.
- **Current state** (`project-knowledge/current.md`): the consolidated, living document. When an event changes the current understanding, update this file and reference the event that caused the change. This is what an agent reads before doing anything else — not the full event log.

Analogy: events are an edit log, current state is the reconstructed, current view. Both are required. History explains how the project got here; current state explains where it is now.

## Event file format

Filename: `<UTC-timestamp>-<short-slug>.md`, e.g. `2026-09-28T101500Z-switched-lineage-parser.md`.

```markdown
## Knowledge Event

Timestamp: 2026-09-28T10:15:00Z

Type: Decision | Finding | Fact | Risk

Summary: one line.

Details: what happened, what was tried, what was found. Enough that someone with no memory of the session understands it.

Evidence: what supports this (a measurement, a test result, a human statement, an external source with link+date). If there is none yet, say so explicitly — do not omit this field.
```

## Current-state format (`project-knowledge/current.md`)

Required sections:

- **Goal** — what this project is for, in one paragraph.
- **Current status** — what stage the project is at, updated whenever it materially changes.
- **Facts and assumptions** — a table. Every row has: the claim, its evidence, its status (`confirmed` / `hypothesis` / `rejected`), and the date. A claim with no evidence is a hypothesis, not a fact, and must be labeled as one — this table is what keeps the project's agents from treating a guess as settled knowledge.
- **Tools and approaches in use** — what is used, why it was chosen, what alternatives were considered and rejected (even briefly). This is what lets someone later ask "is this still the right tool" without redoing the original research.
- **Open questions** — unresolved items, one line each.
- **Promotion candidates** — see [promotion-protocol.md](promotion-protocol.md). Do not put central-documentation material anywhere else; this is the one place a promotion review will look.
- **Change history** — one line per update to this file, each referencing the event that caused it.

## Rule for updating current state

When new knowledge changes the current understanding:

1. Write the event first (append-only, never skip this even if it feels like a small change).
2. Update `current.md`.
3. In the Change History section, record why it changed and link the event.

Do not overwrite a fact silently. If a prior belief turns out to be wrong, the event log keeps the record of what was believed and when it changed; `current.md` reflects only the present understanding.

## Language

Write in whichever language the project team actually works in. This kit does not require English or bilingual output. Pick one language per project and stay consistent within `project-knowledge/`, so an agent reading the file later is not guessing which language a given fact is in.
