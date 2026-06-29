# DataBench

**DataBench** is a browser-based data visualization and analysis workbench for quick spreadsheet-to-dashboard exploration.

Upload a CSV or XLSX file, generate default table and summary pages, build charts on a multi-page canvas, create calculated fields, link datasets, apply filters, customize themes, and export your work as JSON, HTML, PNG, PDF, PowerPoint, or a mobile-friendly viewer file.

DataBench is designed for fast, lightweight, “good enough to understand the data” analysis without setting up a database, BI server, notebook, or build system.

---

## Current Version

**DataBench Editor v1.4.1**  
**DataBench Viewer v1.0-style initial release**

The project currently ships as static browser files:

- `databench.html` — the full desktop-oriented editor/workbench
- `databench-viewer.html` — a mobile-friendly dashboard viewer

Both are plain HTML/CSS/JS files that can be opened locally or hosted on a static web server.

---

## Highlights

- Runs in the browser with no backend required
- Uploads CSV and XLSX files
- Imports published Google Sheets CSV links
- Creates default table pages for uploaded datasets
- Creates automatic data summary pages
- Supports multi-page dashboard canvases
- Adds draggable, resizable widgets
- Supports charts, tables, KPI cards, summaries, and pivot tables
- Provides dimensions, measures, aggregations, and calculated fields
- Links datasets using matching key fields
- Saves and loads full projects as JSON
- Includes autosave with an LED-style save-status indicator
- Includes light, dark, professional, and playful UI themes
- Exports to HTML, PNG, PDF, PPTX, JSON, CSV, and standalone mobile viewer HTML
- Includes a separate mobile-friendly viewer for sharing finished dashboards

---

## Quick Start

1. Download or clone this repository.
2. Open `databench.html` in a modern browser.
3. Click **Load Sample Project** to explore the app immediately, or upload your own CSV/XLSX file.
4. Use the canvas to add and arrange tables, charts, KPI cards, summaries, and pivot tables.
5. Save your work with **Save Project JSON**.
6. To share a mobile-friendly version, use **Mobile Viewer** from the export toolbar.

No installation is required for basic use.

---

## Recommended Repository Structure

For local development or static hosting, use this structure:

```text
.
├── index.html              # DataBench editor, copied from databench.html
├── viewer/
│   └── index.html          # DataBench viewer, copied from databench-viewer.html
├── projects/
│   └── example.databench.json
├── README.md
└── LICENSE
```

If you prefer to keep the original file names during development, a minimal repository can also look like this:

```text
.
├── databench.html
├── databench-viewer.html
├── README.md
└── LICENSE
```

---

## Suggested Deployment Layout

The editor and viewer are designed to work together with this hosted layout:

```text
/databench/           # editor
/databench/viewer/    # viewer
/databench/projects/  # optional hosted project JSON files
```

Recommended deployment files:

```text
databench/
  index.html              # use databench.html here
  viewer/
    index.html            # use databench-viewer.html here
  projects/
    example.databench.json
```

With this layout:

- The editor’s **Open Viewer** button opens `./viewer/`.
- The viewer’s **Editor** button returns to `../`.
- The viewer can load a hosted project with a URL parameter:

```text
/databench/viewer/?project=../projects/example.databench.json
```

---

## Editor vs Viewer

DataBench now has two related experiences.

### DataBench Editor

The editor is the full workbench. Use it to:

- Upload files
- Import Google Sheets CSV links
- Create charts and dashboard pages
- Build pivot tables
- Define calculated fields
- Link datasets
- Configure filters
- Customize themes
- Save project JSON
- Export PDF, PPTX, PNG, HTML, CSV, and mobile viewer files

### DataBench Viewer

The viewer is for reading, presenting, and sharing finished dashboards. It is mobile-friendly and intentionally simpler than the editor.

Use it to:

- Open a `.databench.json` project file
- Open a hosted project with `?project=...`
- Open a standalone viewer HTML file exported from the editor
- Browse dashboard pages
- View charts, tables, KPIs, summaries, and pivot tables
- Use page filters and chart click-to-filter behavior
- View widgets in full-screen mode

The viewer does not include authoring tools like upload parsing, joins, calculated-field editing, widget dragging/resizing, or export configuration.

---

## Data Transfer Between Editor and Viewer

There are three supported transfer paths.

### 1. Manual Project JSON

