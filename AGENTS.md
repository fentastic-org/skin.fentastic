# AGENTS.md — Universal Instructions for All AI Coding Agents

This file provides persistent context and rules for **any** AI coding agent (Claude Code, Cursor, Gemini CLI, Codex, Windsurf, etc.).  
Every agent MUST read and obey these guidelines in every session.

## Project Identity

- FENtastic is a **community-maintained MOD** of Kodi's default Estuary skin.
- Pure XML only — **no** build step, no compilation, no JS/TS/Python.
- Targets **Kodi v21 (Omega)** — addon.xml API: `xbmc.gui` **5.17.0**
- **Do NOT** assume or introduce v22 (Piers) / 5.18.0 APIs, infolabels, or patterns unless explicitly instructed to switch target version.

## Upstream Estuary — Source of Truth

Before any change touching Kodi APIs, deprecations, controls, infolabels, or TODO items:

1. ALWAYS fetch and compare the **current upstream Estuary file** from raw URLs:
   - https://raw.githubusercontent.com/xbmc/xbmc/master/addons/skin.estuary/xml/Home.xml
   - (replace filename as needed)
2. Never fetch GitHub tree/list pages — they stall agents.
3. Upstream `master` tracks **v22 development** → use only for structure, style, and include patterns.
4. If upstream removed/migrated a v21-compatible pattern → **keep the v21 version** in FENtastic unless human says to target v22.

## Compatibility & Migration Rules

- Full migration list → `TODO.md` (items tagged `v21-safe` or `v22-only`).
- **Never apply v22-only changes** (e.g. `Weather.Data()`, certain `ListItem.Art()` patterns).
- No blanket find-and-replace — always verify against upstream Estuary behavior on v21.
- Never bump `xbmc.gui` version in `addon.xml` without explicit human approval.

## Hard Prohibitions

- Do not create build scripts, CI workflows, package.json, tsconfig, etc.
- Do not modify or add `.po` translation files — only add English `<string>` entries.
- Do not assume or edit non-skin files (no helper addons, no Python).

## Versioning Rules

Follow Semantic Versioning (see README / Kodi wiki):

- Read `last_updated_version.txt` first to know current version.
- Classify change: MAJOR (breaking), MINOR (features), PATCH (fixes/cleanup).
- When bumping: propose updates to `addon.xml` @version, `last_updated_version.txt`, `changelog.txt`.

## General Expectations

- Prefer reusing `Includes*.xml`, `Variables.xml` — avoid duplicating infolabel/conditional logic.
- Widget / skin settings → use numbered pattern (`widget_1_type`, `widget_1_path`, etc.).
- XML changes → show line numbers, surrounding context, before/after diff.
- If v21 compatibility is unclear → propose change + upstream diff + ask for confirmation.

Last updated: March 2026
