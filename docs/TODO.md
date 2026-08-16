# TODO.md — Outstanding Work

## Critical

_None currently — this is a personal instructions library, not a shipping product with live users._

## High

- **Fill or delete `CUSTOMCMD.md`** — referenced by `CLAUDE.md` ("Always Check the `.claude/CUSTOMCMD.md` for custom commands") but currently empty at the repo root, and at the wrong path relative to how it's referenced (`.claude/CUSTOMCMD.md` vs. root `CUSTOMCMD.md`). Clarify intended location and populate or remove the reference.
- **Add `skills/frontend-design/LICENSE.txt`** — the skill's frontmatter says "Complete terms in LICENSE.txt" but no such file exists in that folder.

## Medium

- **Resolve the empty note file** `Move The CLAUDE.md File To Project Root` — currently a filename-as-reminder with no body. Either write the actual reminder/checklist as file content, or fold it into `docs/USER.md`'s bootstrap steps and delete the file.
- **Consolidate or cross-link the duplicated migration policy** between `CLAUDE.md`'s `## Database Operations` section and `rules/gemini-agent-rules` (see [DECISIONS.md](DECISIONS.md) D3) if it drifts out of sync again.
- **Add a `.gitignore`** — none exists yet; low risk today since the repo has no build artifacts, but worth adding proactively (editor swap files, OS files) before the repo grows.
- **Wire up `design-taste-frontend`** with an explicit slash-invocation note or trigger description consistent with `frontend-design`, since both currently cover overlapping "frontend design" ground with different depth/style — clarify when each applies (see `docs/USER.md`).
- **Keep `skills/engineering-constitution/SKILL.md` in sync with `CLAUDE.md`'s inline constitution.** Now that the skill file carries the full constitution body under proper `SKILL.md` frontmatter (see [DECISIONS.md](DECISIONS.md) D1), the same text exists in two places; any future rule change must be applied to both or one will go stale.

## Low

- Consider adding a top-level LICENSE for the repo itself if it will ever be shared or made public.
- Consider a lightweight lint/check script that verifies every file path referenced inside `CLAUDE.md`, `README.md`, and skill frontmatter actually exists, to catch future drift automatically instead of by manual review.

## Technical debt

- `archive/CLAUDE.md` and the current `CLAUDE.md` share structure but have diverged; no changelog entry exists explaining exactly what changed between them beyond "expanded." If archived versions accumulate, consider dating archive filenames (e.g. `archive/CLAUDE.2026-08-16.md`) instead of a single `archive/CLAUDE.md`.
