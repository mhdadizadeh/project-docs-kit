# Promotion Protocol

Status: Active

Last updated: 2026-09-28

Defines how a finding, decision, or tool evaluation moves from one project's local knowledge (`project-knowledge/`) into the organization's central documentation. This is the layer the source repo (engineering-os) did not have: it only distinguished a shared, replaceable OS layer from a single project's local knowledge. It had no path from many independent projects into one shared body of knowledge.

## Why this exists

Each project accumulates knowledge fast and informally — that speed is the point of the logging protocol. But not everything in a project's `current.md` belongs in central documentation: most of it is project-specific noise from the org's point of view. Promotion is the deliberate, small, reviewed path for the minority that does matter beyond one project.

## Marking a promotion candidate

In `project-knowledge/current.md`, under **Promotion candidates**, the project owner (or an agent, subject to the project owner's review) adds a row for anything they believe is worth the central documentation's attention:

```markdown
| Claim | Why it matters beyond this project | Evidence | Source event | Status |
| --- | --- | --- | --- | --- |
| Tool X's column-lineage parser fails silently on CTEs | Same tool is a candidate for two other projects | ran on 40 queries, 6 silent failures, see event | events/2026-09-20T...-lineage-parser-eval.md | pending |
```

`Status` starts as `pending` and moves to `promoted` or `rejected` once reviewed (see below) — never delete the row, so the project's own history of what it proposed stays intact.

A candidate with no evidence row, or evidence that is just "an agent suggested it," is not ready — send it back with a note on what evidence is missing, do not promote a guess just because it is plausible.

## Promotion review

Trigger: either on a schedule the organization sets, or on a real event (a milestone, a decision that turned out to generalize) — pick whichever the organization actually sustains; a calendar date nobody protects time for is worse than an honest "review on milestones only."

Process:

1. An agent (or person) reads the **Promotion candidates** section of every project's `project-knowledge/current.md` since the last review. It does not need to read each project's full history — only pending candidates and their linked source events.
2. It produces a **promotion proposal**: for each candidate, the claim, the evidence, which project it came from (path + event reference), and — when two projects proposed conflicting claims — the conflict stated explicitly, not silently resolved in favor of either.
3. The proposal goes to the central documentation's owner for approval. Nothing is merged into central documentation automatically.
4. On approval: the finding is written into central documentation with a citation back to the source project and event (never re-derived from memory); the candidate's `Status` in the source project is updated to `promoted`.
5. On rejection: the candidate's `Status` is updated to `rejected` with a one-line reason, and it stays in the project's own record — a rejection is information too, and re-proposing the same unsupported claim later should be visibly not new.

## Who approves

Default: the central documentation's owner. If the organization has designated a different approver, name them here explicitly rather than leaving it to whoever runs the review.

## What this protects against

- A single project's untested guess quietly becoming "how the org does things."
- The central documentation accumulating claims nobody can trace back to where they came from.
- Two projects' conflicting findings getting silently averaged instead of surfaced.
