# Changelog

Every entry names what changed and why. This is what an update check shows a project owner before they approve pulling in a new pinned version — an update is a reviewed decision, never a blind version bump.

## 2026.09.28.3 — trim README, fill placeholder URLs

- Removed the "What this kit deliberately does not do" and "Provenance" sections from README.md. Their content (dropping the two-stage confirm protocol and mandatory-English rule, and the origin in `mhdadizadeh/engineering-os`) is historical context, not something an agent or a project owner needs on every read of the README.
- Replaced all remaining `<repo-url>` / `<آدرس مخزن>` / `<this-repo-url>` placeholders across README.md, USAGE.md, and instructions/commands.md with the real, published repository URL (`https://github.com/mhdadizadeh/project-docs-kit`), and corrected stale `2026.09.28.1` example version strings to match the current version.

## 2026.09.28.2 — align with AGENTS.md

- Added `templates/AGENTS.snippet.md`: a short, stable section a project adds to its own `AGENTS.md` (the open, widely-adopted convention that Codex, Cursor, GitHub Copilot, and other current tools already read automatically at session start). This makes this kit's bootstrap automatic on any tool that reads `AGENTS.md` on its own, with the explicit commands remaining as the fallback for tools that don't.
- Updated README, `instructions/bootstrap.md`, `instructions/commands.md`, and USAGE.md to describe both the automatic (`AGENTS.md`) and explicit (direct command) paths into bootstrap.
- Reasoning: AGENTS.md is a real, broadly-adopted standard (60,000+ repositories, supported by most major agent tools as of this writing) for exactly the problem this kit's own bootstrap discovery was solving from scratch. Rather than compete with it, this kit now plugs into it. The kit's protocol content is still never vendored into a project — only the pointer lives there, same as before.

## 2026.09.28.1 — initial release

- Distilled from `mhdadizadeh/engineering-os`: kept the append-only events + consolidated `current.md` knowledge model, and the multi-agent task-ownership + handoff protocol.
- Dropped the mandatory two-stage confirm-before-acting workflow. Agents ask when a request is genuinely ambiguous or a decision is expensive to undo; otherwise they proceed.
- Dropped the mandatory-English / bilingual-output rule. A project writes in whichever language its team works in.
- Added `Facts and assumptions` as a required table in `current.md` (claim, evidence, status: hypothesis/confirmed/rejected, date) — the source repo had no equivalent, and without it a guess and a measured result are indistinguishable a month later.
- Added `Tools and approaches in use` (what's used, why, what was rejected) to `current.md` — so "is this still the right tool" doesn't require reconstructing the original research from memory.
- Added the promotion protocol: a `Promotion candidates` table in each project's `current.md`, a periodic or milestone-triggered review across all projects, and an explicit approval step before anything reaches central documentation. The source repo had no concept of many independent projects feeding one shared documentation system.
- Made the kit itself static: it is never vendored or copied into a consumer project. A project keeps only `project-knowledge/` plus a `kit-reference.md` pointer naming this repository and a pinned version. See `instructions/update-protocol.md` for how a project checks for and applies a new version.
