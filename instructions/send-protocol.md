# Send Protocol

Status: Active

Last updated: 2026-09-28

Defines how a project's knowledge reaches the central documentation ("Domain Expert" docs, or whichever repository `project-knowledge/kit-reference.md` names as `Central docs repository`). This kit does not curate what gets promoted — it only gets the whole of `project-knowledge/current.md` there. What happens to it next (whether it becomes new central documentation, a revision of something existing, or nothing at all) is decided entirely on the central side; see that repository's own review protocol.

## What gets sent

The whole of `project-knowledge/current.md`, as it currently stands — not a hand-picked subset, and not `events/`. There is no local curation step and no candidate table to fill in first: send it, then let the center decide how (or whether) any of it enters the aggregated documentation. A section irrelevant to the center (e.g. a purely local open question) is harmless to send; the center's review is what filters, not this kit.

## Trigger

Explicit only, same as every other action this kit defines (e.g. "این پروژه رو به مستندات مرکزی بفرست" / "send this project's docs to the central docs"). Never runs on its own, on a schedule, or as a side effect of a bootstrap or logging step.

## Precondition

`project-knowledge/kit-reference.md` must name a `Central docs repository`. If that field is missing or says "not set," this project has no central destination configured yet — stop and ask the project owner for it (or confirm this is meant to stay manual/unset, see below), rather than guessing a repository.

## Two paths, same result

Either is valid. Which one applies depends only on whether an agent in this session can actually reach the central repository (clone/fetch/push it) — not on preference.

**Path A — agent-driven.** The agent itself sends the document:

1. Reach the central repository named in `kit-reference.md` (clone, or use an existing local copy, or push access — however this environment reaches git repositories).
2. Determine this project's slug (a short, stable, lowercase identifier for this project — check whether the central repo already has one for it from a prior send; if not, propose one from the project's name and confirm it with the owner before first use).
3. Copy the current contents of `project-knowledge/current.md` into that repository's per-project mirror location for this slug (as that repository's own protocol defines — do not invent a location; read its instructions if unsure).
4. Commit and push (or open the change however that repository's own contribution process expects), with a commit message naming this project and the date.
5. Record in this project's own `project-knowledge/current.md` Change history: that a send happened, the date, and to which slug — so a later read of this file shows when it was last sent, without needing to check the central repository.

**Path B — manual copy.** No agent in this session can reach the central repository (no credentials, no network path, or the person simply prefers to do it by hand):

1. The agent tells the project owner plainly: send `project-knowledge/current.md` to the central repository's per-project mirror location for this project (naming the file's path and, if known, the slug to use).
2. A person copies the file by hand into the central repository and commits it there, outside this session.
3. Once done, the agent (in this or a later session) records the same Change history line as in Path A, based on the owner confirming the copy happened.

Both paths produce the identical result: the central repository's mirror of this project ends up matching `project-knowledge/current.md` as of the send date. Neither path is more "correct" than the other — Path A is just Path B done by an agent with the right access.

## What this does not do

- Does not decide which claims are new vs. revisions of something already central — that judgment happens on the central side, which can see the whole aggregated documentation and this project's send history.
- Does not filter, summarize, or pre-select what's "worth" sending — the whole file goes, every time.
- Does not require re-sending only the parts that changed — always send the current file in full; the central side is responsible for detecting what's new since the last send (e.g. by diffing against its stored mirror).
