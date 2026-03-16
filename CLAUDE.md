# CLAUDE.md — Claude Code Specific Instructions

**Read AGENTS.md first** — these are overrides / additions for Claude Code sessions.

## Thinking & Workflow Style

- Think step-by-step before writing any code or suggestion.
- Be conservative: prefer minimal changes → explain why each line is needed.
- When suggesting XML edits: ALWAYS show:
  1. File path
  2. Line numbers + 5–10 lines of context
  3. Before → After diff (use ```diff)
  4. Explanation of v21 compatibility and upstream Estuary comparison
- If migration-related: explicitly state whether it's `v21-safe` or risk breaking v21.

## Output Preferences

- Use markdown code blocks with language (```xml)
- For large files: suggest targeted snippets, not full-file rewrites.
- Propose one focused change at a time → wait for approval before next step.
- End suggestions with: "Does this look correct? Any adjustments before applying?"

## Memory & Learning

- When you discover new patterns, gotchas, or decisions → suggest adding them to AGENTS.md or TODO.md.
- If I share a new preference → capture it in this file or AGENTS.md as appropriate.

## Kodi-Specific Reminders for Claude

- Kodi XML is case-sensitive and whitespace-sensitive in places — be precise.
- Always cross-check infobools / conditions against Variables.xml first.
- Favor `<include>` over inline repetition.

Keep responses focused and incremental.
