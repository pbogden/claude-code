# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is an Observable Framework application - a framework for building data apps, dashboards, and reports using reactive JavaScript and Markdown. Observable Framework uses file-based routing where Markdown files in the `src/` directory become pages.

## Build & Development Commands

```bash
# Install dependencies (uses Yarn with PnP - Plug'n'Play)
yarn install

# Start local dev server at http://localhost:3000
yarn dev

# Build static site to ./dist
yarn build

# Clear data loader cache
yarn clean

# Deploy to Observable
yarn deploy
```

## Architecture

### File-Based Routing
- Pages are Markdown files in `src/` - the filename determines the URL path
- `src/index.md` is the home page
- Nested folders create nested routes (e.g., `src/example-dashboard.md` → `/example-dashboard`)

### Key Directories
- **`src/data/`**: Data loaders (e.g., `.csv.js`, `.json.js` files that fetch/process data) and static data files
- **`src/components/`**: Shared JavaScript modules that can be imported into Markdown pages
- **`src/.observablehq/cache/`**: Auto-generated cache for data loaders (ignored in git)

### Configuration
- **`observablehq.config.js`**: Main config file
  - Controls title, sidebar navigation, theme, header/footer
  - `root: "src"` defines source directory
  - Can configure pages array for custom sidebar organization

### Data Loaders
Data loaders are executable scripts (`.csv.js`, `.json.js`, etc.) that run at build time to fetch or generate data. They output to stdout and are cached in `src/.observablehq/cache/`.

### Package Management
This project uses Yarn with Plug'n'Play (PnP). The `.pnp.cjs` and `.pnp.loader.mjs` files handle module resolution instead of `node_modules/`.

## Important Notes

- The app requires Node.js ≥18
- Built pages go to `dist/` directory
- Observable Framework supports reactive JavaScript blocks in Markdown using fenced code blocks
- Hot reloading works during `yarn dev`
