# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Environment Setup

This project uses conda for environment management. The environment is defined in `environment.yml`:

```bash
conda env create -f environment.yml
conda activate ds
```

Key dependencies:
- Python 3.13
- pandas 2.2
- numpy 2.2
- seaborn (for data visualization)
- geopandas, geojson, contextily (for geospatial analysis)
- imageio

## Build and Run Commands

This project uses Make for task automation. All commands should be run from the repository root:

```bash
# Generate the ISLR2 Figure 1.1 chart (downloads data if needed)
make q1

# Download the Wage.csv dataset manually
make data/Wage.csv

# Clean downloaded data
make clean
```

To run scripts directly:
```bash
python -B src/q1.py  # -B flag prevents .pyc file generation
```

## Project Structure

```
ds/
├── src/           # Python source code
│   ├── q1.py      # Main script for generating ISLR2 Figure 1.1
│   └── readit.py  # Utility module for reading CSV data
├── data/          # Downloaded datasets (gitignored)
├── figs/          # Generated figures/visualizations
└── Makefile       # Build automation
```

## Architecture

**Data Pipeline**: The project follows a simple data science workflow:
1. Data acquisition via `readit.py` utility (downloads from GitHub repo)
2. Data processing and visualization in scripts like `q1.py`
3. Output saved to `figs/` directory

**readit module** (`src/readit.py`):
- Provides a `csv()` function that wraps pandas `read_csv()`
- Default data source: ISLR Wage dataset from `ds5110/rdata` GitHub repository
- Supports both URLs and local file paths

**Visualization scripts** (e.g., `src/q1.py`):
- Import data using the `readit` module
- Use seaborn/matplotlib for plotting
- Save figures to `figs/` directory
- Example: `q1.py` creates a 4th-order polynomial regression plot of age vs wage

## Data Management

- The `data/` directory is gitignored to avoid committing large datasets
- Data is fetched on-demand using Make targets
- Default data source is the ISLR (Introduction to Statistical Learning) Wage dataset
