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
