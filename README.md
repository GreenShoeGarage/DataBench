# DataBench

**DataBench** is a browser-based data visualization and analysis workbench for turning messy spreadsheet data into useful dashboards, reports, and mobile-friendly viewer pages.

Upload CSV/XLSX data, inspect fields, clean common spreadsheet problems, build charts and pivot tables, create calculated fields, link datasets, customize themes, save projects as JSON, and publish dashboards as standalone viewer files or static sites.

DataBench is intentionally lightweight: no backend, no database server, no account system, and no build step required for basic use.

---

## Current Version

**DataBench Editor v2.0.7**  
**DataBench Viewer v2.0.7**  
**Project schema version: 8**

The project currently ships as two static browser apps:

- `databench.html` — the full desktop-oriented editor/workbench
- `databench-viewer.html` — the mobile-friendly dashboard viewer

The old `quickviz_suite.html` compatibility copy is no longer maintained.

---

## Latest Update: v2.0.7

DataBench v2.0.7 is a bug-fix and reliability release focused on dashboard widget sizing.

Fixes and notes:

- Resized widgets now retain their width and height when switching away from a page and returning.
- The editor now uses the dedicated bottom-right resize handle as the authoritative resize path.
- The old observer-based resize tracking that could accidentally save detached widgets at tiny dimensions has been removed.
- Widget geometry is preserved in project state, autosave, and exported project JSON.
- The visible editor/viewer version labels now match the runtime version.

When editing dashboards, resize widgets using the bottom-right resize handle, then switch pages normally. The saved dimensions should remain intact.

---

## What DataBench Is For

DataBench is for the moment when someone has a spreadsheet and needs to understand it quickly.

It is useful for:

- quick spreadsheet exploration
- small dashboards
- repair clinic/event metrics
- classroom data activities
- maker space reports
- inventory snapshots
- survey summaries
- lightweight business intelligence
- quick PDF/PPT/dashboard exports
- mobile-friendly dashboard sharing

It is not intended to replace full enterprise BI platforms, data warehouses, or governed analytics systems.

---

## Highlights

- Runs entirely in the browser
- No backend required
- Uploads CSV, XLSX, XLS, and XLSM data files
- Imports published Google Sheets CSV links
- Creates default table pages for uploaded datasets
- Creates automatic data summary pages
- Provides a Home screen on startup
- Includes autosave with LED-style status indicator
- Saves and loads `.databench.json` project files
- Supports multi-page dashboard canvases with page-specific widget layouts
- Adds draggable, resizable widgets with persistent geometry
- Supports tables, charts, KPIs, summaries, pivot tables, and text/markdown widgets
- Uses dimensions, measures, aggregations, calculated fields, filters, and joins
- Includes data prep and field profiling tools
- Includes page layout tools, snap-to-grid, alignment, and page size presets
- Includes professional and playful themes with contrast checks
- Exports JSON, CSV, HTML, PNG, PDF, PPTX, standalone mobile viewer HTML, and static site packages
- Includes a separate mobile-friendly viewer
- Supports hosted project URLs and QR-code sharing helpers
- Includes a command palette with `Ctrl/Cmd + K`
- Includes project migration support for older saved projects
- Includes a widget registry foundation for future extension

---

## Quick Start

1. Download or clone this repository.
2. Open `databench.html` in a modern browser.
3. The **Home** dialog opens automatically.
4. Choose one of the startup actions:
   - **New project**
   - **Open data file**
   - **Open project JSON**
   - **Restore autosave**
   - **Load sample project**
   - **Open viewer**
   - **Health check**
5. Upload a CSV/XLSX file or load the sample project.
6. Build dashboard pages with tables, charts, KPIs, summaries, pivot tables, and text widgets.
7. Save your work with **Save JSON**.
8. Share or publish using **Mobile Viewer**, **Static Site**, **Publish Link**, PDF, PPTX, PNG, or HTML export.

No installation is required for basic use.

---

## Recommended Repository Structure

For static hosting, use this layout:

```text
/databench/
  index.html              # copy databench.html here
  viewer/
    index.html            # copy databench-viewer.html here
  projects/
    example.databench.json
  README.md
  LICENSE
```

With this structure:

- The editor lives at `/databench/`.
- The viewer lives at `/databench/viewer/`.
- Hosted project JSON files can live at `/databench/projects/`.

The editor’s **Open Viewer** button opens:

```text
./viewer/
```

The viewer’s **Editor** button returns to:

```text
../
```

A hosted project can be opened in the viewer with:

```text
/databench/viewer/?project=../projects/example.databench.json
```

