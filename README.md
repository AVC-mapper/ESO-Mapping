# Philippines ESOs Ecosystem Mapping

Interactive, single-page dashboard that maps Entrepreneur Support Organizations (ESOs) in the Philippines (and SEA) with filters by type, sector, stage, gender lens, and more.

## What’s inside

- `index.html` — the dashboard. It **auto-loads** JSON data placed in the same folder.
- `esos_details.json` — ESO metadata (about, programs, sector/focus, flagship programs, funding, etc.).
- `esos_area.json` — map-ready coverage (AreaType, AreaNames, PSGC codes, pins, etc.).

## Quick start (GitHub Pages)

1. Create a new repo (or use an existing one).
2. Add these three files to the repo root: `index.html`, `esos_details.json`, `esos_area.json`.
3. Commit & push to `main`.
4. In **Settings → Pages**, set **Source** to `Deploy from a branch`, pick `main`, and the root folder `/`.
5. Open your site URL. The page will display “Loaded built-in JSON data.” and the map & filters will be ready.

> Note: Opening `index.html` directly via `file://` may block JSON fetches due to browser security. Host via GitHub Pages (or any static server) to load data correctly. For local testing, use a simple local server (e.g., `python -m http.server`).

## Data model

### `esos_details.json` (sheet: *Data*)
Key fields recognized by the app (others are shown under **More** in the details panel):

- `ESO` (string, **required**)
- `Type` (string or multi-value)
- `About` (string)
- `Programs` (string)
- `Flagship Programs` (string)
- `Sectors` (**from your “Sector/Focus” column**; supports comma/semicolon/slash/newline separators)
- `Stage` (string or multi-value)
- `Gender Lens` (`Yes` / `No`)
- `Provides Funding` (`Yes` / `No`)
- `Funding Type` (string)
- `Portfolio Enterprises` (string, free text)

### `esos_area.json` (sheet: *Area*)
- `ESO` (string, **required**, must match an ESO in details)
- `AreaType` (`country` | `region` | `province` | `city_muni`)
- `AreaNames` (human-readable names)
- `PSGC_Codes` (comma/semicolon/space-separated PSGC codes)
- `Pin_Lat`, `Pin_Lon` (optional, can be multi-value; if absent the app uses centroids for common regions/cities)
- `Notes`, `SourceURL` (optional)

## Using the dashboard

- **Filter & search**: Use the sidebar to filter by Type, Sector, Stage, Area Type, and Gender Lens, or use free-text search.
- **Click an ESO**: Highlights its coverage and shows details (including flagship program(s), funding, and portfolio if provided).
- **Export**: Click *Export Filtered CSV* to export the current filtered list.

## Updating data

- To keep it upload-free, just update `esos_details.json` and `esos_area.json` and push to GitHub. The page auto-loads the new data.
- Alternatively, users can still upload the Excel workbook from the UI to override data at runtime (no redeploy needed).

## Known limitations / roadmap

- Region/city shapes are approximated with centroids by default. We can add exact **GeoJSON polygons** (e.g., Caraga or Quezon City) for precise highlighting.
- If an ESO has multiple coverage areas, all pins/centroids are shown and the map fits to all of them.
- For nationwide ESOs, the Philippines polygon is shaded and a pin is placed at the country centroid.

## Self-tests

The page includes basic self-tests (open DevTools console) and a **Demo Data** button to verify behavior quickly.

—
Built for Villgro Philippines, color scheme `#08842a`.
