# CHANGELOG.md

## Unreleased

### Added

- Root `README.md` describing the repo's purpose and contents.
- Full `/docs/` documentation system: `USER.md`, `DEVELOPMENT.md`, `ARCHITECTURE.md`, `REQUIREMENTS.md`, `PROGRESS.md`, `TODO.md`, `DECISIONS.md`, `CHANGELOG.md`, `SECURITY.md`.

## 2026-09-21

### Added

- `emilkowalski/skills` installed live via `npx skills@latest add emilkowalski/skills`: `animate`, `animate-expo`, `animation-vocabulary`, `apple-design`, `ask-sonner`, `emil-design-eng`, `find-animation-opportunities`, `improve-animations`, `mobile-native`, `pick-ui-library`, `prototype`, `review-animations`, `write-swift`.
- `pbakaus/impeccable` installed live via `npx impeccable install`: the `impeccable` skill, four subagents under `.claude/agents/`, and `PostToolUse`/`Stop` design-check hooks.
- `nextlevelbuilder/ui-ux-pro-max-skill` installed live via `npx ui-ux-pro-max-cli init --ai claude`: `ui-ux-pro-max`, `banner-design`, `brand`, `design`, `design-system`, `slides`, `ui-styling`.
- `.gitignore` — excludes `.claude/settings.local.json`, `.claude/projects/`, the downloaded impeccable engine binary, `node_modules/`, and OS files.
- `docs/DECISIONS.md` D5 documenting why these plugins were installed live rather than vendored into `skills/`.

## 2026-08-16

### Added

- `rules/design-system-master.md` — always-on UI/UX/engineering expert persona rule.
- `rules/gemini-agent-rules` — project rules covering migrations, `.env.example` sync, docs/tests folder conventions, and architecture confirmation.
- `rules/high-quality-modern-ui-design.md` — always-on modern UI design principles rule.
- `rules/local-dev-env.md` — local PHP/MySQL (XAMPP) environment note.
- `CLAUDE.md` — master instruction file: project header instructions, session behavior, database operation rule, Engineering Constitution, and four embedded mini-skills (Goal-Driven Backcasting, Product Maturity Review, UIUX Design Mode, Documentation System).
- `archive/CLAUDE.md` — earlier, shorter version of the master instruction file, kept for reference.
- `skills/design-taste-frontend/SKILL.md` — detailed anti-slop frontend design skill.
- `skills/frontend-design/SKILL.md` — production-grade frontend interface generation skill.
- `CUSTOMCMD.md`, `Move The CLAUDE.md File To Project Root`, `skills/engineering-constitution/SKILL.md` — created as placeholders, currently empty.
