# Arma Reforger Base Placement Tool

Plan MOB, base and radio-relay placement for **Conflict on Everon** — one self-contained
`index.html` with the full topographic map embedded. No build, no server, no dependencies,
no network: download the file, open it, plan. Works from `file://` and any static host.

Sibling project to [lion-board](https://github.com/neavesj88/lion-board) and follows the
same philosophy: single file, everything inlined, data local-only (localStorage — nothing
is uploaded).

## Features

- Place up to **2 MOBs** (hard cap), unlimited **bases**, **supply bases** and **radio relays**
- MOBs/bases draw a green **radio coverage** circle and a pink **build zone** circle; relays
  draw a radio-only circle; supply bases draw a smaller build-only circle
- Radio circles **toggle per type** (MOB / base / relay), and every radius —
  radio ranges and MOB/base/supply build zones — is individually adjustable
- Drag markers to move, click to rename/delete; soft warning when two build zones overlap
- **Measure tool** (drag for distance in metres), 1 km grid overlay, live coordinate readout
- **Select** (default tool): drag the map to move around, drag markers, click one to edit;
  wheel/pinch to zoom
- Settings autosave in the browser — including on a downloaded copy of the file — and a
  **↺ Reset settings** button restores the defaults
- Autosaves the plan to localStorage; **export/import plans as JSON**, **export the map as PNG**
- Installable as a PWA when hosted over HTTPS (custom icon does not apply from `file://`)

## Default ranges — adjust in Settings

Bohemia doesn't publish official numbers and they vary by game version and server config,
so every radius is editable in the ⚙ Settings drawer:

| Setting | Default | Basis |
|---|---|---|
| Base radio range | 1,000 m | community guides |
| Relay radio range | 2,000 m | community guides ("additional 2000 m of radio coverage") |
| MOB radio range | 2,500 m | **estimate** — not published |
| MOB / base build radius | 750 m | **estimate** — not published |
| Supply base build radius | 300 m | **estimate** — no published figure at all |

Sources: [XGamingServer Conflict guide](https://xgamingserver.com/blog/arma-reforger-conflict-mode-guide/),
[XGamingServer radio guide](https://xgamingserver.com/blog/arma-reforger-radio-communications-guide/),
[Steam Ultimate Beginners Guide](https://steamcommunity.com/sharedfiles/filedetails/?id=3402008832).
If you have verified values from game files or your server config, plug them in — circles
update live and the values persist.

## Map calibration

The embedded image is a community topographic render of Everon ("Everon 1989",
Bohemia Interactive terrain), cropped to its grid area and downscaled to 8192 px.
The render's own 100 m grid was measured at 111.82 px per 100 m at source resolution,
giving a rendered area of exactly **13,600 × 13,100 m** (the 12.8 × 12.8 km terrain plus
sea padding). All in-app distances derive from that grid, so measurements match in-game
distances.

## Stack

Vanilla HTML/CSS/JS · SVG overlay for range rings · DOM tokens with pointer events ·
CSS-transform pan/zoom · canvas PNG export · localStorage · inline PWA manifest.
One file, ~8 MB (the map is most of it).
