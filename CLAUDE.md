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

https://github.com/xbmc/xbmc/tree/master/addons/skin.estuary

Fetch the relevant upstream file(s) and compare before applying changes to this skin. Do not assume migration advice (e.g. from Kodi changelogs or wiki) can be applied as a blanket find-and-replace — verify against Estuary's actual implementation.

**Do NOT fetch `https://github.com/xbmc/xbmc/tree/master/addons/skin.estuary/xml`** — this GitHub tree page will cause the LLM to get stuck. Instead, fetch individual raw files directly, e.g. `https://raw.githubusercontent.com/xbmc/xbmc/master/addons/skin.estuary/xml/Home.xml`.
