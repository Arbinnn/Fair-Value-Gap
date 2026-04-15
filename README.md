# Fair Value Gap Detection on NEPSE Data

This project analyzes Nepal Stock Exchange (NEPSE) OHLCV data to detect and evaluate **Fair Value Gaps (FVGs)**.

The workflow is notebook-based and uses pandas + NumPy for analysis and Plotly for interactive charts.

## What This Project Does

- Detects bullish and bearish FVGs with a 3-candle pattern
- Filters weak gaps using a minimum gap threshold (default: 0.5%)
- De-duplicates continuous FVG sequences by keeping the strongest gap
- Finds FVG re-entry points and evaluates forward performance by horizon
- Builds summary tables for:
  - Bullish vs Bearish
  - Sector-wise performance (one dataframe per sector)
- Visualizes grouped bars for Return, MAE, and MFE:
  - X-axis: horizon
  - Bullish bars on the left, Bearish bars on the right
  - Metric value shown above each bar
  - Win-rate labels shown on the left/right side of each bar

## FVG Logic Summary

For candle index `i` (using candles `i-2`, `i-1`, `i`):

- **Bullish FVG**: `Low[i] > High[i-2]`
- **Bearish FVG**: `High[i] < Low[i-2]`

Additional rules:

- Gap must be at least **0.5%** of reference price
- For consecutive (continuous) FVG bars, only the FVG with the **highest gap size** is retained

## Project Structure

- `data/`: Multi-file dataset (sector CSV files)
- `NEPSE/nepse.csv`: Single-file dataset
- `NEPSE/nepse.ipynb`: Original single-file analysis notebook
- `fvg_all_data.ipynb`: Combined all-files analysis notebook

## Setup

1. Create virtual environment:
   - `py -m venv .venv`
2. Activate on PowerShell:
   - `\.venv\Scripts\Activate.ps1`
3. Install dependencies:
   - `pip install pandas numpy plotly jupyter ipykernel`
4. Open in VS Code or Jupyter and run cells in order.

## Notebook Usage

### Single-file workflow

- Open `NEPSE/nepse.ipynb`
- Uses `NEPSE/nepse.csv`

### All-data workflow

- Open `fvg_all_data.ipynb`
- Automatically reads all `*.csv` files in `data/`
- Adds `Sector` from each CSV filename
- Produces:
  - `summary_by_type`
  - `summary_by_sector`
  - `sector_dataframes` (dictionary of one dataframe per sector)

## Chart Cells in `fvg_all_data.ipynb`

- Return comparison chart (Bullish vs Bearish by horizon)
- MAE comparison chart (Bullish vs Bearish by horizon)
- MFE comparison chart (Bullish vs Bearish by horizon)

Each chart is rendered for:

- All sectors combined
- Every sector dataframe in `sector_dataframes`

## Notes

- The optional candlestick chart uses the first symbol in the loaded dataset.
- To inspect another symbol, change symbol selection in the visualization cell.
