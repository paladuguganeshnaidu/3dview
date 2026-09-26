# 3dview

## Project Overview
`3dview` is a static browser application for viewing CityJSON building geometry in 3D and assigning floor/unit metadata per building.

## Executive Summary
This repository contains a client-side Three.js viewer that loads bundled CityJSON tiles (or user-provided CityJSON files), renders building volumes, supports floor division and per-floor unit entry, and exports assignments as JSON. There is no backend service in this repository.

## Problem Statement
Users need a lightweight way to inspect 3D building solids and capture floor/unit assignment data without deploying server infrastructure.

## Background and Motivation
The UI and data model are oriented to volumetric-cadastre workflows, with building attributes such as approved floor count (`b3_bouwlagen`) and support for ULPIN-style unit code composition.

## Proposed Solution
Provide a single-page static app (`index.html` + `3dmap.html`) that:
- Loads CityJSON data
- Renders buildings in 3D
- Lets users select buildings and set floor count
- Lets users add/edit unit-side and coordinate fields per floor
- Exports assignment data as JSON

## Project Objectives
- Keep deployment simple (static hosting)
- Keep interaction responsive for large tiles (time-sliced build loop)
- Preserve key building metadata for assignment context

## Project Scope
### In Scope
- Static 3D rendering of CityJSON buildings
- Floor assignment and unit entry UI
- Exporting assignment JSON
- Built-in sample datasets

### Out of Scope
- Multi-user collaboration
- Server-side persistence/database
- Authentication/authorization
- Public API endpoints

### Future Scope
Not explicitly documented in repository artifacts.

## Target Users
- GIS/3D data practitioners
- Volumetric-cadastre and property-data workflows
- Analysts who need quick local review of CityJSON building tiles

## Real-World Use Cases
- Review a city tile and compare measured model floors vs approved floors
- Prepare floor/unit mapping records for downstream processing
- Inspect third-party CityJSON files via the “Open file…” option

## Key Features
- Three.js-based 3D viewer with orbit/pan/zoom controls
- Dataset picker for bundled tiles: `9-356-364.city.json`, `9-572-508.city.json`
- Building selection panel with measured height, footprint, approved/model floors
- Floor-divider visualization
- Per-floor unit rows (`side`, `number`, `latitude`, `longitude`)
- JSON export of assignments (`3d-building-assignments.json`)

## Functional Requirements
- Load CityJSON via fetch (bundled files) or local file input
- Parse `Building`/`BuildingPart` objects and render highest available LOD geometry
- Allow user floor-count updates and per-floor unit edits
- Export current assignment state to JSON

## Non-Functional Requirements
- Runs in modern browser with JavaScript enabled
- No server runtime required
- Interactive responsiveness supported via incremental geometry build loop

## User Roles and Permissions
Single-user local interaction only. No role or permission model is implemented.

## System Workflow
1. Open app (`index.html` -> `3dmap.html` iframe)
2. Select a bundled dataset or upload a CityJSON file
3. Click a building in the 3D view
4. Review metadata and set floor count
5. Add/edit units per floor
6. Export assignment JSON

## Technology Stack
### Frontend
- HTML, CSS, JavaScript
- Three.js (`three.min.js`)
- OrbitControls
- Earcut triangulation

### Backend
Not applicable.

### Database
Not applicable.

### APIs
Not applicable (no HTTP API service in repository).

### Authentication
Not applicable.

### Cloud / Infrastructure
- Static hosting compatible
- Repository history and prior README indicate GitHub Pages usage

### DevOps
- GitHub Actions workflow history shows Pages build/deploy runs

### Testing Tools
No automated test framework detected in repository.

### Monitoring Tools
Not configured in repository.

## System Architecture
Client-only static architecture:
- `index.html` hosts full-screen iframe
- `3dmap.html` contains UI + rendering/runtime logic
- `.city.json` files are local static data assets

## Application Flow
Input CityJSON -> parse objects/geometry -> render meshes -> user assigns floors/units -> export assignment JSON.

## Data Flow
- Read path: JSON file -> in-memory geometry/metadata -> UI state
- Write path: UI state -> generated export JSON file download