---

## Local File Layout

For simple local use, the repository can also be kept flat:

```text
.
├── databench.html
├── databench-viewer.html
├── README.md
└── LICENSE
```

Open `databench.html` directly in a browser.

Some browser security rules may limit certain file/URL workflows when opening HTML from `file://`. For publishing and hosted project links, use a small local server or static host.

Example local server:

```bash
python3 -m http.server 8000
```

Then open:

```text
http://localhost:8000/databench.html
```

---

## Editor vs Viewer

DataBench has two related apps.

### DataBench Editor

The editor is the full authoring workbench. Use it to:

- upload spreadsheets
- import published Google Sheets CSV links
- inspect and clean data
- create charts and dashboard pages
- build pivot tables
- add text/markdown notes
- create calculated fields
- link datasets through relationships
- configure page and widget filters
- customize themes
- arrange layouts
- save project JSON
- run health checks
- export dashboards and published packages

### DataBench Viewer

The viewer is for reading, presenting, and sharing finished dashboards. It is intentionally simpler than the editor and is optimized for phones, tablets, and presentation use.

The viewer supports:

- opening `.databench.json` project files
- opening hosted project URLs with `?project=...`
- opening local preview projects with `?source=local`
- loading standalone embedded viewer exports
- loading a default `project.databench.json` next to `index.html` in static-site exports
- browsing pages
- page filters
- filter dropdowns populated from unique field values
- chart click/tap-to-filter
- tables with search, sorting, and pagination
- mobile stacked widget layout
- desktop/tablet canvas-style layout
- fullscreen widget view
- presentation mode
- sharing panel with link and QR-code helper

The viewer does not include authoring features such as spreadsheet upload parsing, widget dragging/resizing, calculated-field editing, data modeling, or export configuration.

---

## Data Transfer Between Editor and Viewer

DataBench supports several transfer paths.

### 1. Project JSON

In the editor:

1. Click **Save JSON**.
2. Open the viewer.
3. Open the saved `.databench.json` file.

This is the safest long-term storage and archive format.

### 2. Preview Viewer

In the editor:

1. Click **Preview Viewer**.
2. The current project is saved to local browser storage.
3. The viewer opens with:

```text
/viewer/?source=local
```

This is useful while designing a dashboard.

### 3. Standalone Mobile Viewer HTML

In the editor:

1. Build a dashboard.
2. Click **Mobile Viewer**.
3. Share the exported `.databench.viewer.html` file.

The exported HTML contains the current project embedded in the file.

### 4. Hosted Project Link

Host a project JSON file and open it from the viewer:

```text
/databench/viewer/?project=../projects/example.databench.json
```

This is useful for GitHub Pages, Netlify, Cloudflare Pages, intranets, and simple static web servers.

### 5. Static Site Export

In the editor, click **Static Site** to export a publishable package containing:

```text
index.html
project.databench.json
databench.manifest.json
README.txt
```

The exported `index.html` is a viewer page that automatically loads `project.databench.json` from the same folder.

---

## Home Screen

DataBench opens with the **Home** dialog displayed.

Available Home actions:

- **New project** — start with an empty project
- **Open data file** — upload CSV/XLSX/XLS/XLSM as a new data source
- **Open project JSON** — load a saved `.databench.json` project
- **Restore autosave** — recover browser-saved work
- **Load sample project** — load built-in sample data and dashboards
- **Open viewer** — open the mobile-friendly dashboard viewer
- **Health check** — scan the current project for common issues

The Home dialog can be closed and reopened with the **Home** button in the toolbar.

---

## Data Sources

A data source is a table loaded into the project.

Sources can come from:

- CSV files
- XLSX/XLS/XLSM spreadsheet files
- Published Google Sheets CSV URLs
- Built-in sample data
- Joined/materialized datasets created inside DataBench

Each uploaded source receives:

- a default table page
- a default summary page
- field type detection
- role hints for dimensions/measures
- optional field profiles in Data Prep

---

## Tables

Table widgets support:

- search
- sortable column headers
- pagination
- row count notes
- horizontally scrollable tables for wide data
- viewer-side search/sort/pagination

Default pages for uploaded files are table pages so users can inspect raw data before building charts.

---

## Widgets

Current widget types include:

- Table
- Bar chart
- Horizontal bar chart
- Line chart
- Pie chart
- Donut chart
- Scatter chart
- KPI card
- Data summary
- Pivot table
- Text/Markdown

Widgets can be:

- selected
- configured
- dragged by the widget header
- resized with the bottom-right resize handle
- persist their size/position when switching pages
- duplicated
- deleted
- sent forward/backward
- exported through page/project export workflows

