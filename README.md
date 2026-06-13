# Stock Data Analytics Project (AAPL - 10 Year)

## Overview
This project performs end-to-end data analytics on 10 years of historical
stock data (default: AAPL), including data collection, cleaning,
preprocessing, feature engineering, exploratory data analysis (EDA), and
visualization — all done in Python (Google Colab).

## Project Structure
```
stock_eda_pipeline.py   # Main script (run in Google Colab)
AAPL_cleaned.csv         # Output: cleaned dataset with engineered features
```

## Requirements
- Google Colab (recommended) or Jupyter Notebook
- Python libraries: yfinance, pandas, numpy, matplotlib, seaborn

Install with:
```
pip install yfinance pandas numpy matplotlib seaborn
```

## Pipeline Steps

### 1. Data Collection
- Source: Yahoo Finance via `yfinance`
- Downloads 10 years of OHLCV (Open, High, Low, Close, Volume) data for a
  given ticker symbol.

### 2. Initial Inspection
- Checks shape, data types, missing values, duplicates, and summary
  statistics.

### 3. Data Cleaning
- Converts `Date` to datetime, numeric columns to proper float types
- Removes duplicate rows
- Fills missing price values via linear interpolation
- Fixes invalid (negative) volume values
- Caps outliers in price columns using the IQR method

### 4. Feature Engineering
- `Daily_Return`: day-over-day percentage change in closing price
- `MA_7`, `MA_30`, `MA_200`: 7/30/200-day moving averages
- `Volatility_30`: 30-day rolling standard deviation of returns
- `Year`, `Month`, `Weekday`: date-derived columns

### 5. Exploratory Data Analysis (EDA)
- Summary statistics for price, volume, and returns
- Yearly average closing price

### 6. Visualizations
- Closing price trend with 30-day and 200-day moving averages
- Trading volume over time
- Daily returns distribution (histogram)
- 30-day rolling volatility over time
- Correlation heatmap (Open, High, Low, Close, Volume, Daily Return)
- Yearly average closing price (bar chart)
- Boxplot of price columns for outlier inspection

## How to Run
1. Open Google Colab.
2. Paste the contents of `stock_eda_pipeline.py` into a cell (or split by
   the `# STEP` comments into separate cells).
3. Change the `ticker` variable to the desired company's stock symbol.
4. Run all cells in order.
5. The cleaned dataset is saved as `<ticker>_cleaned.csv` and downloaded
   automatically.

## Customization
- Change the date range in `yf.download(ticker, start=..., end=...)`.
- Adjust the IQR multiplier (default 1.5) for stricter/looser outlier
  capping.
- Add additional technical indicators (RSI, MACD, Bollinger Bands) as
  needed.

## Notes
- Rolling-window features (`MA_30`, `MA_200`, `Volatility_30`) will have
  `NaN` values for the initial rows, which is expected behavior.
- Data availability depends on Yahoo Finance; some tickers may have
  shorter history than 10 years.
