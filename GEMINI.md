# GEMINI.md – Gemini CLI Context

See AGENTS.md for core project rules.

## Commit Message Conventions

Use Conventional Commits strictly:

- Format: type(scope): short description (max 72 chars, imperative)
- Types: feat | fix | refactor | style | docs | chore | perf | test | build | ci | revert
- Scope: optional (e.g. home, view, widget, migration)
- Body: What changed + why (esp. for deprecations/migrations)
- Footer: Refs (e.g. TODO.md item, upstream PR)
- Before committing, always review `git diff HEAD` to understand the changes.

Examples:

- feat(home): add custom widewall view layout
- fix(widget): correct numbered setting fallback (v21-safe)
- refactor: align ListItem usage with upstream Estuary (keep v21 compat)

## General Preferences

- Concise, bullet-point responses when possible.
- For XML: clean, indented blocks.
- Flag v21 risks clearly.

Use for commit generation via Gemini CLI / Git integrations.
