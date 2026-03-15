# Agents

## Upstream Reference

FENtastic is an Estuary MOD. Before making changes based on Kodi migration notes, deprecations, or TODO items, always check how the upstream Estuary skin handles it first:

https://github.com/xbmc/xbmc/tree/master/addons/skin.estuary

Fetch the relevant upstream file(s) and compare before applying changes to this skin. Do not assume migration advice (e.g. from Kodi changelogs or wiki) can be applied as a blanket find-and-replace — verify against Estuary's actual implementation.

**Do NOT fetch `https://github.com/xbmc/xbmc/tree/master/addons/skin.estuary/xml`** — this GitHub tree page will cause the LLM to get stuck. Instead, fetch individual raw files directly, e.g. `https://raw.githubusercontent.com/xbmc/xbmc/master/addons/skin.estuary/xml/Home.xml`.
