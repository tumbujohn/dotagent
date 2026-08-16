# SECURITY.md — Security Posture

This repo is a collection of markdown instruction files. It has no runtime, no authentication, no database, and no network surface of its own, so most standard sections (auth, sessions, API security) don't apply directly to *this* repo — they apply to the projects that consume it. This document covers what actually matters here.

## What could go wrong in a rules-only repo

- **Secrets leaking into instruction files.** Rule/skill files sometimes reference environment setup (e.g. `rules/local-dev-env.md` mentions local PHP/MySQL paths) or `.env.example` sync practices (`rules/gemini-agent-rules`). These must stay generic — paths, tool names, conventions — and must never include real credentials, API keys, database passwords, or connection strings, even as examples.
- **Instructions that weaken security in consuming projects.** Because `CLAUDE.md` and the rule files are copied wholesale into other projects and followed literally by an AI agent, an insecure instruction here (e.g. "skip validation for speed," "disable CSRF for convenience") would propagate that weakness everywhere this repo is used. Every rule file is implicitly a security-relevant artifact.
- **Overly broad automation instructions.** `CLAUDE.md`'s "Session Behaviour" section instructs the agent to work autonomously without stopping for token-budget concerns. This is scoped to *implementation work*, not to bypassing the Engineering Constitution's explicit gates (destructive migrations, credential handling, force-push, etc.) — those confirmation requirements stand regardless of autonomy settings.

## Standing security rules carried by CLAUDE.md (enforced in every consuming project)

- OWASP Top 10 awareness: validate and sanitize all input, escape output, use parameterized queries.
- Passwords are hashed, never encrypted.
- Secrets and credentials live only in environment variables, never hardcoded, never committed.
- Migrations are additive-only, never destructive, and never applied without confirmation on a live system.
- Authorization decisions are always server-side; frontend permission checks are never trusted.
- File uploads are validated by type, size, MIME, and extension; stored outside the public directory when possible; given random filenames.
- Logs never contain passwords, tokens, API secrets, or unnecessary PII.
- Errors shown to users are friendly; detailed errors are logged internally, not exposed as stack traces.

## Contributor guidance for this repo specifically

- Before committing any new rule, skill, or doc file, scan it for anything that looks like a real credential, internal hostname, or personal data — even in an "example" — and remove it.
- Keep `.env`/`.env.example` guidance (see `rules/gemini-agent-rules`) generic: key names and sync discipline, never real values.
- If a future rule file needs to document a real incident for context, redact identifying details.

## Known limitations

- No automated secret-scanning is configured for this repo yet (no CI at all currently — see [DEVELOPMENT.md](DEVELOPMENT.md)). Manual review is the only current safeguard.
- No `.gitignore` exists yet, so there's no automatic protection against accidentally committing a local `.env` or similar file dropped into this repo by mistake. Tracked in [TODO.md](TODO.md).

## Incident response

Not applicable at this repo's current scale (no deployed service, no user data). If a secret is ever accidentally committed, treat it as compromised immediately: rotate the credential and remove it from history, rather than relying on a follow-up commit that merely deletes the line.