Right-click a widget to open the context menu.

---

## Dimensions, Measures, and Aggregations

DataBench uses a lightweight BI-style model.

- **Dimensions** group rows into categories.
- **Measures** calculate numeric or count-based values.

Example:

```text
Dimension: Region
Measure: Revenue
Aggregation: Sum
```

Supported aggregations include:

- Sum
- Average
- Median
- Min
- Max
- Range
- Count
- Count if
- Count distinct
- First
- Last
- Percent of total

---

## Charts

Supported chart types include:

- Bar
- Horizontal bar
- Line
- Pie
- Donut
- Scatter

Chart options include:

- data source
- dimension
- measure
- aggregation
- sort by dimension or measure
- ascending/descending sort
- Top N groups
- custom chart colors
- chart click/tap-to-filter behavior

---

## Pivot Tables

Pivot table widgets support:

- row field
- column field
- measure field
- aggregation
- row totals
- grand totals

Pivot tables are available in both the editor and viewer.

---

## Calculated Fields

Calculated fields add derived columns to a source table.

Example formulas:

```text
[Revenue] - [Cost]
year([Order Date])
ifelse([Status] == "Closed", 1, 0)
round([Profit] / [Revenue], 2)
```

Supported helper functions include:

- `number(value)`
- `text(value)`
- `upper(value)`
- `lower(value)`
- `trim(value)`
- `contains(value, search)`
- `year(date)`
- `month(date)`
- `day(date)`
- `ifelse(condition, trueValue, falseValue)`
- `round(value, digits)`

Use brackets for field names with spaces:

```text
[Order Date]
[Total Revenue]
```

---

## Relationships and Joins

DataBench can link datasets using shared key fields.

The Data Model tools can:

- suggest matching key fields
- preview match counts
- warn about blank keys
- warn about duplicate keys
- save relationships
- delete relationships
- materialize relationships into joined tables
- create left joins or inner joins

Relationships are currently materialized into joined tables rather than backed by a live query model.

---

## Filters

Filters can be applied at the page or widget level.

Supported operators include:

- Equals
- Does not equal
- Contains
- Greater than
- Less than
- Greater than or equal
- Less than or equal
- Between
- Before date
- After date

The viewer’s filter value control uses a dropdown populated with unique values from the selected field. Blank values are shown as `(blank)`, and very large unique-value lists are capped for usability.

On mobile, viewer filters appear in a slide-up filter drawer.

---

## Data Prep and Field Profiles

The editor includes a **Data Prep & Field Profiles** panel.

Field profiles show:

- detected field type
- suggested role
- blank values
- unique values
- possible key status
- numeric min/max/average
- detected date range
- top value distribution
- likely Excel serial-date warnings

Cleanup tools include:

- rename field
- change field type
- convert Excel serial dates to ISO dates
- trim text
- replace blank values
- remove empty rows
- remove duplicate rows

Field rename attempts to update charts, pivots, filters, and widget references where possible.

---

## Layout Tools

The editor includes dashboard layout tools:

- page size presets
- custom page dimensions
- snap to grid
- grid size control
- snap selected widget
- align selected widget left/center/right
- align selected widget top/middle/bottom
- fit page to widgets
- arrange widgets to grid
- duplicate page

Page width/height is saved in project JSON and respected by the viewer. Widget position and size are also saved per page and retained when navigating between pages.

On phones, the viewer transforms dashboard pages into stacked cards for readability.

---

## Text / Markdown Widgets

Text widgets can be used for:

- dashboard notes
- page introductions
- headings
- explanations
- bullet lists
- simple report-style commentary

Text widgets render in both the editor and viewer.

---

## Theme Studio

DataBench includes built-in themes ranging from professional to playful.

Themes include:

- Light Professional
- Dark Professional
- Slate Minimal
- Forest Workshop
- Ocean Lab
- Candy Pop
- Retro Arcade
- Maker Neon
- Custom

Theme settings can control:

- accent colors
- app background
- panel colors
- text colors
- canvas color
- card color
- grid color

Theme Studio includes a live contrast report. Project Health Check also flags obvious low-contrast combinations.

The viewer applies contrast-aware text handling so light card/table backgrounds remain readable inside dark themes.

---

## Autosave

DataBench includes browser-based autosave using `localStorage`.

Autosave behavior:

- saves project state automatically as changes happen
- debounces rapid edits
- periodically flushes unsaved changes
- saves before tab close when possible
- saves when the tab becomes hidden
- maintains a backup autosave copy
- restores current or older autosave slots
- records recent browser projects

