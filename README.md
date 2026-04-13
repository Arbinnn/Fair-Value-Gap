# Fair Value Gap Detection on NEPSE Data

This project analyzes Nepal Stock Exchange (NEPSE) OHLCV data to detect and visualize **Fair Value Gaps (FVGs)** on candlestick charts.

It uses a Jupyter notebook workflow with pandas for data processing and Plotly for interactive charting.

## What This Project Does

- Loads historical NEPSE data from `NEPSE/nepse.csv`
- Cleans and prepares OHLCV columns (`Open`, `High`, `Low`, `Close`, `Volume`)
- Detects bullish and bearish FVGs using a 3-candle structure
- Filters FVGs using a minimum gap threshold (currently 0.5%)
- Handles continuous FVG sequences by keeping the strongest gap (largest size)
- Plots candlestick charts with small pointer markers where valid FVGs occur

## FVG Logic Summary

For candle index `i` (using candles `i-2`, `i-1`, `i`):

- **Bullish FVG**: `Low[i] > High[i-2]`
- **Bearish FVG**: `High[i] < Low[i-2]`

Additional rules in this project:

- Gap must be at least **0.5%** of reference price
- For consecutive (continuous) FVG bars, only the FVG with the **highest gap size** is retained

## Project Structure

- `NEPSE/nepse.csv`: Input market data
- `NEPSE/nepse.ipynb`: Analysis notebook (data prep, FVG detection, Plotly visualization)

## Setup

1. Create virtual environment:
   - `py -m venv .venv`
2. Activate on PowerShell:
   - `.\.venv\Scripts\Activate.ps1`
3. Install dependencies:
   - `pip install pandas numpy plotly jupyter ipykernel`
4. Open the notebook:
   - `jupyter notebook`
   - or open in VS Code and run cells

## How To Use

1. Place or update your data in `NEPSE/nepse.csv`
2. Run notebook cells in order
3. Review detected FVG table output
4. View chart markers that indicate bullish/bearish FVG locations

## Notes

- Current plotting uses the first symbol found in the dataset.
- You can change symbol filtering in the notebook to inspect other symbols.
