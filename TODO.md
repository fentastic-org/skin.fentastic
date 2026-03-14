# TODO

Outstanding items left by the previous developer.

## UI / Cosmetic

- [ ] **Find way to apply diffuse texture to notification avatar**
  `xml/DialogNotification.xml:28` — The notification dialog's avatar image (control id 400) needs a diffuse texture applied.

- [ ] **Add new MPAA icons and playback info message**
  `xml/VideoOSD.xml:17` — Add new MPAA rating icons and show an info message at the start of playback displaying title, year, MPAA rating, audio codec, and video codec.

## Home Screen

- [ ] **Add sideblade panel for widget/section management**
  `xml/Home.xml:832` — Add a sideblade panel allowing direct editing of widgets, hiding sections, and other shortcuts from the home screen.

- [ ] **Add one-click actions to category labels**
  `xml/Includes_Home.xml:13` — Add one-click functionality for Trakt Manager, viewing trailers, etc. on home screen category labels.

## Data / Variables

- [ ] **Fix seasons not showing release year**
  `xml/Variables.xml:963` — The season-level info line is missing the release year variable (e.g. `$VAR[RI_Year]`) that other DB types include.
