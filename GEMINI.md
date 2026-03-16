# GEMINI.md — Instructions for Gemini CLI / Gemini Code Assist

Read AGENTS.md first for core project rules.

## Commit Message Style (Primary Use)

When generating commit messages:

- Follow Conventional Commits strictly: type(scope): description
  - Types: feat, fix, refactor, style, docs, chore, perf, test, build, ci, revert
  - Scope: optional, e.g. (home), (view), (widget), (migration)
- First line: max 72 chars, imperative mood
- Body: explain **what** changed + **why** (especially for migration/deprecation)
- Footer: reference TODO.md item or upstream commit if relevant
- Example:
  feat(home): add custom widewall view
  refactor: replace deprecated ListItem.Icon (v21-safe)

## General Gemini Behavior

- Be concise — prefer short, accurate answers.
- For XML: output clean, indented code blocks.
- When unsure about v21 compatibility → flag it clearly and suggest checking upstream raw file.

Use bullet points for lists.
Prioritize speed and clarity.
