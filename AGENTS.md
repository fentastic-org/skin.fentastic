# AGENTS.md – Instructions for All AI Coding Agents

Vendor-neutral context file. Read this first. Applies to Claude Code, Cursor, Gemini CLI, Copilot agents, etc.

## Project Overview

FENtastic is a pure-XML community MOD of Kodi's Estuary skin.  
Targets **Kodi v21 (Omega)** only — addon.xml: xbmc.gui 5.17.0  
No build/compilation step. XML + media only.

## Upstream Reference – Always Check First

Before API/deprecation/migration changes:

- Fetch **raw** upstream Estuary file:  
  https://raw.githubusercontent.com/xbmc/xbmc/master/addons/skin.estuary/xml/{filename}.xml
- Never use tree/list pages.
- Upstream master = v22 dev — reference for structure/style only.
- Keep v21 patterns unless explicitly switching to v22 target.

## Compatibility Rules

See TODO.md (tagged v21-safe / v22-only).

- Never apply v22-only changes (e.g. Weather.Data(), unsafe ListItem.Art swaps).
- No blanket replacements — verify upstream v21 behavior.
- Never bump xbmc.gui past 5.17.0 without approval.

## Prohibitions

- No build scripts, CI, package.json, tsconfig, etc.
- No direct .po edits — add English <string> only.
- Skin-only — no Python/JS addons.

## Versioning

Follow SemVer (MAJOR breaking, MINOR features, PATCH fixes).

- Read last_updated_version.txt first.
- On bump: update addon.xml version, last_updated_version.txt, changelog.txt.

## Workflow Expectations

- Reuse Includes\*.xml / Variables.xml — avoid duplication.
- Widgets: numbered skin settings (widget_1_type etc.).
- XML edits: show file, line numbers, context, ```diff before/after.
- If v21 risk unclear: propose + upstream diff + ask.

Last updated: March 2026