## Project Structure
```text
/home/runner/work/3dview/3dview
├── index.html
├── 3dmap.html
├── 9-356-364.city.json
├── 9-572-508.city.json
└── README.md
```

## Database Design
Not applicable.

## API Documentation
Not applicable.

## Authentication and Authorization
Not applicable.

## Security
- No secret/environment configuration exists in this repository.
- App executes entirely in browser context.
- Input files are user-provided JSON; validation hardening is limited to parse/error handling in current implementation.

## Installation and Setup
### Prerequisites
- Modern browser (Chrome/Edge/Firefox/Safari)

### Clone Repository
```bash
git clone https://github.com/paladuguganeshnaidu/3dview.git
cd 3dview
```

### Local Development
You can open `index.html` directly, but serving statically is recommended for consistent file loading.

Example:
```bash
python -m http.server 8000
```
Then open `http://localhost:8000/`.

## Environment Variables
None required.

## Running / Deployment
- Local: static file serving
- Deployment model: static hosting (GitHub Pages workflow history observed)

## User Guide
- Use dataset dropdown or **Open file…**
- Click building to open assignment panel
- Set floor count and click **Apply**
- Add/remove floor units and edit fields
- Click **Download assignments (JSON)**

## Screenshots / Demo
- Demo URL (from existing project documentation): <https://paladuguganeshnaidu.github.io/3dview/>
- No repository-managed screenshots were found.

## Testing Strategy and Observed Results
### Strategy
For this repository state, validation is limited to repository inspection and CI history because no test/lint/build scripts are defined.

### Observed Results (this update)
- Repository file scan: no `package.json`, test directories, or build tooling files detected.
- GitHub Actions runs reviewed:
  - `pages build and deployment` run `34139639500` (completed, success)
  - Failed-job log query on that run returned: `No failed jobs found`.

## Performance
No benchmark scripts or measured performance reports are included in this repository.

## Limitations
- No backend persistence; exported JSON must be managed externally.
- No built-in authentication/authorization.
- No automated test suite currently present.

## Known Issues
No explicit issue list is maintained inside repository files.

## Troubleshooting
- If dataset loading fails, ensure files are accessible from the hosting path.
- If local `file://` loading is blocked by browser policy, use a local static server.

## Logging and Monitoring
- Runtime user feedback via UI toast messages.
- Browser console logs are used for load errors.
- No centralized logging/monitoring/alerts configured.

## Deployment
Static-site deployment is suitable. Prior workflow history indicates GitHub Pages deployment.

## CI/CD Pipeline
Observed via GitHub Actions history:
- Workflow: **pages build and deployment**
- Recent completed runs on `main` are successful.

## Backup, Privacy, Compliance
- Backup/recovery strategy is not documented in repository artifacts.
- Data privacy/compliance controls are not documented.

## Dependencies and Integrations
- CDN dependencies in `3dmap.html`:
  - `three@0.128.0`
  - `OrbitControls` from Three.js examples
  - `earcut@2.2.4`
- No backend third-party service integrations detected.

## Versioning and Releases
No explicit versioning or release process documentation found.

## Roadmap
No formal roadmap file or section found in repository artifacts.

## Contribution and Development Guidelines
No dedicated `CONTRIBUTING.md` was found. Recommended baseline for contributors:
- Keep changes focused and reviewable
- Validate behavior in browser for UI/runtime changes
- Document functional changes in README

## Branching / Commit / PR Guidance
Not formally defined in repository files. Use standard GitHub PR workflow.

## License
See [LICENSE](./LICENSE).

## Authors / Contributors
- Repository owner: **Paladugu Ganesh Naidu**
- Additional contributors are not enumerated in repository documentation.

## Acknowledgements
- Three.js and Earcut open-source projects
- Source CityJSON/BAG-derived building data included in repository

## References
- Repository source files: `index.html`, `3dmap.html`, bundled `.city.json` datasets
- GitHub Actions run history for CI/deployment evidence

## FAQ
**Q: Is a backend required?**
A: No. This repository is a static client-side app.

**Q: Where is data stored?**
A: In browser memory during use; exports are downloaded as JSON files.

**Q: Are there automated tests?**
A: None were found in current repository contents.
