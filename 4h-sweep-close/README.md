# 4H Sweep/Close

See [CHANGELOG.md](CHANGELOG.md) for the version history.

## Overview

This indicator marks 4H and 1H candles that sweep the prior candle's high or low and then close back beyond the prior candle's close. Spotting these by hand means flipping between the 4H, 1H and lower timeframes. This indicator marks them automatically on the 4H and 1H charts and projects them onto the 30m, 15m, 5m, 4m and 3m charts.

## Concepts

- **Bearish sweep (4HS- / 1HS-):** a bullish candle followed by a bearish candle that trades above the bullish candle's high and closes below its close.
- **Bullish sweep (4HS+ / 1HS+):** a bearish candle followed by a bullish candle that trades below the bearish candle's low and closes above its close.
- The line is drawn at the swept high/low (the prior candle's high or low). On lower timeframes, the line starts at the lower-timeframe candle that made that high/low.
- Higher-timeframe sweeps are only drawn after the sweeping candle has closed, so marks don't repaint.

## How to Use

1. Copy `mod.pine` into TradingView's Pine Editor, save it, and add it to a chart.
2. Open the chart on a supported timeframe:

   | Chart | 4H sweeps | 1H sweeps |
   | --- | --- | --- |
   | 4H | Yes | No |
   | 1H | Yes | Yes |
   | 30m, 15m, 5m, 4m, 3m | Yes | Yes |

3. Use **Show setups** to show bearish sweeps, bullish sweeps or both.
4. Use **Sweep candle must close** to choose how far back the sweeping candle has to close: beyond the prior close, inside the prior body, or beyond the prior open.
5. Use **Min sweep beyond prior high/low (ticks)** and **Min prior candle body (%)** to filter out small sweeps and doji-like candles.

After updating `mod.pine`, save it again in the Pine Editor so the chart picks up the new version.

## Features

- 4H and 1H sweeps on the 4H, 1H, 30m, 15m, 5m, 4m and 3m charts
- Lines at the swept high/low with text labels (4HS-, 4HS+, 1HS-, 1HS+)
- Optional highlight of the prior and sweeping candles
- Configurable colors and label text for each timeframe and direction
- Alerts for sweeps on the chart timeframe and for 4H/1H sweeps on lower charts
