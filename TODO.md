# TODO

## Kodi v22 (Piers) Migration

Upstream Estuary (v4.1.0) has fully migrated to v22 — targeting `xbmc.gui` 5.18.0.

> Items marked **`v21-safe`** can be done now — they are backward-compatible with Kodi v21 (Omega).
> Items marked **`v22-only`** require Kodi v22 and would break or lose functionality on v21.

---

### v22-only — Requires Kodi v22

These changes use new v22 APIs, infobools, or controls that don't exist in v21.

#### Required (breaking)

- [ ] **Bump `xbmc.gui` from `5.17.0` to `5.18.0`**
      `addon.xml:5` — Required to target Kodi v22.

- [ ] **Migrate weather infolabels to `Weather.Data()` interface**
      53 occurrences across 5 files. 1. **Direct infolabels** (5 occurrences): `Weather.Location` → `Weather.Data(Current.Location)` — `Home.xml:574`; `Weather.Conditions` → `Weather.Data(Current.Condition)` — `Home.xml:585`, `MyWeather.xml:127`; `Weather.Temperature` → `Weather.Data(Current.Temperature)` — `Home.xml:596`, `MyWeather.xml:121`. 2. **`Window(weather).Property(...)` → `Weather.Data(...)`** (48 occurrences): `Home.xml` — 7, `Includes_Home.xml` — 31, `MyWeather.xml` — 9, `Variables.xml` — 1.
      **Upstream:** Also uses new keys: `Current.FeelsLike`, `Current.Wind`, `Current.Humidity`, `Current.Precipitation`, `Today.Sunrise`, `Today.Sunset`, `WeatherProvider`, `Daily.IsFetched`, `Hourly.IsFetched`.

- [ ] **Remove manual `System.TemperatureUnits` appending**
      4 occurrences across 3 files. Kodi v22 appends temperature units automatically — keeping manual appending causes double units. `Includes.xml:1022`, `MyWeather.xml:127`, `Includes_Home.xml:2024` (×2).
      **Upstream:** Estuary has removed all `System.TemperatureUnits` references.

- [ ] **Add weather loading spinner**
      `Home.xml` — New loading spinner group (visible: `!Weather.IsFetched + Weather.IsUpdating`) with rotating `loading.png` animation. Uses v22-only infobools.

#### Structural (major rework)

- [ ] **Redesign MediaFlags from images to text-based rendering**
      Major change across many files. The old image-based `InfoFlag`/`MediaFlag` system (PNG icons) is replaced with text-rendered `<button>` controls using `font_flag` and `width=auto`. Bar height changed from 70 to 40. Now works in multiple contexts (library, fullscreen video, music visualization, PVR recordings). New flags: Dolby Atmos, DTS:X, BPM, Samplerate/kHz, BitRate/kbps, BitsPerSample/bit, RDS.
      Files affected: `Includes.xml`, `Home.xml`, `DialogVideoInfo.xml`, `MyVideoNav.xml`, `MyMusicNav.xml`, `MyPlaylist.xml`, and more.

- [ ] **Rename settings system: SettingsList → SettingsDialog**
      `Custom_1101_SettingsList.xml` renamed to `Custom_1101_SettingsDialog.xml`. `Custom_1105_MusicOSDSettings.xml` removed (merged into new `Includes_SettingsDialog.xml`). References changed from `settingslist_content`/`settingslist_header` to `settingsdialog_content`/`settingsdialog_header` throughout `Timers.xml`, `VideoOSD.xml`, `MusicOSD.xml`, `GameOSD.xml`.

- [ ] **Add `Includes_SettingsDialog.xml`**
      New include file for the settings dialog system. Contains per-category widget toggle includes, stream selection, video/music/game/3D settings dialogs.

- [ ] **Extract constants to resolution-aware files**
      All constants moved from inline in `Includes.xml` to `Constants_1080.xml` / `Constants_720.xml`, conditionally loaded via `System.ScreenHeight`. New constant: `MediaFlagBorder` (2 at 1080p, 1.5 at 720p).

- [ ] **Restructure `DialogVideoInfo.xml`**
      Button bar changed from `<grouplist>` with `InfoDialogButton`/`InfoDialogToggleButton` includes to a `<list>` with `<content>` items using `SendClick()` to trigger hidden buttons. Default control changed. Plot now uses `$VAR[VideoInfoPlotVar]` (tagline + plot combined, season show plot fallback). `VideoInfoBottomLabelVar` removed.

- [ ] **Rewrite `DialogPVRInfo.xml`**
      Complete rewrite — now matches `DialogVideoInfo` layout pattern with poster/logo area, plot textbox, and structured metadata panel (`InfoDialogMetadata` include). New buttons: fanart viewer (id=102), director search (id=13). MediaFlags bar added.

- [ ] **Swap `DialogBackgroundCommons` header/body tints**
      `Includes.xml` — Header now uses `dialog_header_tint` colordiffuse with `height=70`, body uses `dialog_tint`. Previously reversed.