In the editor:

1. Click **Save Project JSON**.
2. Open the viewer.
3. Load the saved JSON file.

This is the simplest portable workflow.

### 2. Standalone Mobile Viewer HTML

In the editor:

1. Build a dashboard.
2. Click **Mobile Viewer**.
3. Share the exported `.databench.viewer.html` file.

The exported viewer HTML contains the project data embedded inside the file, so the recipient does not need the editor.

### 3. Hosted Project URL

Host a project JSON file, then open it in the viewer with a URL like:

```text
/databench/viewer/?project=../projects/example.databench.json
```

This is useful for static websites, intranets, GitHub Pages, Netlify, Cloudflare Pages, and similar hosting.

---

## Browser Requirements

Recommended browsers:

- Chrome / Chromium
- Edge
- Firefox
- Safari

For best results, use a current desktop browser for editing. The viewer is optimized for phones and tablets, but very large datasets can still strain mobile browsers.

---

## External Libraries

DataBench uses CDN-loaded browser libraries for spreadsheet parsing, charts, and exports.

Commonly used libraries include:

- **SheetJS** for XLSX parsing
- **Chart.js** for chart rendering
- **html2canvas** for canvas/page image export
- **jsPDF** for PDF export
- **PptxGenJS** for PowerPoint export

Because these are loaded from CDNs, internet access is currently required for full functionality unless the dependencies are bundled locally in a future release.

---

## Core Concepts

### Data Sources

A data source is an uploaded or imported table. Sources can come from:

- CSV files
- XLSX files
- Published Google Sheets CSV URLs
- Built-in sample data
- Joined/materialized datasets created inside DataBench

Each uploaded source gets a default table page and a summary page.

### Pages

A project can contain multiple pages. Pages act like dashboard sheets or slides. Each page has a canvas where widgets can be placed and arranged.

### Widgets

Widgets are objects placed on a page. Current widget types include:

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

Widgets can be selected, configured, moved, resized, duplicated, deleted, and exported.

### Dimensions and Measures

DataBench uses a simple BI-style model:

- **Dimensions** group or categorize rows.
- **Measures** calculate numeric or count-based values.

Example:

- Dimension: `Department`
- Measure: `Sales`
- Aggregation: `sum`

This produces total sales by department.

### Aggregations

Supported aggregation functions include:

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

### Calculated Fields

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

Field names with spaces can be referenced using brackets:

```text
[Order Date]
[Total Revenue]
```

### Relationships and Joins

DataBench can link tables using shared key fields. The Data Model tools can:

- Suggest matching key fields
- Preview match counts
- Warn about blank keys
- Warn about duplicate keys
- Save relationships
- Materialize relationships into joined tables
- Create left joins or inner joins

### Filters

Filters can be applied at the page or widget level.

Supported filter operators include:

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

Charts can also support click-to-filter behavior for quick exploration.

---

## Theme Studio

DataBench includes built-in themes ranging from professional to playful.

Examples include:

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

- Accent colors
- App background
- Panel colors
- Text colors
- Canvas color
- Card color
- Grid color

---

## Autosave

DataBench includes browser-based autosave using `localStorage`.

Autosave behavior:

- Saves project state automatically as changes happen
- Debounces rapid edits
- Periodically flushes unsaved changes
- Saves before tab close when possible
- Saves when the tab becomes hidden
- Maintains a backup autosave copy
- Can restore from current or older autosave slots

The header includes an LED-style autosave indicator:

- **Dark** means there are unsaved changes or autosave is pending.
- **Green/lit** means the latest state has been saved.
- **Red** means autosave failed, usually because storage is unavailable or full.

Autosave is convenient, but project JSON remains the safest long-term storage format.

---

## Saving and Loading Projects

Use **Save Project JSON** to download a `.json` project file. Use **Load JSON** to restore a saved project.

Project JSON stores the project structure, including:

- Version metadata
- Data sources
- Pages
- Widgets
- Filters
- Relationships
- Calculated fields
- Theme settings
- Viewer settings

Suggested project extension:

```text
.databench.json
```

---

## Export Options

DataBench includes several export tools.

### Save Project JSON

Saves the editable project file.

### Export Mobile Viewer

Exports a standalone, mobile-friendly viewer HTML file with the current project embedded.

This is the recommended way to share a finished dashboard with people who do not need editing tools.

### Open Viewer

