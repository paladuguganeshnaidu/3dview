# 3dview — 3D Building Floor Assignment Viewer

A static, browser-based CityJSON viewer for **volumetric cadastre** workflows. Click any building in the 3D city, set the number of floors, and assign per-floor units (side, unit number, latitude, longitude). Assignments export to JSON.

Built with Three.js — no server or build step required. Deployed on GitHub Pages.

## Features
- Renders CityJSON (3D BAG style) building volumes using the most detailed solid (LOD 2.2) — one clean volume per building, no overlapping duplicates.
- Click a building → measured height, footprint, approved floors (from `b3_bouwlagen`) and a height-vs-approved review chip.
- Divide any building into N floors with visible dividers.
- Per-floor unit editor: side (N/E/S/W), unit number, latitude, longitude; add/remove units per floor.
- ULPIN-style unit code preview per floor.
- Export all building assignments as JSON.
- Two bundled datasets (`9-356-364.city.json`, `9-572-508.city.json`) plus "Open file…" for any CityJSON.
- Time-sliced rendering keeps the page responsive on large tiles.

## Use
Open https://paladuguganeshnaidu.github.io/3dview/ (or `index.html` locally via a static server).

- **Click building** — open the record/assignment panel.
- **Drag** — rotate · **Scroll** — zoom · **Right-drag** — pan.

## Data notes
Each `Building` (Pand) carries its metadata (`b3_bouwlagen` = approved floor count, roof heights, footprint area). Its `BuildingPart` child holds the actual 3D solid. The viewer renders each part once at its highest LOD and joins it to the parent building for floor assignment. Where no approved floor count exists in the source, the value is marked accordingly and can be set manually.