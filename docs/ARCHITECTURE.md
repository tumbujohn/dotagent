# ARCHITECTURE.md — How This Library Is Put Together

There is no runtime architecture (no servers, database, or APIs). The "architecture" here is the structure of instruction files and how an AI coding agent (primarily Claude Code) discovers and applies them.

## Layers

```
.agent/
├── CLAUDE.md                              # Master instruction file (project-root convention for Claude Code)
├── CUSTOMCMD.md                           # Project-specific command overrides (currently empty, see TODO)
├── Move The CLAUDE.md File To Project Root  # Empty file used as a filename-as-note reminder
├── archive/
│   └── CLAUDE.md                          # Superseded, shorter version of the master file
├── rules/                                 # Standalone, tool-agnostic instruction snippets
│   ├── design-system-master.md
│   ├── gemini-agent-rules
│   ├── high-quality-modern-ui-design.md
│   └── local-dev-env.md
├── skills/                                # Claude Code skill packages (SKILL.md convention)
│   ├── design-taste-frontend/SKILL.md
│   ├── engineering-constitution/SKILL.md  # placeholder, empty
│   └── frontend-design/SKILL.md
└── docs/                                  # This documentation system
```

## How Claude Code consumes these files

1. **Global instructions**: `~/.claude/CLAUDE.md` (outside this repo, personal machine config) is always loaded and can reference globally-installed skills (e.g. `graphify`).
2. **Project instructions**: when this repo's `CLAUDE.md` is copied into a target project's root, Claude Code loads it as project instructions on every session in that project. It layers on top of (and can override, for project-specific behavior) the global file.
3. **Skills**: Claude Code discovers skills under a project's `.claude/skills/<name>/SKILL.md`. The `skills/` folder in *this* repo is the source library — a skill only becomes active in a target project once its folder is copied there. Skills are invoked explicitly via `/skill-name`, or proactively when the skill's `description` frontmatter matches the task.
4. **Rules**: the `rules/` folder holds files in the Cursor/Windsurf "always-on rule" convention (`trigger: always_on` frontmatter + persona/instruction body), plus at least one free-form instruction file. These are not a Claude Code native concept — they're either pasted into `CLAUDE.md`, or used with tools (Cursor, Windsurf, Gemini CLI) that support that convention directly.
5. **Mini-skills embedded in CLAUDE.md**: rather than separate files, several skills (Goal-Driven Backcasting, Product Maturity Review, UIUX Design Mode, Documentation System) are written directly inside `CLAUDE.md` and triggered by phrase-matching in conversation, so they travel with the file as a single copy-paste unit rather than requiring a `.claude/skills/` install step.

## Why content lives inline in CLAUDE.md instead of as skills

`CLAUDE.md` is designed to be portable — copied wholesale into a new project's root. Anything that must always be present without a separate install step (the Engineering Constitution, the four mini-skills) is written inline. Anything reusable but optional, or large enough to warrant independent iteration (frontend design guidance, the anti-slop frontend skill), lives as a separate skill package that gets installed only where needed. See [DECISIONS.md](DECISIONS.md).

## Known structural gaps

- `skills/engineering-constitution/SKILL.md` exists as a folder but is empty — the constitution content currently only lives inline in `CLAUDE.md`. Whether this should be extracted into the skill file (single source, referenced by both) or removed is an open decision — see [TODO.md](TODO.md).
- `skills/frontend-design/SKILL.md` frontmatter references `LICENSE.txt` "for complete terms," but no `LICENSE.txt` exists in that folder.
- No `.claude/` directory exists in this repo itself (expected — the skills here are a source library for *other* projects' `.claude/skills/`, not for this repo's own use).
- No `.gitignore` exists yet.