Opens the viewer app at `./viewer/` when using the recommended deployment layout.

### Export HTML

Exports the current project/page as browser-viewable HTML.

### Export PNG

Exports the current page as an image.

### Export PDF

Exports project pages into a PDF document.

### Export PPTX

Exports project pages as slides in a PowerPoint deck.

### Export CSV

Exports selected widget/source data as CSV.

Export quality depends on browser rendering, loaded chart libraries, and available memory.

---

## Keyboard and Interaction Notes

Useful interactions include:

- Drag a widget header to move a widget.
- Resize widgets using resize handles.
- Right-click a widget to open a context menu.
- Use the inspector to edit selected widget settings.
- Use page tabs to switch between dashboard pages.
- Use **Undo** and **Redo** for recent changes.
- Use **Restore Autosave** to recover the last autosaved project.

Panel shortcuts:

- `Ctrl/Cmd + Shift + L`: toggle the left panel
- `Ctrl/Cmd + Shift + R`: toggle the right panel

---

## Known Limitations

DataBench is intentionally lightweight and browser-only. Current limitations include:

- Very large files may slow down or crash the browser.
- Export fidelity may vary by browser.
- CDN dependencies require internet access.
- Google Sheets import requires a published CSV link, not a private sheet link.
- Relationships are materialized into joined tables rather than backed by a full query engine.
- Formula support is useful but not a complete spreadsheet formula language.
- Autosave depends on browser local storage limits.
- The mobile viewer is optimized for finished dashboards, not dashboard editing.
- The app currently uses a single-file architecture, which is convenient but harder to maintain as the project grows.

---

## Privacy Notes

DataBench runs in the browser. Uploaded files are processed locally by the app unless you modify the code to send data elsewhere.

Important notes:

- Files are not intentionally uploaded to a server by DataBench.
- Autosave data is stored in the browser’s local storage.
- CDN libraries are loaded from third-party URLs.
- Published Google Sheets CSV imports fetch data from the provided URL.
- Hosted project links load project JSON from the URL you provide.

For sensitive data, consider bundling dependencies locally, avoiding public hosted project links, and reviewing the source before use.

---

## Development Notes

The current version is implemented as static HTML files. This makes distribution easy, but future development may benefit from splitting the code into modules.

A future source layout might look like this:

```text
src/
├── editor/
│   ├── app.js
│   ├── canvas.js
│   ├── inspector.js
│   └── exports.js
├── viewer/
│   ├── viewer.js
│   ├── layout.js
│   └── project-loader.js
├── shared/
│   ├── state.js
│   ├── data.js
│   ├── formulas.js
│   ├── charts.js
│   ├── widgets.js
│   ├── filters.js
│   └── themes.js
└── styles/
    ├── editor.css
    └── viewer.css
```

A Vite or similar build setup could eventually make the app easier to test, bundle, and maintain.

---

## Roadmap Ideas

Potential future improvements:

- Fully bundled offline build
- Shared editor/viewer module architecture
- More polished mobile viewer navigation
- Hosted static-site export package
- QR code for viewer links
- More polished export templates
- More chart types
- Better formula editor with validation
- Field drag-and-drop builder
- Improved pivot table controls
- Dashboard layout templates
- Dataset cleanup tools
- Column rename/type management
- Better accessibility and keyboard navigation
- Test suite for formulas, filters, joins, autosave, and project migration
- Optional hosted/cloud version

---

## Contributing

Contributions are welcome. Good first areas to improve include:

- UI polish
- Mobile viewer polish
- Accessibility
- Export reliability
- Chart configuration options
- Formula functions
- Documentation
- Sample datasets
- Bug fixes
- Project schema migration

Before making large changes, consider opening an issue or discussion describing the proposed direction.

---

## Suggested GitHub Description

> A browser-based spreadsheet-to-dashboard workbench with charts, pivots, themes, JSON projects, autosave, exports, and a mobile dashboard viewer.

---

## Suggested Topics

```text
data-visualization dashboard csv xlsx spreadsheet chartjs business-intelligence pivot-table html css javascript no-build browser-app mobile-viewer
```

---

## License

Choose a license that matches your goals. If you want broad reuse, the MIT License is a common choice for small web tools.

---

## Acknowledgments

DataBench builds on excellent browser-based open-source tools for spreadsheet parsing, chart rendering, and document export.
