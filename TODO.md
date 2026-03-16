# TODO

## Kodi v21 (Omega) Leftovers

The original developer migrated the skin from Kodi v20 (Nexus) to v21 (Omega). Most migration was completed — `DialogFavourites.xml` was replaced with `MyFavourites.xml`, `DialogColorPicker.xml` was added, `Player.Cutlist` was migrated to `Player.Editlist`/`Player.Cuts`, and old boolean syntax (`StringCompare`, `SubString`, `IntegerGreaterThan`) was replaced with modern equivalents. Two items remain:

- [ ] **Add `DialogVideoManager.xml`**
      Missing required window for Omega's Video Versions & Extras management feature. Window IDs: 12004 (`managevideoversions`), 12017 (`managevideoextras`). Without this file, the video version/extras manager has no skin-defined layout and falls back to Kodi's default.
      **Upstream:** Estuary has `DialogVideoManager.xml` with list ID 50 and button IDs 21–28 (Play, Add version, Add extras, Rename, Set default, Remove, Choose art, Rename extra).

- [ ] **Remove `System.HasCMS` reference**
      `Custom_1101_SettingsList.xml:56` — Used as a `<visible>` condition for a settings item. This boolean is not present in upstream Estuary and appears to be a leftover from Nexus. The referenced setting item is likely never shown.

## Kodi v22 (Piers) Migration

Upstream Estuary (v4.1.0) has fully migrated to v22 — targeting `xbmc.gui` 5.18.0.

> Items marked **`v21-safe`** can be done now — they are backward-compatible with Kodi v21 (Omega).
> Items marked **`v22-only`** require Kodi v22 and would break or lose functionality on v21.

### Breaking

- [ ] **Bump `xbmc.gui` from `5.17.0` to `5.18.0`** · `v22-only`
      `addon.xml:5` — Required to target Kodi v22.

- [ ] **Migrate weather infolabels to `Weather.Data()` interface** · `v22-only`
      53 occurrences across 5 files. Two kinds of changes: 1. **Direct infolabels** (5 occurrences) — replace old-style weather infolabels: - `Weather.Location` → `Weather.Data(Current.Location)` — `Home.xml:574` - `Weather.Conditions` → `Weather.Data(Current.Condition)` — `Home.xml:585`, `MyWeather.xml:127` - `Weather.Temperature` → `Weather.Data(Current.Temperature)` — `Home.xml:596`, `MyWeather.xml:121` 2. **`Window(weather).Property(...)` → `Weather.Data(...)`** (48 occurrences): - `Home.xml` — 7 - `Includes_Home.xml` — 31 - `MyWeather.xml` — 9 - `Variables.xml` — 1
      **Upstream:** Estuary has fully migrated. Also uses new keys: `Current.FeelsLike`, `Current.Wind`, `Current.Humidity`, `Current.Precipitation`, `Today.Sunrise`, `Today.Sunset`, `WeatherProvider`, `Daily.IsFetched`, `Hourly.IsFetched`.

- [ ] **Remove manual `System.TemperatureUnits` appending** · `v22-only`
      4 occurrences across 3 files. Kodi v22 appends temperature units automatically — keeping manual appending causes double units. - `Includes.xml:1022` - `MyWeather.xml:127` - `Includes_Home.xml:2024` (×2, same line)
      **Upstream:** Estuary has removed all `System.TemperatureUnits` references.

- [ ] **Verify full-screen background coverage** · `v21-safe`
      Kodi v22 changed how the screen is cleared at frame start. The skin must explicitly draw over the entire screen or set a background color, otherwise undefined/garbage content may appear in undrawn areas.

### Deprecated (still work, will be removed later)

- [ ] **`ListItem.Icon` deprecation** · do not migrate yet
      48 occurrences across 17 files. Deprecated in v22 but not removed. **Not a simple find-and-replace** — `ListItem.Art(thumb)` only works where items have actual thumbnail artwork. System items (file browser, profiles, addon lists, etc.) only have icons, so `ListItem.Art(thumb)` returns empty for them.
      **Upstream:** Estuary still uses `ListItem.Icon` (11 in Variables.xml, 2 in Includes.xml) alongside `ListItem.Art(thumb)`. No wholesale migration has occurred. Do not migrate ahead of upstream.

- [ ] **`ListItem.PictureColour` and `ListItem.PictureProcess` deprecation** · do not migrate yet
      `MyPics.xml` — Both deprecated in v22, no direct replacement.
      **Upstream:** Estuary still uses both in MyPics.xml. Do not migrate ahead of upstream.

### Optional Enhancements (new v22 features)

- [ ] **Update language strings 31112 and 31115** · `v21-safe`
      `Custom_1101_SettingsList.xml:61,69` + language files — FENtastic uses "Toggle audio stream" (#31112) and "Toggle subtitle" (#31115). Upstream changed these to "Audio streams" and "Subtitles streams".

- [ ] **Add codec variables for new audio formats** · `v21-safe`
      Upstream added `AudioCodecVar` and `ObjectAudioTypeVar` to Variables.xml. New codec identifiers: `dtshd_ma_x` (DTS:X), `eac3_ddp_atmos` (Dolby Digital Plus Atmos), `truehd_atmos` (TrueHD Atmos), `dtshd_ma_x_imax` (DTS:X IMAX), and AAC variants. `AudioCodecVar` maps to display names ("DTS-HD MA", "Dolby Digital+", "Dolby TrueHD") while `ObjectAudioTypeVar` maps spatial formats ("DTS:X", "Dolby Atmos"). Additive — v21 ignores unknown values.

- [ ] **Add support for parental rating infolabels** · `v22-only`
      `ListItem.ParentalRatingIcon`, `ListItem.ParentalRatingSource`, `VideoPlayer.ParentalRatingCode`, `VideoPlayer.ParentalRatingIcon` — New infolabels for parental rating display. These don't exist in v21.
      **Upstream:** Estuary does not use any of these yet.

- [ ] **Consider `imagefilter` / `diffusefilter` tags** · `v22-only`
      New image control tags with values `linear` (smooth) or `nearest` (pixelated) for texture scaling quality. Unknown tags may cause issues on v21.
