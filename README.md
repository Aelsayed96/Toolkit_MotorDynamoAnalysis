# Dynamometer Analysis Toolkit

<p align="center">
  <img src="https://ar.wikipedia.org/wiki/%D9%85%D9%84%D9%81: -group-logo.png" height="80" alt="  Group"/>
</p>

<p align="center">
  <strong>A unified, browser-based dynamometer data reader and analyzer for motor performance engineering.</strong><br/>
  Supports Magtrol MDF files and Chinese dynamometer Excel exports — no installation required.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/platform-Browser-blue?style=flat-square"/>
  <img src="https://img.shields.io/badge/license-Proprietary-red?style=flat-square"/>
  <img src="https://img.shields.io/badge/built%20by- %20Group-orange?style=flat-square"/>
  <img src="https://img.shields.io/badge/stack-HTML%20%2F%20JS%20%2F%20Chart.js-yellow?style=flat-square"/>
</p>

---

## Overview

The **Dynamometer Analysis Toolkit** is a single-file, self-contained web application for loading, analyzing, and exporting motor test data from dynamometer rigs. It is designed for motor test engineers and production QA teams who need fast, accurate performance region extraction and reporting — directly in the browser, with no backend required.

### Key Capabilities

| Feature | Description |
|---|---|
| **Multi-format file support** | Magtrol `.MDF`, standard `.CSV`, Chinese dyno `.XLS`/`.XLSX` |
| **Automatic region extraction** | Locked rotor, No-load, Max torque, Max power output, custom regions |
| **Rated point definition** | By output power, speed, or fan-curve load torque equation |
| **Motor comparison** | Overlay two motors side-by-side with performance delta tables |
| **Batch statistics** | Summary, distribution histograms, and box plots across many test files |
| **Stats session compare** | Load a previous stats snapshot JSON and compare against current session |
| **PDF export** | Themed, chart-embedded PDF reports for all pages |
| **LaTeX export** | Structured data export for LaTeX-based reporting pipelines |

---

## Screenshots



---

## Getting Started

The tool is a **single HTML file** — no build step, no server, no dependencies to install.

### Option A — Open directly

1. Download `index.html` from this repository.
2. Open it in any modern browser (Chrome, Edge, Firefox).
3. Enter the access password when prompted.
4. Drop or browse to your dynamometer file.

### Option B — Serve locally (recommended for large files)

```bash
# Python
python -m http.server 8080

# Node.js
npx serve .
```

Then visit `http://localhost:8080`.

---

## Supported File Formats

### Magtrol `.MDF` / Standard `.CSV`

Column aliases are fully configurable in the **Config** tab. Default expected headers:

| Signal | Default Alias |
|---|---|
| Speed | `Speed`, `RPM`, `n` |
| Torque | `Torque`, `T`, `Nm` |
| Input Power | `Pin`, `Power_in` |
| Output Power | `Pout`, `Power_out` |
| Current | `I`, `Current`, `A` |
| Voltage | `V`, `Voltage`, `U` |
| Efficiency | `Eta`, `Eff`, `%` |
| Power Factor | `PF`, `CosPhi` |

### Chinese Dynamometer `.XLS` / `.XLSX`

The parser auto-detects the sheet structure. Row offset and column mapping are adjustable in **Config → Chinese Dyno**.

---

## Application Pages

### ⊞ Analyze

The main single-file analysis page.

- Upload a file via drag-and-drop or file browser
- Configure MDF column mapping and test metadata
- Extract all operating regions automatically
- View interactive performance curves (All / Efficiency / Power sub-tabs)
- Inspect the region table with all calculated parameters
- Export a styled PDF report

**Region extraction settings:**
- Locked rotor threshold (speed, torque, or current)
- No-load threshold
- Rated point: by Pout, speed, or fan-curve torque equation
- Custom region: define by any parameter range, with directional search (high-speed → or low-speed →)

### ⊟ Compare

Side-by-side tabular comparison of two or more processed files. Highlights parameter deltas. Exports to PDF.

### ⊡ Compare Motors

Full overlay analysis for two motors (Motor A vs Motor B). Features:

- Separate file upload per motor
- Independent region configuration
- Overlay charts: All / Efficiency & PF / Power / Torque / Current
- Delta (Δ) toggle on comparison table
- PDF export with embedded overlay charts

### ⊠ Statistics

Batch analysis across a fleet of test files.

- Summary table of all region parameters
- Distribution histograms per parameter
- Box plots for spread visualization
- Export stats snapshot to JSON (for later session comparison)
- Export average curve PDF and full stats PDF

### ⊠⊟ Stats Compare

Load a previously saved stats JSON and compare it against the current session:

- Avg curve overlay (current vs previous)
- Side-by-side stats table
- Box plot comparison

### ⚙ Config

Global tool configuration:

- Column alias mapping for Magtrol / CSV format
- Column mapping for Chinese dynamometer format
- UI theme options

### 🖋 Settings

Per-session display and reporting preferences.

---

## Region Definitions

| Region | Detection Logic |
|---|---|
| **Locked Rotor** | Speed below locked-rotor speed threshold |
| **No-Load** | Torque below no-load torque threshold |
| **Max Torque** | Point of maximum torque on the curve |
| **Max Pout** | Point of maximum output power on the curve |
| **Rated** | Defined by: (a) target Pout, (b) target speed, or (c) fan-load torque equation `T = k·n²` |
| **Custom** | User-defined parameter + value range, with search direction (high-speed ↓ or low-speed ↑) |

---

## Export Formats

### PDF Report
Themed PDF with:
- Test metadata header
- Embedded Chart.js chart images (canvas-captured)
- Region parameter table
- Per-region performance values

### LaTeX / JSON
Structured data export for integration into automated report pipelines.

---

## Tech Stack

| Library | Version | Purpose |
|---|---|---|
| [Chart.js](https://www.chartjs.org/) | 4.4.1 | Interactive performance curve charts |
| [PapaParse](https://www.papaparse.com/) | 5.4.1 | CSV parsing |
| [SheetJS (xlsx)](https://sheetjs.com/) | 0.18.5 | Excel file reading |
| Native Browser APIs | — | PDF generation via `window.print()`, file drag-and-drop |

No frameworks. No build tools. Pure HTML + JavaScript.

---

## Project Structure

```
Toolkit_MotorDynamoAnalysis/
└── index.html        # Complete self-contained application
```

---

## Roadmap

- [ ] Dark mode theme toggle
- [ ] Multi-file batch analyze with curve overlay
- [ ] Direct Magtrol binary MDF v5 support
- [ ] Configurable report template (logo, company name)
- [ ] CSV export of extracted region table

---

## Contributing

This is an internal   Group engineering tool. For bug reports or feature requests, please open an issue or contact the Motor Testing team directly.

---

## License

Proprietary —   Group. All rights reserved.

Not for redistribution without written permission.
