# CSV / TSV / XLSX / JSON Viewer

Browser-based viewer for CSV, TSV, Excel, and JSON files with inline row filtering. No server, no upload — everything runs locally in your browser.

<!-- ![Viewer](screenshots/viewer.png) -->

## Tools

### CSV / TSV Viewer
View CSV and TSV files as a full table with inline row filtering.

- **Configurable delimiter** — comma, semicolon, or tab; defaults to auto-detect (samples the first 10 lines to pick the most consistent delimiter)

### XLSX Viewer
View Excel files (.xlsx, .xls, .xlsm, .xlsb, .ods). Powered by [SheetJS](https://sheetjs.com/).

- Automatically parses **all sheets** in each workbook
- Each sheet appears as a separate entry in the file list

### JSON Viewer
View JSON files as a table.

- Supports **array of objects** (`[{...}, {...}]`) and **JSON Lines / NDJSON** (one object per line)
- Supports **keyed objects** (`{"id": {...}, ...}`) — shown as key/value rows
- **Expand values** — for keyed objects, switches to an interactive tree view: each key is collapsible, nested objects expand recursively into child rows
- Filter works across all tree nodes including collapsed ones — matching entries are auto-expanded

## What it does

Load one or more files and view them as a full table. Enter filter terms to narrow down the visible rows — matching cells are highlighted inline. Clear the filter to see all rows again.

These are the viewer companions to [CSV & XLSX Search](https://github.com/ExpandYourself/csv-xlsx-search). The key difference: instead of listing individual cell matches, the viewer shows complete rows in their original table structure.

## Features

Both tools share the same feature set:

- **Full table view** — all columns visible, rows displayed with their original structure
- **Inline row filtering** — matching rows stay visible, non-matching rows are hidden
- **Cell highlighting** — matched cells are marked with a yellow left border
- **Multi-file support** — load and filter across multiple files at once
- **Sortable columns** — click any column header to sort; click `#` to restore original row order
- **Sticky header & row numbers** — header row and row number column stay visible while scrolling
- **Wrap text toggle** — per-file toggle for long cell values
- **Match types** — partial match, exact match, or wildcard patterns
- **Wildcard syntax** — asterisk style (`*`, `?`) or SQL style (`%`, `_`)
- **Multiple filter terms** — comma-separated, combined with AND or OR
- **Match scope** — row-wide or cell-level matching (affects AND behaviour)
- **Case sensitivity** — toggle case-sensitive matching
- **Auto-filter** — results update as you type (with debounce)
- **Pagination** — configurable rows per page (50 / 100 / 250 / 500 / 1000)
- **CSV export** — export the currently filtered rows; multi-file/sheet export adds `file` and `sheet` columns
- **Privacy** — all processing happens in the browser, no data leaves your machine

## Usage

### Option 1: GitHub Pages
Visit the hosted version: **https://expandyourself.github.io/csv-viewer/**

### Option 2: Download
1. Download [`index.html`](index.html)
2. Open it in any modern browser
3. Load your files and start browsing

No install, no dependencies, no build step. Format is auto-detected from the file extension — just open any CSV, TSV, XLSX, or JSON file directly.

The individual viewers ([`csv-viewer.html`](csv-viewer.html), [`xlsx-viewer.html`](xlsx-viewer.html), [`json-viewer.html`](json-viewer.html)) remain available for standalone use.

## Filter Modes

### Match Type
| Mode | Behaviour |
|---|---|
| Partial match | Term appears anywhere in the cell value |
| Exact match | Cell value equals the term exactly |
| Wildcard | `*` / `%` match any number of characters, `?` / `_` match exactly one |

### Multiple Terms (comma-separated)
- **OR** — a row is shown if any term matches
- **AND** — a row is shown only if all terms match (behaviour depends on scope)

### Match Scope
- **Row** — terms are matched across the entire row. With AND, each term must appear in at least one cell of the row (different cells are fine).
- **Cell** — terms are matched per cell. With AND, a single cell must contain all terms simultaneously.

**Example:** Filter `Smith, Engineering` with AND + Row scope finds rows where one cell contains "Smith" and another (or the same) contains "Engineering".

## License

[MIT](LICENSE)
