# nwg-drawer

This application is a part of the [nwg-shell](https://github.com/nwg-piotr/nwg-shell) project.

Nwg-drawer is a golang replacement to the `nwggrid` command
(a part of [nwg-launchers](https://github.com/nwg-piotr/nwg-launchers)). It's being developed with
[sway](https://github.com/swaywm/sway) in mind, but should also work with other wlroots-based Wayland compositors.
X Window System is not officially supported, but you should be able to use the drawer on some floating
window managers (tested on Openbox).

The `nwg-drawer` command displays the application grid. The search entry allows to look for installed applications,
and for files in XDG user directories. The grid view may also be filtered by categories.

You may pin applications by right-clicking them. Pinned items will appear above the application grid. Right-click
a pinned item to unpin it. The pinned items cache is shared with [nwg-menu](https://github.com/nwg-piotr/nwg-menu)
and `nwggrid`.

![screenshot-01.png](https://scrot.cloud/images/2021/05/30/screenshot-01.png)

[more screenshots](https://scrot.cloud/album/nwg-drawer.Bogd) | [see on YouTube](https://youtu.be/iIgxJQhCQf0)

[![Packaging status](https://repology.org/badge/vertical-allrepos/nwg-drawer.svg)](https://repology.org/project/nwg-drawer/versions)

## Installation

### Dependencies

- go >=1.16 (just to build)
- gtk3
- gtk-layer-shell
- xdg-utils

Optional (recommended):

- thunar
- alacritty

You may use another file manager and terminal emulator (see command line arguments), but mentioned above have been
confirmed to work well with the program. Also see **Files** below.

### Steps

1. Clone the repository, cd into it.
2. Install necessary golang libraries with `make get`.
3. `make build`
4. `sudo make install`

Building the gotk3 library takes quite a lot of time. If your machine is x86_64, you may skip steps 2-3, and
install the provided binary by executing step 4.

## Command line arguments

```text
$ nwg-drawer -h
Usage of nwg-drawer:
  -c uint
    	number of Columns (default 6)
  -fm string
    	File Manager (default "thunar")
  -fscol uint
    	File Search result COLumns (default 2)
  -fslen int
    	File Search name length Limit (default 80)
  -is int
    	Icon Size (default 64)
  -lang string
    	force lang, e.g. "en", "pl"
  -nocats
    	Disable filtering by category
  -nofs
    	Disable file search
  -o string
    	name of the Output to display the drawer on (sway only)
  -ovl
    	use OVerLay layer
  -s string
    	Styling: css file name (default "drawer.css")
  -spacing uint
    	icon spacing (default 20)
  -term string
    	Terminal emulator (default "alacritty")
  -v	display Version information
  ```

  *NOTE: the `TERM` environment variable overrides the `-term` argument if defined.*

## Styling

Edit `~/.config/nwg-panel/drawer.css` to your taste.

## Files

When the search phrase is at least 3 characters long, your XDG user directories are being searched.

![screenshot-03.png](https://scrot.cloud/images/2021/05/30/screenshot-03.png)

Use the **left mouse button** to open a file with the `xdg-open` command. As configuring file associations for it is
PITA, you may override them, by creating the `~/.config/nwg-panel/preferred-apps.json` file with your own definitions.

### Sample file content

```json
{
  "\\.pdf$": "atril",
  "\\.svg$": "inkscape",
  "\\.(jpg|png|tiff|gif)$": "feh",
  "\\.(mp3|ogg|flac|wav|wma)$": "audacious",
  "\\.(avi|mp4|mkv|mov|wav)$": "mpv",
  "\\.(doc|docx|xls|xlsx)$": "libreoffice"
}
```

Use the **right mouse button** to open the file with your file manager (see `-fm` argument). The result depends on the
file manager you use.

- thunar will open the file location
- pcmanfm will open the file with its associated program
- caja won't open anything, except for directories

I've noy yet tried other file managers.

## Credits

This program uses some great libraries:

- [gotk3](https://github.com/gotk3/gotk3) Copyright (c) 2013-2014 Conformal Systems LLC,
Copyright (c) 2015-2018 gotk3 contributors
- [gotk3-layershell](https://github.com/dlasky/gotk3-layershell) by [@dlasky](https://github.com/dlasky/gotk3-layershell/commits?author=dlasky) - many thanks for writing this software, and for patience with my requests!
- [go-sway](https://github.com/joshuarubin/go-sway) Copyright (c) 2019 Joshua Rubin
- [go-singleinstance](github.com/allan-simon/go-singleinstance) Copyright (c) 2015 Allan Simon
