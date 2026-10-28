# HTF Separators

## Overview

This indicator draws vertical lines that mark where higher-timeframe candles start, so you can see the higher-timeframe structure while on a lower timeframe. It marks each new day on every intraday chart, and adds hourly, 4-hour or 15-minute separators depending on the chart's timeframe.

## Concepts

- **Daily separators:** a solid line at the start of each trading session, with the day of the week (MON, TUE, …) printed at the bottom of the chart.
- **Higher-timeframe separators** depend on the chart's timeframe:

  | Chart | Separators |
  | --- | --- |
  | 1m | 4H candles (solid) and 15m candles (dotted) |
  | 5m | 1H candles (dotted) |
  | 15m | 4H candles (dotted) |

- 4H separators follow the 4H candles that open at 02:00, 06:00, 10:00, 14:00, 18:00 and 22:00 UTC.

## How to Use

1. Copy `mod.pine` into TradingView's Pine Editor, save it, and add it to an intraday chart.
2. Set **Show Daily Separators** to:
   - **Lines and Labels:** daily lines with day-of-week labels
   - **Lines:** daily lines only
   - **None:** no daily lines
3. Switch between the 1m, 5m and 15m charts to see the matching higher-timeframe separators.

## Features

- Daily separators with day-of-week labels on all intraday charts
- 1H separators on the 5m chart
- 4H separators on the 15m and 1m charts
- 15m separators on the 1m chart
