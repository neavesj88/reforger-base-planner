# Arma Reforger Base Placement Tool

Plan MOB, base and radio-relay placement for **Conflict on Everon** — one self-contained
`index.html` with the full topographic map embedded. No build, no server, no dependencies,
no network: download the file, open it, plan. Works from `file://` and any static host.

Sibling project to [lion-board](https://github.com/neavesj88/lion-board) and follows the
same philosophy: single file, everything inlined, data local-only (localStorage — nothing
is uploaded).

## Features

- Place up to **2 MOBs** (hard cap), unlimited **bases**, **supply bases** and **radio relays**
- Each marker draws a green **radio coverage** circle and a pink **minimum base distance**
  circle (the "con limit" spacing from `SCR_MinBaseDistanceConfig`); supply/source points
  have no radio, so they show only the spacing ring
- Radio circles **toggle per type** (MOB / base / relay), and every radius — radio ranges
  and each type's min-distance — is individually adjustable
- Drag markers to move, click to rename/delete; soft warning when two markers sit inside
  each other's minimum distance
- **Measure tool** (drag for distance in metres), 1 km grid overlay, live coordinate readout
- **Select** (default tool): drag the map to move around, drag markers, click one to edit;
  wheel/pinch to zoom
- Settings autosave in the browser — including on a downloaded copy of the file — and a
  **↺ Reset settings** button restores the defaults
- Autosaves the plan to localStorage; **export/import plans as JSON**, **export the map as PNG**
- Installable as a PWA when hosted over HTTPS (custom icon does not apply from `file://`)

## Default ranges — adjust in Settings

Defaults come from a real Conflict server config; values vary by game version and server, so
every radius is editable in the ⚙ Settings drawer.

Radio coverage:

| Setting | Default | Basis |
|---|---|---|
| Base radio range | 2,000 m | server config |
| Relay radio range | 3,000 m | server config |
| MOB radio range | 2,000 m | **estimate** — treated like a base |

Minimum base distance — the "con limits" from `SCR_MinBaseDistanceConfig`:

| Base type | Default | Basis |
|---|---|---|
| Base (`BASE`) | 850 m | server config |
| Supply / source (`SOURCE_BASE`) | 450 m | server config |
| Relay (`RELAY`) | 300 m | server config |
| MOB spacing | 850 m | **estimate** — treated like a base |

Radio coverage and minimum distance are two different mechanics: green shows how far a base
projects radio; pink shows how close another base of that type may be placed. Supply/source
points have no radio, so no green circle. If you have different values from your own server
config, plug them in — circles update live and the values persist.

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
