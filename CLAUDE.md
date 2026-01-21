# CLAUDE.md - Project Guide for Claude Code

## Project Overview

This is a **procurement analysis presentation** for lumber purchasing decision-making. It presents a business case for purchasing STK (Select Tight Knot) rustic channel cedar siding lumber at current seasonal low prices (Jan/Feb 2026) rather than waiting until March when prices are projected to increase.

**Core Recommendation:** Execute purchase at $3.40/linear foot in Jan/Feb 2026 to avoid the projected $3.70/lf March price (+9% seasonal premium).

## Tech Stack

- **HTML5** - Single-page application structure
- **Tailwind CSS** (CDN) - Styling framework
- **Chart.js** (CDN) - Price projection visualization
- **chartjs-plugin-annotation** (CDN) - Timeline markers on charts
- **Vanilla JavaScript** - Chart rendering and interactivity

**No build process required** - all dependencies are CDN-delivered.

## File Structure

```
cedar-presentation/
├── index.html          # Main presentation (all UI, styling, and logic)
├── README.md           # Basic project info
├── CLAUDE.md           # This file
└── docs/
    ├── Cedar Siding Market Assessment Inquiry - Google Docs.pdf
    └── Cedar Siding Quotes.xlsx   # Vendor quote data (7 suppliers)
```

## Running the Project

Simply open `index.html` in any modern browser:
```bash
open index.html
```

No server, build tools, or installation required.

## Key Data Points

Located in `index.html`:

| Data | Value | Location |
|------|-------|----------|
| Current price (Jan/Feb) | $3.40/lf | Line 63 |
| Projected March price | $3.47/lf | Line 68 |
| Material needed | 120k-140k LF | Lines 72-74 |
| Seasonal variance | 2-5% | Based on FRED PPI data (WPU084903, 2005-2023) |

### Vendor Quote Data (from docs/Cedar Siding Quotes.xlsx)

| Vendor | Location | Price/LF |
|--------|----------|----------|
| Legacy Pre-Finishing | NC | $3.40 |
| Interstate | CT | $3.44 |
| Buffalo Lumber | TN | $3.77 |
| Lyon & Billard | CT | $3.80 |
| Builder's FirstSource | CT | $3.93 |
| Ring's End | CT | $4.04 |
| Liberty Cedar | RI | $4.10 |

**Key metrics:**
- Vendor spread: $0.70/lf (21%)
- 140k LF: Best vs Worst = $98,000 difference
- 140k LF: Best vs Next-tier ($3.77) = $51,800 difference

### Price Projection Arrays (Lines ~340-350)
- `dataMean` - Mean projection based on 2-5% seasonal swing (FRED PPI data)
- `dataHigh` - Upper bound (~8% swing, higher volatility)
- `dataLow` - Lower bound (~2% swing, stable market)

## Content Sections in index.html

1. **Header** (31-45) - Sticky nav with recommendation status
2. **Executive Summary** (49-104) - Key metrics and STK vs Clear context
3. **Vendor Comparison** (106-213) - Current market quotes from 7 vendors with cost analysis
4. **Price Forecast Chart** (215-232) - 12-month Chart.js visualization
5. **Financial Scenarios** (234-330) - Three quantity models + vendor risk scenario
6. **Data Sources** (332-365) - Verified source links, tariff info, and methodology

## Important Conventions

### Data Accuracy
- All price projections use **documented 10-15% seasonal variance** (industry standard)
- January $3.40/lf is a **secured vendor quote**, not an estimate
- Sources are cited in the footer with links to CME Group, Madison's, NAHB, BC Gov

### Design Patterns
- Color scheme: Teal primary (#0F766E), Cedar accent (#B45309)
- Emerald for positive/current prices, Rose for risk/higher prices
- The 140k LF scenario is highlighted as "LIKELY SCOPE" with visual emphasis

### Calculations
Financial scenarios follow this pattern:
- Jan/Feb cost = Quantity × $3.40
- March cost = Quantity × $3.47
- Loss = March cost - Jan/Feb cost (e.g., 140k LF = $9,800)

## Common Tasks

### Update Price Data
1. Modify `dataMean`, `dataHigh`, `dataLow` arrays (lines 234-241)
2. Update the stat cards if Jan/Feb or March prices change (lines 61-75)
3. Recalculate financial scenarios if prices change (lines 131-192)
4. Update methodology note if variance assumptions change (line 216)

### Add New Quantity Scenario
Copy an existing scenario card structure (e.g., lines 133-150) and update:
- Quantity header
- Calculations for both price points
- Loss calculation

### Modify Chart Appearance
Chart configuration is in the `new Chart()` call (lines 240-332):
- Y-axis range: lines 323-324 (currently 3.30-3.80)
- Colors: lines 248-249 (mean), 259 (uncertainty fill)
- Annotation line: lines 300-318

## Git Workflow

Remote: `https://github.com/dissidentcode/cedar-presentation.git`
Main branch: `master`

Commit messages should describe what changed and why, especially when adjusting financial projections or data sources.