The header includes an LED-style autosave indicator:

- **Dark** means changes are pending or unsaved.
- **Green/lit** means the latest state has been saved.
- **Red** means autosave failed, usually because storage is unavailable or full.

Autosave is convenient, but downloaded project JSON remains the safest long-term storage format.

---

## Recent Browser Projects

Autosaved projects appear in the Home dialog under **Recent browser projects**.

These are stored in browser local storage. They are useful for convenience, but they should not replace explicit `.databench.json` backups for important work.

---

## Command Palette

Open the command palette with:

```text
Ctrl/Cmd + K
```

The command palette supports:

- typing to search commands
- arrow-key navigation
- Enter to run a command
- Escape to close
- click-outside to close

Commands include common project actions, exports, publishing tools, widget creation, layout tools, undo/redo, and panel toggles.

---

## Project Health Check

The editor includes a **Health Check** tool.

It reports common issues such as:

- missing data sources
- missing pages
- widgets with incomplete configuration
- unsupported widget types
- missing widget IDs
- low-contrast widget/theme combinations
- project schema details
- widget registry status
- optional dependency availability
- export/publishing dependency notes

Run Health Check before publishing or sharing a dashboard.

---

## Publishing and Sharing

DataBench includes several publishing workflows.

### Save JSON

Downloads the editable project file.

Suggested extension:

```text
.databench.json
```

### Mobile Viewer

Exports a standalone HTML viewer with the current project embedded.

This is the easiest way to share a finished dashboard with someone who does not need editing tools.

### Preview Viewer

Saves the current project to local storage and opens the viewer with:

```text
?source=local
```

### Open Viewer

Opens the deployed viewer at:

```text
./viewer/
```

### Publish Link

Helps build a hosted viewer URL and QR code.

Example:

```text
/databench/viewer/?project=../projects/example.databench.json
```

### Static Site

Exports a publishable static viewer package containing:

```text
index.html
project.databench.json
databench.manifest.json
README.txt
```

Use this for GitHub Pages, Netlify, Cloudflare Pages, an intranet, or any simple static web host.

---

## Export Options

DataBench supports:

- project JSON
- standalone mobile viewer HTML
- static site package
- current page HTML
- current page PNG
- multi-page PDF
- PowerPoint PPTX
- selected/source CSV

Export quality depends on browser rendering, loaded chart libraries, and available memory.

---

## Version Notes

Current release: **v2.0.7**.

Recent v2 patch releases focused on stability after the v2.0 architecture update:

- **v2.0.7** — fixed widget resize persistence when switching pages.
- **v2.0.6** — added the dedicated widget resize handle and synchronized visible version labels.
- **v2.0.5** — improved page-switch geometry syncing.
- **v2.0.4** — opened the Home dialog automatically on startup.
- **v2.0.3** — restored missing contrast helper functions.
- **v2.0.2** — repaired CSV/XLSX/XLS/XLSM data-file opening paths.
- **v2.0.1** — fixed command-palette overlay visibility/close behavior.
- **v2.0.0** — introduced schema v8, migrations, architecture metadata, and the widget registry foundation.

---

## Project Schema and Migration

DataBench v2.0 uses project schema version `8`.

Project JSON includes architecture metadata such as:

- `projectType`
- `appVersion`
- `schemaVersion`
- `createdAt`
- `updatedAt`
- `viewer`
- `architecture`
- `migrationHistory`
- widget registry metadata

Older projects are normalized through a migration layer when loaded in the editor or viewer. Migration history is stored in project JSON.

---

## Widget Registry

DataBench includes a widget registry foundation.

The registry tracks supported widget types, normalizes widget defaults, and helps Health Check identify unsupported widgets.

This is groundwork for future plugin-style widgets.

---

## Browser Requirements

Recommended browsers:

- Chrome / Chromium
- Edge
- Firefox
- Safari

Use a current desktop browser for editing. The viewer is optimized for phones and tablets, but very large projects can still strain mobile browsers.

---

## External Libraries

DataBench uses browser libraries for spreadsheet parsing, charts, and exports.

Common dependencies include:

- **SheetJS** for XLSX parsing
- **Chart.js** for charts
- **html2canvas** for page/image capture
- **jsPDF** for PDF export
- **PptxGenJS** for PowerPoint export
- **JSZip** for static-site package export
- QR-code support for publish/share helpers

These are currently CDN-loaded in the browser. Internet access may be required for full functionality unless dependencies are bundled locally in a future release.

---

## Privacy Notes

