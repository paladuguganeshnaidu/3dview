# 3dview — 3D Building Floor Assignment Viewer

A static, browser-based **CityJSON viewer** for experimenting with volumetric-cadastre and vertical-property workflows.

The application lets a user inspect a 3D building, assign floors and units, preview ULPIN-style unit identifiers, and export assignments as JSON.

> **Status:** Static prototype / research demonstrator. It is not a legal cadastral or land-title system.

## Features

- Renders CityJSON building volumes.
- Uses the most detailed available building part representation selected by the viewer.
- Displays building metadata such as measured height, footprint and approved-floor information when present.
- Divides a building into a configurable number of floors.
- Assigns per-floor units with:
  - side (N/E/S/W);
  - unit number;
  - latitude;
  - longitude.
- Shows a ULPIN-style unit-code preview.
- Exports building assignments as JSON.
- Bundles two CityJSON demo datasets:
  - `9-356-364.city.json`
  - `9-572-508.city.json`
- Supports opening another CityJSON file locally.
- Uses time-sliced rendering to keep large tiles responsive.

## Technology

- Three.js
- CityJSON data
- HTML / CSS / JavaScript
- Browser APIs for local file selection and JSON export

No backend or database is required for the current application.

## Online demo

GitHub Pages:

https://paladuguganeshnaidu.github.io/3dview/

You can also open the static `index.html` locally through a static web server.

## Usage

1. Open the viewer.
2. Click a building.
3. Inspect the building record and floor metadata.
4. Choose the number of floors.
5. Add or edit units for each floor.
6. Export the assignments as JSON.

### Controls

| Action | Interaction |
|---|---|
| Rotate | Drag |
| Zoom | Scroll |
| Pan | Right-drag |

## Data interpretation

The viewer uses the metadata supplied by the CityJSON source. Building and BuildingPart relationships are used to associate 3D geometry with building-level attributes.

Fields such as `b3_bouwlagen` are source metadata, not measurements invented by the viewer.

When an approved floor count is unavailable, the interface allows manual assignment rather than fabricating a source value.

## Project scope

### In scope

- 3D building inspection.
- Floor visualization.
- Unit assignment.
- JSON export.
- Demonstration of vertical-property data handling.

### Out of scope

- Official cadastral registration.
- Ownership verification.
- Survey-grade positioning.
- Persistent multi-user storage.
- Server-side authorization.

## Validation and performance

The project is a static browser application. This repository does not claim independently measured P95/P99 latency, throughput, concurrent-user capacity, or formal accessibility scores.

Large-file responsiveness depends on browser, device and CityJSON tile size.

## Known limitations

- No backend persistence.
- No authentication.
- No database.
- No authoritative cadastral integration.
- ULPIN-style codes are demonstrative and should not be interpreted as official identifiers.

## License

No explicit open-source license is currently declared in the repository.

Until a license is added, reuse should be treated as restricted by copyright law.

## Author

Paladugu Ganesh Naidu

Repository: https://github.com/paladuguganeshnaidu/3dview
