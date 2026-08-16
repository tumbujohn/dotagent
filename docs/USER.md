# USER.md — Using the Rules Library

This is not an application with an end user; the "user" is whoever (currently the repo owner) sets up a new project and wants that project's AI coding agent to inherit consistent standards. This document explains the day-to-day workflows.

## Getting started with a new project

1. Copy [`../CLAUDE.md`](../CLAUDE.md) into the new project's root as `CLAUDE.md`.
2. Trim or adjust the project-specific parts near the top (skills location, database rules, custom instructions) to match the new project — the Engineering Constitution and mini-skills further down are meant to travel unchanged.
3. If the project needs any of the reusable skills, copy the relevant folder from [`../skills/`](../skills/) into that project's `.claude/skills/` directory.
4. If the project needs an always-on rule snippet (e.g. a UI design persona, a local dev environment note), copy the relevant file from [`../rules/`](../rules/) into the target tool's rules mechanism.
5. Create that project's own `/docs/` folder (README, DEVELOPMENT, ARCHITECTURE, REQUIREMENTS, PROGRESS, TODO, DECISIONS, CHANGELOG, SECURITY) as instructed by the Documentation System mini-skill embedded in `CLAUDE.md`.

## The mini-skills embedded in CLAUDE.md

`CLAUDE.md` embeds several "mini skills" that a Claude Code session recognizes by trigger phrase (case-insensitive, spacing-insensitive):

| Trigger phrase | What it does |
|---|---|
| "Goal-Driven ..." (e.g. "be goal driven") | Switches to a Gap-Analysis & Backcasting PM persona that reverse-engineers a roadmap from a stated end-goal back to today. |
| "Product Maturity Review" / "Product Review" | Switches to an aggressive, multi-expert Product Review Board persona that audits the current project against world-class SaaS standards and produces a scored report with an action plan. |
| "UIUX Design Mode" / "Design Mode" / "Design Review" | Switches to an elite product-design-team persona for reviewing or producing UI/UX work against real design systems and UX heuristics. |
| "Documentation Mode" / "Docs Mode" / "Documentation Review" / "Review the docs" / "Update project docs" | Activates the Documentation System: treats the project's `/docs/` (or repo-root `README.md`) as the source of truth, reviews for drift, and creates/updates the core docs. |

These are invoked by saying the trigger phrase in conversation with Claude Code inside a project that has this `CLAUDE.md` installed — no slash command needed.

## Slash-invoked skills

Skills under `skills/` are invoked with `/skill-name` once installed into a project's `.claude/skills/`:

- `/frontend-design` — production-grade, distinctive UI generation (see [`../skills/frontend-design/SKILL.md`](../skills/frontend-design/SKILL.md)). The project `CLAUDE.md` requires this to be invoked before any frontend work.
- `design-taste-frontend` — a more detailed anti-slop frontend skill for landing pages, portfolios, and redesigns, with explicit "dials" for variance/motion/density and hard layout rules (see [`../skills/design-taste-frontend/SKILL.md`](../skills/design-taste-frontend/SKILL.md)). Not yet wired up with a slash trigger of its own — currently reference material.
- `engineering-constitution` — placeholder skill; currently empty. The actual constitution content lives inline in `CLAUDE.md` (see [ARCHITECTURE.md](ARCHITECTURE.md) and [DECISIONS.md](DECISIONS.md)).

## Global vs. project CLAUDE.md

The repo owner also maintains a separate global `~/.claude/CLAUDE.md` (outside this repo) with cross-project preferences (e.g. the `graphify` skill trigger). That file is personal machine configuration, not part of this library, and is out of scope for this repo's documentation.
