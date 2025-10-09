# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a static web dashboard for visualizing blob scaling metrics, designed to be hosted on GitHub Pages. It's a single-page application using vanilla HTML, CSS, and JavaScript with Chart.js for data visualization.

## Commands

Since this is a static website with no build process:
- **Run locally**: Open `index.html` directly in a browser or use a local web server (e.g., `python -m http.server 8000` or `npx serve`)
- **No build/lint/test commands** - This is a static site with no build tooling

## Architecture

The entire application consists of two files:

1. **index.html**: Single-page dashboard containing:
   - All HTML structure, CSS styles (embedded), and JavaScript logic
   - Chart.js integration for line chart visualization
   - Metrics calculation (current target, growth rates based on target values)
   - Responsive design for mobile/desktop

2. **data.json**: Static JSON file with Ethereum hard fork blob parameters:
   - Contains a `blobData` array with objects having `date`, `upgrade-name`, `target`, and `max` properties
   - `upgrade-name`: name of the Ethereum hard fork (e.g., "Dencun", "Pectra", "Fusaka")
   - `target`: target blobs per block for that hard fork
   - `max`: maximum blobs per block for that hard fork
   - `projected` (optional): boolean indicating if the data point is a future projection
   - Currently contains historical data (Dencun) and projected upgrades (Pectra, Fusaka with BPOs)
   - Used to visualize Ethereum's blob scaling progression over time

## Key Implementation Details

- **Chart.js Configuration**: The chart displays two datasets:
  - Target values (dashed green line)
  - Max capacity (dashed red line)
  - Uses smooth curves (`tension: 0.4`), custom colors, and responsive sizing
- **Data Processing**: JavaScript fetches `data.json` and calculates:
  - Current target value (last data point's target)
  - Monthly target growth (percentage change between last two target points)
  - Total target growth (percentage change from first to last target point)
- **No Backend**: All data is static; updates require modifying `data.json` and committing changes

## Development Notes

- The dashboard automatically adapts to the data in `data.json` - to update metrics, modify the JSON file
- Chart.js is loaded from CDN (version 4.2.1), no local dependencies
- CSS uses modern features (CSS variables, gradients, flexbox) - test in modern browsers