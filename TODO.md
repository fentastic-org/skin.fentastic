# TODO

Outstanding items left by the previous developer.

## UI / Cosmetic

- [x] **Find way to apply diffuse texture to notification avatar**
  `xml/DialogNotification.xml:28` — Applied `masks/focus.png` diffuse texture to the avatar image control.

- [ ] **Add new MPAA icons and playback info message**
  `xml/VideoOSD.xml:17` — Add new MPAA rating icons and show an info message at the start of playback displaying title, year, MPAA rating, audio codec, and video codec.

## Home Screen

- [ ] **Add sideblade panel for widget/section management**
  `xml/Home.xml:832` — Add a sideblade panel allowing direct editing of widgets, hiding sections, and other shortcuts from the home screen.

- [ ] **Add one-click actions to category labels**
  `xml/Includes_Home.xml:13` — Add one-click functionality for Trakt Manager, viewing trailers, etc. on home screen category labels.

## Data / Variables

- [x] **Fix seasons not showing release year**
  `xml/Variables.xml:963` — Added `$VAR[RI_Year]` to the season info line, matching movie and tvshow patterns.

## Kodi v22 (Piers) Migration

Breaking changes, deprecations, and required updates for Kodi v22 compatibility.

> Items marked **`v21-safe`** can be done now — they are backward-compatible with Kodi v21 (Omega).
> Items marked **`v22-only`** require Kodi v22 and would break or lose functionality on v21.

### Breaking

- [ ] **Bump `xbmc.gui` dependency from `5.17.0` to `5.18.0`** · `v22-only`
  `addon.xml:5` — Required to target Kodi v22.

- [ ] **Migrate weather infolabels to `Weather.Data()` interface** · `v22-only`
  `xml/Home.xml:574-643`, `xml/Includes_Home.xml:1980-2021`, `xml/MyWeather.xml:121-207`, `xml/Variables.xml:464`, `xml/Includes.xml:1022` — `Weather.Location`, `Weather.Conditions`, `Weather.Temperature` must migrate to `Weather.Data(Current.Location)`, `Weather.Data(Current.Condition)`, `Weather.Data(Current.Temperature)`. All `Window(weather).Property(...)` calls should migrate to `Weather.Data(...)`.

- [ ] **Remove manual `System.TemperatureUnits` appending for weather** · `v22-only`
  `xml/Includes.xml:1022`, `xml/MyWeather.xml:127`, `xml/Includes_Home.xml:2012` — Kodi v22 now appends temperature units automatically. Keeping manual appending will cause double units.

- [ ] **Add new stream selection dialogs (`DialogSelectAudio.xml`, `DialogSelectSubtitle.xml`)** · `v21-safe`
  Window IDs 12301 and 12302 — New required windows for audio/subtitle stream selection. The old `SelectVideoVersion` (12015) and `SelectVideoExtra` (12016) windows have been removed and replaced by these. The new files can be added now (v21 ignores them), but do not remove the old windows until v22 is targeted.

- [ ] **Verify full-screen background coverage** · `v21-safe`
  Kodi v22 changed how the screen is cleared at frame start. The skin must explicitly draw over the entire screen or set a background color, otherwise undefined/garbage content may appear in undrawn areas.

### Deprecated (still work, will be removed later)

- [ ] **Replace `ListItem.Icon` with `ListItem.Art(thumb)`** · `v21-safe`
  Used in 17 XML files (30+ occurrences) including `DialogAddonInfo.xml`, `FileBrowser.xml`, `LoginScreen.xml`, `Includes_Home.xml`, `GameOSD.xml`, `EventLog.xml`, `DialogPVRInfo.xml`, `DialogPVRGroupManager.xml`, `MyPVRGuide.xml`, and others. `ListItem.Icon` is deprecated in v22. `ListItem.Art(thumb)` works on v21 and earlier.

- [ ] **Replace `ListItem.PictureColour` and `ListItem.PictureProcess`** · `v22-only`
  `xml/MyPics.xml:97,189` — Both are deprecated in v22 with no direct replacement. Removing them now would lose functionality on v21.

### Optional Enhancements (new v22 features)

- [ ] **Update language strings 31112 and 31115** · `v21-safe`
  `xml/Custom_1101_SettingsList.xml:61,69` + all language files — Upstream Estuary changed 31112 from "Toggle audio stream" to "Audio streams" and 31115 from "Toggle subtitle" to "Subtitles streams". Review if the skin's values should match.

- [ ] **Add support for new audio codec values** · `v21-safe`
  New codec identifiers in v22: `dtshd_ma_x` (DTS:X), `eac3_ddp_atmos` (Dolby Digital Plus Atmos), `truehd_atmos` (TrueHD Atmos), and AAC variants. Add corresponding icons/labels if the skin displays codec info. Additive change — v21 simply won't trigger the new values.

- [ ] **Add support for new parental rating infolabels** · `v22-only`
  `ListItem.ParentalRatingIcon`, `ListItem.ParentalRatingSource`, `VideoPlayer.ParentalRatingCode`, `VideoPlayer.ParentalRatingIcon` — New infolabels for parental rating display. Could enhance the MPAA icons TODO item above. These infolabels don't exist in v21.

- [ ] **Consider using `imagefilter` / `diffusefilter` tags** · `v22-only`
  New image control tags `<imagefilter>` and `<diffusefilter>` with values `linear` (smooth) or `nearest` (pixelated). Useful for controlling texture scaling quality. Unknown tags may cause issues on v21.
