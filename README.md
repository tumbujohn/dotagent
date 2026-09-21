# .agent — Personal Agentic Development Rules Library

A personal, versioned library of instructions, skills, and rules for working with AI coding agents (Claude Code, Gemini CLI, Cursor/Windsurf-style tools). This repo is not an application — it *is* the configuration: an "engineering constitution," a set of reusable Claude Code skills, and a collection of standalone rule files that get copied or referenced into other project repositories.

## Purpose

Keep one canonical, evolving copy of:

- The master `CLAUDE.md` — an engineering constitution plus embedded mini-skills (Goal-Driven Backcasting, Product Maturity Review, UIUX Design Mode, Documentation System) that get dropped into a project's root so any Claude Code session in that project inherits the same standards.
- Reusable Claude Code **skills** (`skills/`) — self-contained `SKILL.md` packages invoked with `/skill-name`.
- Standalone **rules** (`rules/`) — always-on instruction snippets in the Cursor/Windsurf `trigger: always_on` style, or free-form notes, that can be pasted into a project's agent config.

The goal is to stop re-writing the same instructions for every new project and instead maintain one source of truth that improves over time.

## Contents

| Path | What it is |
|---|---|
| [`CLAUDE.md`](CLAUDE.md) | Master instruction file for Claude Code: engineering constitution, documentation system, and mini-skills. Meant to be copied to a new project's root (or referenced from it). |
| [`CUSTOMCMD.md`](CUSTOMCMD.md) | Placeholder for project-specific custom commands that fine-tune `CLAUDE.md` (currently empty — see [docs/TODO.md](docs/TODO.md)). |
| [`archive/CLAUDE.md`](archive/CLAUDE.md) | Earlier, shorter version of the master `CLAUDE.md`, kept for reference. |
| [`skills/frontend-design/`](skills/frontend-design/SKILL.md) | Claude's official-style skill for distinctive, production-grade frontend UI generation. |
| [`skills/design-taste-frontend/`](skills/design-taste-frontend/SKILL.md) | Detailed "anti-slop" frontend skill for landing pages, portfolios, and redesigns (brief inference, design dials, layout/typography/motion rules). |
| [`skills/engineering-constitution/`](skills/engineering-constitution/SKILL.md) | Placeholder skill wrapper for the engineering constitution (currently empty — content currently lives inline in `CLAUDE.md`). |
| [`rules/`](rules/) | Standalone always-on rule snippets (UI design expert persona, modern UI design principles, local dev environment notes, general project rules). |
| `.claude/skills/`, `.agents/skills/` | Live, installed third-party plugin skills for use in *this* repo (not the source library — see below). |

## Installed plugin skills

Unlike `skills/` (a source library meant to be copied into other projects), `.claude/skills/` and `.agents/skills/` hold third-party skills installed directly into this repo with their own official installers, so they're available immediately in any Claude Code (or Codex CLI) session opened here:

| Plugin | Install command | What it adds |
|---|---|---|
| [emilkowalski/skills](https://github.com/emilkowalski/skills) | `npx skills@latest add emilkowalski/skills` | Animation, Apple design, Swift, and UI-library-choice skills (`animate`, `apple-design`, `emil-design-eng`, `review-animations`, and others). |
| [pbakaus/impeccable](https://github.com/pbakaus/impeccable) | `npx impeccable install` | The `impeccable` skill: 24 `/impeccable <command>` design commands plus deterministic detector rules, wired to a `PostToolUse`/`Stop` hook in `.claude/settings.local.json`. Run `/impeccable init` once inside Claude Code to finish setup. |
| [nextlevelbuilder/ui-ux-pro-max-skill](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill) | `npx ui-ux-pro-max-cli init --ai claude` | The `ui-ux-pro-max` skill plus `banner-design`, `brand`, `design`, `design-system`, `slides`, `ui-styling` skills for design-system generation. |

Each installer can be re-run with its `update` (or equivalent) subcommand to pull newer versions. See [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md) for how this coexists with the `skills/` source library.

## How to use this repo

1. **New project bootstrap:** copy `CLAUDE.md` into the target project's root (see the empty note file `Move The CLAUDE.md File To Project Root` — a reminder of this step) and adjust the project-specific sections (skills path, DB rules, etc.) to match that project.
2. **Skills:** copy a folder from `skills/` into the target project's `.claude/skills/` directory so it can be invoked with `/skill-name`.
3. **Rules:** paste the relevant file from `rules/` into whatever always-on rules mechanism the target tool supports (e.g. Windsurf/Cursor rules, or a section of `CLAUDE.md`).

## Documentation

Full project documentation lives in [`docs/`](docs/):

- [USER.md](docs/USER.md) — how to use this library day to day
- [DEVELOPMENT.md](docs/DEVELOPMENT.md) — conventions for adding/editing rules and skills
- [ARCHITECTURE.md](docs/ARCHITECTURE.md) — how the pieces fit together
- [REQUIREMENTS.md](docs/REQUIREMENTS.md) — what this library is for and its constraints
- [PROGRESS.md](docs/PROGRESS.md) — current state
- [TODO.md](docs/TODO.md) — outstanding work
- [DECISIONS.md](docs/DECISIONS.md) — why things are structured this way
- [CHANGELOG.md](docs/CHANGELOG.md) — history of meaningful changes
- [SECURITY.md](docs/SECURITY.md) — security posture for a rules-only repo

## Status

Early stage, actively growing. See [docs/PROGRESS.md](docs/PROGRESS.md) and [docs/TODO.md](docs/TODO.md).
