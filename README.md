> [!WARNING]
> This is a **community fork** of [ivarbrandt's FENtastic skin](https://github.com/ivarbrandt/skin.fentastic). The original project is no longer actively maintained. This fork aims to continue development with community-requested features and improvements.

# FENtastic Skin for Kodi

FENtastic is a modded version of the default Estuary skin, specifically designed for FEN users. It features a modern UI, custom viewtypes, customizable widgets, and a new default color theme.

---

## What's New in the Community Fork

Since [morgann1](https://github.com/morgann1) took over maintenance of FENtastic, the following changes have been made:

- **One-click quick actions on widgets** — press the Info key on any widget to access actions like Trakt Manager, trailers, and more
- **Sideblade management panel** — manage widgets and sections directly from the home screen sidebar
- **Search provider selection dialog** — switch between search providers (FEN, Umbrella, etc.) with a dedicated picker
- **Experiments tab** — replaces the old Extra info tab in skin settings for testing new features
- **Seasons release year fix** — seasons now correctly display their release year
- **HDR/video processing labels** — added HDR10+, Dolby Vision, HDR10, HLG, bit depth, and tone mapping info to player overlay
- **Code cleanup** — refactored code structure, cleaned up font licenses, and improved overall maintainability
- **Rebranded to "FENtastic (Community)"** — to distinguish from the original upstream skin

---

## Features

- Modern UI experience with adjustments to pre-existing views
- 2 custom viewtypes: **WideWall** and **WideInfoWall**
- Customizable movie and show main menu items
- Customizable widgets and category widgets for movies, tvshows, and episodes
- Custom stacked widgets for movies, tvshows, and episodes
- Ratings displayed for movies, tvshows, seasons, and episodes
- InfoPanel for widgets with optional ratings display
- Custom search window with multi-category and Trakt list support
- Progress displayed for movies, tvshows, seasons, and episodes
- Advanced player info overlays (HDR10+, Dolby Vision, HDR10, HLG, bit depth, tone mapping)

---

## Screenshots

### UI Experience

|                                                        |                                                    |
| ------------------------------------------------------ | -------------------------------------------------- |
| ![Viewtypes Widelist](resources/images/viewtypes1.jpg) | ![Viewtypes List](resources/images/viewtypes2.jpg) |
| ![Viewtypes Widelist](resources/images/viewtypes3.jpg) | ![Viewtypes List](resources/images/viewtypes4.jpg) |

### Custom Viewtypes

![Viewtypes WideInfoWall](resources/images/viewtypes.jpg)

### Customizable Widgets

![Customizable Widgets](resources/images/customizable_widgets.jpg)

### Stacked Widgets

![Stacked Widgets](resources/images/stacked_widgets.jpg)

### Search Window

|                                                      |                                                       |
| ---------------------------------------------------- | ----------------------------------------------------- |
| ![Search Window](resources/images/search_window.jpg) | ![Search Window](resources/images/search_window1.jpg) |

### InfoPanel with Ratings

![InfoPanel](resources/images/infopanel.jpg)

---

## Download and Installation

### 1. Add the source

Go to **Settings > File Manager** and click **Add Source** at the bottom. Add the following source:

```
https://fentastic-org.github.io/repository.fentastic-org/
```

![Add Source](resources/images/add_source.jpg)

### 2. Install the repository

Go to **Settings > Addons > Install from zip file**, select the source you just added, and install `repository.fentastic-org-1.0.0.zip`.

![Install from zip](resources/images/install_from_zip.jpg)

### 3. Install the skin

Go to **Install from repository > fentastic-org's Repository > Look and feel > Skin > FENtastic** and install.

![Addon Info](resources/images/addon_info.jpg)

---

## Setup Guide

> [!TIP]
> On first install, go to **Settings > Interface > Configure skin... > Extra info > Setup Guide** for tips on setting up your main menu paths and widgets.

On first install, the home screen will be empty with the Movie and Show sections missing from the main menu.

![Empty Home Screen](resources/images/empty_home_screen.jpg)

### 1. Enable menu sections

Go to **Settings > Interface > Configure skin...** and navigate to **Main menu items**.

![Step 1](resources/images/step_1.jpg)

### 2. Toggle sections on

Click a menu item to toggle it on or off. Toggle the Movie/Show section to **on** and you'll see additional menu items appear.

> [!NOTE]
> Even with Movie/Show toggled on, they won't appear on the home screen until you set a main menu path.

![Step 2](resources/images/step_2.jpg)

### 3. Set main menu path

Click **Set main menu path** and choose any path within FEN (e.g., your Trakt movie/tvshow collection).

![Step 3](resources/images/step_3.jpg)

### 4. Configure widgets

Click **Set widgets** to configure up to 10 movie and 10 TV show widgets. For each widget you can set:

- **Path** to the content source
- **Label** for display
- **Display type** (Poster, Landscape, LandscapeInfo, or Category)
- **Stacked widget** option (when using Category display type)

![Step 4](resources/images/step_4.jpg)

### 5. Manage widgets

Click any configured widget to rearrange, rename, remake, change display type, or remove it. Main menu items can also be renamed, remade, or removed.

![Step 5](resources/images/step_5.jpg)

## License

This project is dual-licensed:

- **Code** — [GNU General Public License v2.0](LICENSE)
- **Artwork** — [Creative Commons Attribution-ShareAlike 4.0 International](LICENSE-ARTWORK)

Originally created by [Ivar Brandt](https://github.com/ivarbrandt). See individual license files for full terms.
