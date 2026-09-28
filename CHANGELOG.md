# Changelog

Every entry names what changed and why. This is what an update check shows a project owner before they approve pulling in a new pinned version — an update is a reviewed decision, never a blind version bump.

## 2026.09.28.5 — replace promotion with whole-document sending

- Removed `instructions/promotion-protocol.md` and the "Promotion candidates" table entirely (from `templates/project-knowledge/current.md` and the required-sections list in `instructions/logging-protocol.md`). A project no longer pre-curates which findings are "worth" the center's attention before anything leaves the project.
- Added `instructions/send-protocol.md` and a 4th canonical command (`instructions/commands.md`): sending now means the whole of `project-knowledge/current.md` goes to the central documentation, every time, with the central side entirely responsible for deciding what's new and how (or whether) it enters the aggregated docs.
- Two ways to send, both valid and producing the same result: an agent with access to the central repository sends it directly, or a person copies the file by hand. `kit-reference.md` gained two fields — `Central docs repository` and `Last sent` — so a project can name its destination and record when it last sent.
- Reasoning: the old model asked each project to gate-keep its own findings with an evidence table before anything reached the center, duplicating judgment that the center is better placed to make once it can see the whole aggregated documentation and every project's send history. This also removes a real bridge gap the old model had: nothing previously told an agent the central repository's address or how to actually get a candidate there.
- Updated README.md, USAGE.md §4, and `templates/AGENTS.snippet.md`'s wording accordingly.

## 2026.09.28.4 — drop multi-agent task coordination

- Removed `instructions/agent-coordination.md`, `project-knowledge/agents/` (current.md + handoffs/) from the expected structure and templates, and every reference to task claiming / handoff notes across README.md, USAGE.md, instructions/bootstrap.md, instructions/update-protocol.md, instructions/commands.md, and templates/AGENTS.snippet.md.
- Reasoning: that mechanism solves conflicts between multiple agents or people working the *same project at the same time*. This team works one session per project at a time, with a daily in-person meeting that already resolves ownership questions; `current.md`'s Change history plus `events/` already give session-to-session continuity. Keeping an unused coordination file was overhead with no one to benefit from it — added back later, with a version bump, if concurrent work on one project actually happens.
- `project-knowledge/current.md` and `events/` are unaffected; this only removes the `agents/` layer.

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
