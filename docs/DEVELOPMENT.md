# DEVELOPMENT.md — Contributing to This Library

This repo has no build, no dependencies, and no runtime — it is markdown. "Development" means authoring and curating instruction files. This document covers the conventions for doing that consistently.

## Environment

- Plain text / Markdown editing. No install step, no package manager.
- Git repository, currently a single local branch (`main`), no remote configured yet.

## Folder conventions

- **`skills/<skill-name>/SKILL.md`** — Claude Code skill packages. Each skill folder holds a `SKILL.md` with YAML frontmatter (`name`, `description`, optionally `license`) followed by the skill body. This is the Claude Code skill format (invoked via `/skill-name` once installed into a project's `.claude/skills/`).
- **`rules/`** — flat files, not skill packages. Two current styles coexist:
  - Cursor/Windsurf-style always-on rules: YAML frontmatter with `trigger: always_on` followed by a persona/instruction block (see `rules/design-system-master.md`, `rules/high-quality-modern-ui-design.md`, `rules/local-dev-env.md`).
  - Free-form instruction notes with no frontmatter (see `rules/gemini-agent-rules`).
  When adding a new rule file, match the style of the tool it targets; don't force every rule into the `trigger: always_on` frontmatter if the target tool doesn't use it.
- **`archive/`** — superseded versions of files kept for historical reference (currently an older `CLAUDE.md`). Never edit files in `archive/` — only add newly-superseded versions to it.
- **`docs/`** — this documentation system, per the Documentation System mini-skill embedded in the root `CLAUDE.md`.

## Adding a new skill

1. Create `skills/<kebab-case-name>/SKILL.md`.
2. Add YAML frontmatter: `name` (matches the folder name), `description` (specific — this is what a Claude Code session uses to decide relevance).
3. Write the skill body: role/context, process, and any hard rules. Prefer concrete, testable rules over vague guidance (see `skills/design-taste-frontend/SKILL.md` for the density of detail to aim for).
4. If the skill references a `LICENSE.txt`, include one in the same folder — don't reference a file that doesn't exist (see [TODO.md](TODO.md)).
5. Update the root [`README.md`](../README.md) contents table and [`docs/USER.md`](USER.md) with the new skill's trigger and purpose.

## Adding a new rule

1. Add the file under `rules/`, named for what it configures (not the tool it happens to have been written for first, unless it's genuinely tool-specific).
2. Keep each rule file scoped to one concern (one persona, one environment note, one set of problem/best-practice pairs) rather than growing a catch-all file.
3. Cross-reference from `README.md` if the rule is significant enough to be discoverable at a glance.

## Editing the master CLAUDE.md

`CLAUDE.md` is copied into other projects, so treat changes carefully:

- Keep the Engineering Constitution and the embedded mini-skills (Goal-Driven Backcasting, Product Maturity Review, UIUX Design Mode, Documentation System) generic and project-agnostic — they should work unmodified in any project.
- Keep genuinely project-specific instructions (skills path, DB engine notes, custom commands) near the top, clearly separated, so a project bootstrapping from this file knows what to edit.
- When behavior changes materially (a rule added, removed, or reversed), record it in [DECISIONS.md](DECISIONS.md) and [CHANGELOG.md](CHANGELOG.md) — never silently reverse an established rule.
- If a change supersedes the whole file's structure, copy the previous version into `archive/` before rewriting, so prior instructions remain recoverable.

## Git workflow

- Small commits, one logical change per commit (adding one skill, one rule file, or one doc update).
- Meaningful commit messages describing what instruction/skill changed and why, not just "update files."
- No CI, no automated tests exist for this repo — "correctness" is reviewed by reading the instruction text and, where practical, exercising the skill/rule in a real Claude Code session against a sample project.

## Verifying a change

There is no automated test suite. Before considering a skill or rule change done:

- Re-read the file for internal consistency (no contradictory rules within the same file).
- Check that any file path, command, or tool name it references actually exists (this repo has previously drifted — see [DECISIONS.md](DECISIONS.md) and [TODO.md](TODO.md)).
- If practical, load the change into an actual project and confirm the trigger phrase or slash command activates it as expected.
