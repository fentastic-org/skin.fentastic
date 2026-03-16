# CLAUDE.md – Claude Code Specific Guidance

**Read AGENTS.md first** — this adds Claude preferences.

## Thinking Process

- Think step-by-step: plan → upstream check → compatibility → edit proposal → diff.
- Conservative: minimal changes, explain every addition/removal.
- When v21 migration: state tag (v21-safe / v22-only) + upstream comparison.

## Output Format

- Use ```xml for code blocks.
- Edits:
  1. File path
  2. Line numbers + context (5–10 lines)
  3. ```diff before → after

     ```
  4. Why + v21 safety
- Propose one focused change → ask: "Apply? Adjustments?"

## Kodi XML Reminders

- Case-sensitive, whitespace-sensitive in places — precise indentation.
- Prefer <include> over inline repeats.
- Cross-check infobools/conditions in Variables.xml first.

## Memory Tips

- If pattern repeats → suggest adding to AGENTS.md.
- Use concise language — avoid redundancy.

Keep responses incremental and focused.
