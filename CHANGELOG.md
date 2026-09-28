# Changelog

Every entry names what changed and why. This is what an update check shows a project owner before they approve pulling in a new pinned version — an update is a reviewed decision, never a blind version bump.

## 2026.09.28.1 — initial release

- Distilled from `mhdadizadeh/engineering-os`: kept the append-only events + consolidated `current.md` knowledge model, and the multi-agent task-ownership + handoff protocol.
- Dropped the mandatory two-stage confirm-before-acting workflow. Agents ask when a request is genuinely ambiguous or a decision is expensive to undo; otherwise they proceed.
- Dropped the mandatory-English / bilingual-output rule. A project writes in whichever language its team works in.
- Added `Facts and assumptions` as a required table in `current.md` (claim, evidence, status: hypothesis/confirmed/rejected, date) — the source repo had no equivalent, and without it a guess and a measured result are indistinguishable a month later.
- Added `Tools and approaches in use` (what's used, why, what was rejected) to `current.md` — so "is this still the right tool" doesn't require reconstructing the original research from memory.
- Added the promotion protocol: a `Promotion candidates` table in each project's `current.md`, a periodic or milestone-triggered review across all projects, and an explicit approval step before anything reaches central documentation. The source repo had no concept of many independent projects feeding one shared documentation system.
- Made the kit itself static: it is never vendored or copied into a consumer project. A project keeps only `project-knowledge/` plus a `kit-reference.md` pointer naming this repository and a pinned version. See `instructions/update-protocol.md` for how a project checks for and applies a new version.
