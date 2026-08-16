# REQUIREMENTS.md — What This Library Is For

## Objective

Maintain a single, evolving source of truth for how AI coding agents should behave across all of the owner's projects, so standards (architecture, security, UX, documentation discipline) don't have to be re-specified from scratch every time a new project starts.

## Primary user

The repo owner, acting as the person who bootstraps new projects and who wants every project's AI agent to start from the same baseline of engineering judgment.

## Functional requirements

- `CLAUDE.md` must be **portable**: copyable as a single file into any new project's root and immediately usable, with only a small, clearly-marked section needing project-specific edits (skills path, DB engine, custom commands).
- Skills in `skills/` must be **self-contained**: a folder copy into a target project's `.claude/skills/` should be sufficient to activate it, with no dependency on other files in this repo.
- Rules in `rules/` must be **tool-flexible**: usable either pasted into `CLAUDE.md`, or consumed natively by tools that support the `trigger: always_on` convention (Cursor, Windsurf) or equivalent.
- Mini-skills embedded in `CLAUDE.md` must be **phrase-triggerable** without requiring a slash command, since they travel inline with the file.
- The Documentation System mini-skill must be applicable to any target project, producing the standard doc set (`README.md`, `USER.md`, `DEVELOPMENT.md`, `ARCHITECTURE.md`, `REQUIREMENTS.md`, `PROGRESS.md`, `TODO.md`, `DECISIONS.md`, `CHANGELOG.md`, `SECURITY.md`).

## Non-functional requirements

- **No secrets, ever.** This repo is instructions only and may be shared or reused broadly; it must never contain credentials, API keys, or real customer/business data (see [SECURITY.md](SECURITY.md)).
- **Backward compatibility of instructions.** Once a rule is established (e.g. "never destructive migrations," "never claim AI authorship"), it should not be silently reversed — changes go through [DECISIONS.md](DECISIONS.md).
- **Low maintenance overhead.** Prefer editing an existing rule/skill file over creating a new one for a near-duplicate concern; avoid fragmenting the same guidance across multiple files (this itself has already drifted once — see `rules/gemini-agent-rules` vs. the `## Database Operations` section duplicated in `CLAUDE.md`, noted in [DECISIONS.md](DECISIONS.md)).

## Out of scope

- Any actual application code, build tooling, or runtime — this repo produces no software artifact of its own.
- The owner's global `~/.claude/CLAUDE.md` (outside this repo) — that's personal machine configuration, not versioned here.

## Acceptance criteria for "this library is working"

- A brand-new project can be bootstrapped with consistent engineering, security, and documentation standards in under a few minutes by copying `CLAUDE.md` and any relevant `skills/`/`rules/` files.
- Every file referenced from another file in this repo (a skill's `LICENSE.txt`, a doc's cross-link, a path like `.claude/skills/`) actually exists or is explicitly marked as a known gap in [TODO.md](TODO.md).