- [ ] **Add new stream selection dialogs**
      `dialogselectvideo`, `dialogselectaudio`, `dialogselectsubtitle` replace old `selectvideoversion`/`selectvideoextra` windows. Each shows stream properties (codec, resolution, bitrate, HDR, FPS, channels, language). New variables: `StreamCodecVar`, `StreamChannelsVar`, `StreamHDRTypeVar`, `StreamBitrateVar`.

- [ ] **Replace `AudioChannelsVar` with builtin**
      `Variables.xml` — Manual channel count mapping (0→0.0, 1→1.0, etc.) replaced with `AudioChannels(DefaultLayout)` / `MusicPlayer.Channels(DefaultLayout)` builtins.

- [ ] **Update codec variables for dual-context (library + playback)**
      `Variables.xml` — `VideoCodecVar`, `VideoResolutionTypeVar`, `VideoHDRTypeVar` (renamed from `VideoHDRVar`), `AudioCodecVar`, `AudioChannelsVar` now work in both ListItem and VideoPlayer/MusicPlayer contexts via `Window.IsActive(fullscreenvideo)` / `Window.IsActive(visualisation)` conditions. New `ObjectAudioTypeVar` for Dolby Atmos / DTS:X / DTS:X IMAX.

#### New windows / views

- [ ] **Add `MyPVRProviders.xml`**
      New PVR Providers browser window using existing PVR list/info panel infrastructure with `BreadcrumbsPVRProvidersVar`.

- [ ] **Add `View_504_MediaList.xml`**
      New fixedlist view (id=504) for video assets (`videoassets`, `videoversions`, `videoextras`). Shows label, duration, media info, watched icon.

- [ ] **Add video assets support**
      New `videoasset_true` expression for `Container.Content(videoassets | videoversions | videoextras)`. `BreadcrumbsVideoAssetTypeVar` variable. Overlay icons (`HasVideoVersions`, `HasVideoExtras`) hidden when already browsing assets. Affects `View_51_Poster`, `View_53_Shift`, `View_54_InfoWall`.

#### New PVR features

- [ ] **Add new PVR infobools and multi-instance support**
      New infobools: `ListItem.TitleExtraInfo`, `ListItem.EpisodePart`, `ListItem.PVRClientName`, `ListItem.PVRInstanceName`, `ListItem.MediaProviders`, `ListItem.ChannelNumberLabel`, `PVR.ClientCount`, `Player.IsLive`. Used throughout `Includes_PVR.xml`, `Variables.xml`, `Home.xml`.

- [ ] **Update `DialogPlayerProcessInfo.xml`**
      New fields: HDR type (`VideoPlayer.HdrType`), audio language (`VideoPlayer.AudioLanguage`), cache level (`Player.CacheLevel`), CPU temperature (`System.CPUTemperature`). Layout widths and positions adjusted.

#### Optional enhancements

- [ ] **Add support for parental rating infolabels**
      `ListItem.ParentalRatingIcon`, `ListItem.ParentalRatingSource`, `VideoPlayer.ParentalRatingCode`, `VideoPlayer.ParentalRatingIcon` — New infolabels for parental rating display.
      **Upstream:** Estuary does not use any of these yet.

- [ ] **Consider `imagefilter` / `diffusefilter` tags**
      New image control tags with values `linear` (smooth) or `nearest` (pixelated) for texture scaling quality. Unknown tags may cause issues on v21.

- [ ] **Add game controller preview to settings**
      `DialogSettings.xml` — New `<control type="gamecontroller" id="100">` for animated controller preview (290x290).

- [ ] **Update subtitle language variable**
      `Variables.xml` — `ActiveVideoPlayerSubtitleLanguage` expanded from 2 to 4 values: no subtitles ("N/A"), disabled ("Off"), with language name (uppercase), without language name ("Unknown"). New `ActiveVideoPlayerAudioLanguage` variable.

---

### Deprecated (still work in v22, will be removed later)

- [ ] **`ListItem.Icon` deprecation** · do not migrate yet
      48 occurrences across 17 files. Deprecated in v22 but not removed. **Not a simple find-and-replace** — `ListItem.Art(thumb)` only works where items have actual thumbnail artwork. System items (file browser, profiles, addon lists, etc.) only have icons, so `ListItem.Art(thumb)` returns empty for them.
      **Upstream:** Estuary still uses `ListItem.Icon` (11 in Variables.xml, 2 in Includes.xml) alongside `ListItem.Art(thumb)`. No wholesale migration has occurred. Do not migrate ahead of upstream.

- [ ] **`ListItem.PictureColour` and `ListItem.PictureProcess` deprecation** · do not migrate yet
      `MyPics.xml` — Both deprecated in v22, no direct replacement.
      **Upstream:** Estuary still uses both in MyPics.xml. Do not migrate ahead of upstream.

---

### Notes

- Upstream media assets switched from compiled `.xbt` texture bundles (`Textures.xbt`, `curial.xbt`, `flat.xbt`) to loose PNG files. This may affect FENtastic's build/packaging approach.
- Upstream `Includes_Home.xml` weather icons changed from `<image>` to `<multiimage>` control type.
- Two theme textures changed: `themes/curial/lists/panel.png` and `themes/curial/overlays/shadow.png`.
- Two language directories removed in v22: `resource.language.fil` and `resource.language.kn_in`.
