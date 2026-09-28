# Update Protocol

Status: Active

Last updated: 2026-09-28

Defines how a consumer project checks whether a newer version of this kit exists, and how it applies an update. This kit is never vendored (see README), so an update never touches more than `project-knowledge/kit-reference.md`.

## Trigger

Run this protocol when the user explicitly asks for it in a project — any clear phrasing of "check for a kit update," "update the kit," "is the docs protocol current," etc. counts. It does not run automatically or silently in the background.

An agent may proactively note that a check has not run in a long time (see `Last checked` below) and suggest running it, but must not run it, and must never apply an update, without the user asking.

## Steps

1. Read `project-knowledge/kit-reference.md` for the kit repository URL and the currently pinned version.
2. Fetch, from that repository's default branch: `OS_VERSION` and `CHANGELOG.md`. This does not require vendoring the kit — read the two files directly (e.g. a shallow fetch, or reading the files at the remote HEAD), discard anything else fetched.
3. Update `Last checked` in `kit-reference.md` to today's date regardless of outcome — a check that finds nothing new is still a check that happened.
4. Compare the fetched `OS_VERSION` with the pinned version.
   - **Same:** report "kit is current, no changes since last check." Stop.
   - **Different:** continue.
5. From `CHANGELOG.md`, extract every entry strictly newer than the pinned version, up to and including the fetched version. Show these to the user as what would change — not just the version number.
6. Ask for explicit confirmation before applying. An update is a deliberate, reviewed decision by the project owner, never automatic — same principle the source repo (engineering-os) held for its own updates, kept here even though the old per-request confirmation workflow was dropped.
7. **On confirmation:** set `Pinned version` to the new version and `Last updated` to today's date in `kit-reference.md`. Commit this as its own change in the project's repository, with a message naming the old and new version. For the remainder of the session, follow the instructions at the new pinned version — re-fetch and re-read them; do not keep relying on an earlier reading from before the update.
8. **On decline:** leave `Pinned version` unchanged. Optionally record a one-line knowledge event noting an update was checked and declined, and why, if the reason is worth remembering (see `instructions/logging-protocol.md`) — this prevents the same version being re-proposed without anyone recalling it was already considered and rejected.

## What this does not cover

This protocol updates only which version of the kit's instructions a project follows. It never touches `project-knowledge/current.md`, `events/`, or `agents/` — those are the project's own data and are never part of a kit update.
