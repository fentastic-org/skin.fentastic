# FENtastic Skin — Claude Code Instructions

FENtastic is a community-maintained Kodi skin, built as a MOD of the default Estuary skin. It is pure XML — no build step, no compilation. The skin targets Kodi v21 (Omega), with v22 (Piers) migration in progress (see `TODO.md`).

## Project Layout

- `xml/` — All skin window and include definitions (122 files). This is where all UI work happens.
- `colors/` — Color theme values (`defaults.xml`).
- `themes/` — Curial and flat theme overrides (buttons, dialogs, overlays).
- `media/` — Icons, images, and overlay graphics used by the skin.
- `fonts/` — TrueType fonts (Noto, Roboto).
- `language/` — `.po` translation files for 77 languages.
- `playlists/` — Pre-configured Kodi smart playlists (`.xsp`).
- `addon.xml` — Addon manifest. Current API target: `xbmc.gui` 5.17.0 (v21). Helper dependency: `script.fentastic.helper`.

## Upstream Reference (Required Before Changes)

FENtastic is an Estuary MOD. Before applying any change based on Kodi migration notes, deprecations, or TODO items, **always fetch and compare the upstream Estuary file first**:

- Upstream repo: `https://github.com/xbmc/xbmc/tree/master/addons/skin.estuary`
- Fetch raw files directly, e.g.:
  `https://raw.githubusercontent.com/xbmc/xbmc/master/addons/skin.estuary/xml/Home.xml`

**Do NOT fetch the GitHub tree page** (`https://github.com/xbmc/xbmc/tree/master/addons/skin.estuary/xml`) — it will stall the agent. Always use raw file URLs.

**Important:** Upstream Estuary's `master` branch tracks Kodi's development branch and targets future Kodi versions (currently v22 Piers / `xbmc.gui` 5.18.0). FENtastic targets **Kodi v21 (Omega)** for stability. Use upstream as a reference for how Estuary handles things, but do not pull in v22-only patterns or infolabels. If upstream has migrated away from a v21 pattern, keep the v21 version in FENtastic unless explicitly instructed otherwise.

Do not apply Kodi changelog or wiki advice as a blanket find-and-replace. Verify against what Estuary actually does, and only adopt changes that are compatible with Kodi v21.

## Key Conventions

- **Skin settings** are stored as Kodi skin strings/booleans (e.g., `Skin.HasSetting(...)`, `Skin.String(...)`). Widget config lives in numbered skin settings (`widget_1_type`, `widget_1_path`, etc.).
- **Includes** (`xml/Includes*.xml`) define reusable components referenced by `<include>` tags across window files. New shared components go here.
- **Variables** (`xml/Variables.xml`) centralizes infolabel logic and conditional values. Check here before duplicating infolabel logic inline.
- **Custom windows** (`xml/script-fentastic-*.xml`, `xml/Custom_*.xml`) are FENtastic-specific UI — not present in Estuary.
- **View types** (`xml/View_*.xml`) define the media browsing layouts. FENtastic adds WideWall and WideInfoWall on top of Estuary's defaults.

## Kodi v22 Migration (See TODO.md)

The `TODO.md` tracks all migration items with per-item compatibility flags:

- `v21-safe` — can be done now, backward-compatible
- `v22-only` — will break on v21; hold until we target v22

**Do not apply v22-only changes** unless explicitly instructed. The API target in `addon.xml` is still `5.17.0` (v21).

## What Not to Do

- Do not replace `ListItem.Icon` with `ListItem.Art(thumb)` across the board — it is not a simple swap (see `TODO.md`).
- Do not apply weather infolabel migration (`Weather.Data()`) until v22 is targeted.
- Do not bump `xbmc.gui` past `5.17.0` without explicit instruction.
- Do not create build scripts, CI config, or package files — this project has none by design.
- Do not add or modify `language/` files directly for new strings; add `<string>` entries to the English source and note that translations follow separately.

## Version Bumping

This project follows Semantic Versioning (MAJOR.MINOR.PATCH):

    MAJOR — breaking changes (removed features, incompatible API changes, dropped Kodi version support)
    MINOR — new features, new functionality (new widgets, new menu options, new integrations)
    PATCH — bug fixes, code cleanup, deprecation updates, cosmetic changes

When making changes that warrant a version bump:

    Check last_updated_version.txt to know the current version
    Determine the appropriate bump level based on the changes made
    Update the version attribute in addon.xml
    Update last_updated_version.txt to match

The version in addon.xml is what Kodi uses to detect updates. The last_updated_version.txt file exists so you can quickly check the current version without parsing XML.
