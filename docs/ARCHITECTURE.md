# ARCHITECTURE.md — How This Library Is Put Together

There is no runtime architecture (no servers, database, or APIs). The "architecture" here is the structure of instruction files and how an AI coding agent (primarily Claude Code) discovers and applies them.

## Layers

```
.agent/
├── CLAUDE.md                              # Master instruction file (project-root convention for Claude Code)
├── CUSTOMCMD.md                           # Project-specific command overrides (currently empty, see TODO)
├── Move The CLAUDE.md File To Project Root  # Empty file used as a filename-as-note reminder
├── .gitignore                             # Local-only state and downloaded binaries excluded from version control
├── archive/
│   └── CLAUDE.md                          # Superseded, shorter version of the master file
├── rules/                                 # Standalone, tool-agnostic instruction snippets
│   ├── design-system-master.md
│   ├── gemini-agent-rules
│   ├── high-quality-modern-ui-design.md
│   └── local-dev-env.md
├── skills/                                # Claude Code skill packages (SKILL.md convention) — SOURCE LIBRARY
│   ├── design-taste-frontend/SKILL.md
│   ├── engineering-constitution/SKILL.md  # placeholder, empty
│   └── frontend-design/SKILL.md
├── .claude/                               # LIVE install target for this repo's own Claude Code sessions
│   ├── agents/                            # Subagents shipped by the impeccable plugin
│   ├── settings.local.json                # Hooks wired by the impeccable installer (gitignored)
│   └── skills/                            # Installed third-party plugin skills (see below)
├── .agents/skills/                        # Same plugin skills, in the tool-agnostic "universal" layout (Codex CLI, etc.)
├── .codex/hooks.json                      # Codex CLI hook wiring, written by the impeccable installer
├── skills-lock.json                       # Provenance/hash lockfile for skills installed via `npx skills@latest`
└── docs/                                  # This documentation system
```

## How Claude Code consumes these files

1. **Global instructions**: `~/.claude/CLAUDE.md` (outside this repo, personal machine config) is always loaded and can reference globally-installed skills (e.g. `graphify`).
2. **Project instructions**: when this repo's `CLAUDE.md` is copied into a target project's root, Claude Code loads it as project instructions on every session in that project. It layers on top of (and can override, for project-specific behavior) the global file.
3. **Skills (source library)**: Claude Code discovers skills under a project's `.claude/skills/<name>/SKILL.md`. The `skills/` folder in *this* repo is a source library — a skill only becomes active in a *target* project once its folder is copied there. Skills are invoked explicitly via `/skill-name`, or proactively when the skill's `description` frontmatter matches the task.
4. **Skills (live, installed in this repo)**: `.claude/skills/` and `.agents/skills/` are a *second*, separate mechanism — third-party plugin skills installed directly into this repo via each plugin's own official installer (`npx skills@latest add emilkowalski/skills`, `npx impeccable install`, `npx ui-ux-pro-max-cli init --ai claude`), so they're active in any Claude Code or Codex CLI session opened in *this* repo. `.agents/skills/` is the "universal" layout some installers also write for tools that read that convention (Codex CLI, Cursor, Gemini CLI, etc.); on this repo's Windows/Git-Bash environment, several `.claude/skills/<name>` entries are symlinks into `.agents/skills/<name>` rather than duplicated folders. These installed skills are not copied into `skills/` — they stay independent of the source-library workflow described in point 3, since they're meant for use while working in *this* repo, not for redistribution. See [DECISIONS.md](DECISIONS.md) D5.
5. **Rules**: the `rules/` folder holds files in the Cursor/Windsurf "always-on rule" convention (`trigger: always_on` frontmatter + persona/instruction body), plus at least one free-form instruction file. These are not a Claude Code native concept — they're either pasted into `CLAUDE.md`, or used with tools (Cursor, Windsurf, Gemini CLI) that support that convention directly.
6. **Mini-skills embedded in CLAUDE.md**: rather than separate files, several skills (Goal-Driven Backcasting, Product Maturity Review, UIUX Design Mode, Documentation System) are written directly inside `CLAUDE.md` and triggered by phrase-matching in conversation, so they travel with the file as a single copy-paste unit rather than requiring a `.claude/skills/` install step.
7. **Hooks**: the impeccable installer wired `PostToolUse` (after `Edit`/`Write` on UI files) and `Stop` hooks into `.claude/settings.local.json` (gitignored, per-machine) and `.codex/hooks.json`, running its `impeccable` binary to flag design anti-patterns automatically during a session.

## Why content lives inline in CLAUDE.md instead of as skills

`CLAUDE.md` is designed to be portable — copied wholesale into a new project's root. Anything that must always be present without a separate install step (the Engineering Constitution, the four mini-skills) is written inline. Anything reusable but optional, or large enough to warrant independent iteration (frontend design guidance, the anti-slop frontend skill), lives as a separate skill package that gets installed only where needed. See [DECISIONS.md](DECISIONS.md).

## Known structural gaps

- `skills/engineering-constitution/SKILL.md` exists as a folder but is empty — the constitution content currently only lives inline in `CLAUDE.md`. Whether this should be extracted into the skill file (single source, referenced by both) or removed is an open decision — see [TODO.md](TODO.md).
- `skills/frontend-design/SKILL.md` frontmatter references `LICENSE.txt` "for complete terms," but no `LICENSE.txt` exists in that folder.
- `.claude/skills/impeccable/scripts/bin/windows-x64/impeccable.exe` and its `.agents/` duplicate are ~15 MB platform-specific downloaded binaries, excluded via `.gitignore` rather than committed — a fresh clone needs to re-run the impeccable installer (or `impeccable update`) to restore them.
- `.claude/skills/` and `.agents/skills/` duplicate ~15 MB of content each (the impeccable engine, font index, live-browser bundle) since Windows symlinks weren't used for every installed skill — acceptable for now since both are gitignored where large, but worth revisiting if disk/repo size becomes a concern.