DataBench runs in the browser. Uploaded files are processed locally by the app unless you modify the code to send data elsewhere.

Important notes:

- Files are not intentionally uploaded to a DataBench server.
- Autosave data is stored in browser local storage.
- Recent projects are stored in browser local storage.
- CDN libraries are loaded from third-party URLs.
- Published Google Sheets CSV imports fetch data from the provided URL.
- Hosted project links load project JSON from the URL you provide.
- Standalone viewer exports embed project data inside the HTML file.

For sensitive data, consider bundling dependencies locally, avoiding public hosted project links, disabling autosave, or reviewing the source before use.

---

## Known Limitations

- Very large spreadsheets may slow down or crash the browser.
- Export fidelity may vary by browser.
- CDN dependencies require internet access unless bundled locally.
- Google Sheets import requires a published CSV link, not a private sheet link.
- Relationships are materialized into joined tables rather than backed by a full query engine.
- Formula support is useful but not a full spreadsheet formula language.
- Autosave depends on browser local storage limits.
- Recent projects are local to one browser/device.
- Static site ZIP export depends on JSZip availability.
- PDF/PPT/PNG export depends on browser rendering and third-party export libraries.
- The mobile viewer is for finished dashboards, not editing.
- The current implementation is still mostly single-file HTML, which is convenient but harder to maintain at scale.

---

## Keyboard and Interaction Notes

Useful interactions:

- Drag a widget header to move it.
- Resize widgets using the bottom-right resize handle. Widget size is saved to project state and should persist when changing pages.
- Right-click a widget for the context menu.
- Click **Edit** on a widget to open the Configure inspector.
- Use page tabs to switch pages.
- Use **Duplicate Page** to copy a page.
- Use **Undo** and **Redo** for recent changes.
- Use **Restore** to recover autosaved work.
- Use **Home** to reopen the startup dialog.

Shortcuts:

```text
Ctrl/Cmd + K          Open command palette
Ctrl/Cmd + Shift + L  Toggle left panel
Ctrl/Cmd + Shift + R  Toggle right panel
Escape                Close overlays/menus where supported
```

---

## Development Notes

DataBench currently ships as static HTML files. This makes distribution easy, but the project is large enough that future development would benefit from splitting shared logic into modules.

A future source layout could look like:

```text
src/
├── editor/
│   ├── app.js
│   ├── canvas.js
│   ├── inspector.js
│   ├── home.js
│   ├── data-prep.js
│   └── exports.js
├── viewer/
│   ├── viewer.js
│   ├── layout.js
│   ├── filters.js
│   └── project-loader.js
├── shared/
│   ├── state.js
│   ├── data.js
│   ├── formulas.js
│   ├── charts.js
│   ├── widgets.js
│   ├── filters.js
│   ├── migrations.js
│   ├── themes.js
│   └── exports.js
└── styles/
    ├── editor.css
    └── viewer.css
```

A Vite or similar build setup could eventually make the app easier to test, bundle, and maintain while still exporting static files.

---

## Roadmap Ideas

Potential future improvements:

- Fully bundled offline build
- Shared editor/viewer module architecture
- Dedicated `vendor/` dependency folder for static hosting
- Test suite for formulas, filters, joins, autosave, migration, and exports
- Better formula editor with validation and previews
- More chart types: histogram, area, stacked bar, heatmap, gauge, combo chart
- Drag-and-drop field buckets for chart building
- Improved pivot table controls
- More dashboard templates
- More text/report widgets
- Image widgets
- Better accessibility and keyboard navigation
- More robust project schema migration tests
- Static publishing wizard
- Optional hosted/cloud version

---

## Contributing

Contributions are welcome. Good first areas to improve include:

- UI polish
- mobile viewer polish
- accessibility
- export reliability
- chart configuration options
- formula functions
- documentation
- sample datasets
- bug fixes
- project schema migration
- offline dependency bundling
- test coverage

Before making large changes, consider opening an issue or discussion describing the proposed direction.

---

## Suggested GitHub Description

> A browser-based spreadsheet-to-dashboard workbench with charts, pivots, data prep, themes, autosave, JSON projects, publishing exports, and a mobile dashboard viewer.

---

## Suggested Topics

```text
data-visualization dashboard csv xlsx spreadsheet chartjs business-intelligence pivot-table html css javascript no-build browser-app mobile-viewer static-site dataviz
```

---

## License

Choose a license that matches your goals. If you want broad reuse, the MIT License is a common choice for small web tools.

---

## Acknowledgments

DataBench builds on excellent browser-based open-source tools for spreadsheet parsing, chart rendering, and document export.
