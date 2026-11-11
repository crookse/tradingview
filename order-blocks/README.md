# Order Blocks

See [CHANGELOG.md](CHANGELOG.md) for the version history.

## Overview

This indicator marks order blocks that form around the previous day's high (PDH) and low (PDL) when a 1h candle closes through them. Each order block is drawn as a line that extends right until price returns to it, so the end of the line shows the retest. Each line is tagged on its right end: **1h OB+** for bullish, **1h OB-** for bearish. Detection always uses 1h candles, and the lines can be shown on the 1h chart or on a lower timeframe such as 5m.

## Concepts

- **PDH / PDL:** Previous Day High and Previous Day Low. Days follow the symbol's trading session, the same as Super Crooks - Daily Highs/Lows.
- **Bullish order block:** a 1h candle closes above the PDH or PDL after the previous candle closed at or below it. The last down-close candle before that close is the order block, as long as it sits around the broken level. The line is drawn at the lowest low of the candles after the order block candle, up to and including the candle that closed above the level, and starts at that candle.
- **Bearish order block:** a 1h candle closes below the PDH or PDL after the previous candle closed at or above it. The last up-close candle before that close is the order block, as long as it sits around the broken level. The line is drawn at that candle's high.
- **Around the level:** the order block candle's range (low to high) reaches within **PDH/PDL Proximity** × the 1h ATR(14) of the level. At 0, the candle has to touch the level.
- Each level gives at most one bullish and one bearish order block per day.
- **Engulfing continuation (bullish):** once a 1h OB+ is respected (retested and held, see below), every bullish engulfing candle after it also marks a 1h OB+. A bullish engulfing candle is an up-close candle that closes above the high of the last down-close candle, within **Engulfing Within** candles of it. The line is drawn at the lowest low after the down-close candle, up to and including the engulfing candle. This keeps going until a 1h candle closes below the respected line; a newly respected OB+ takes over as the line to hold.
- **Engulfing continuation (bearish):** the mirror. After a 1h OB- is respected, a down-close candle that closes below the low of the last up-close candle marks a 1h OB-, with the line at the highest high after the up-close candle. It stops when a 1h candle closes above the respected line.
- **Lifecycle (bullish; bearish is mirrored):**
  1. **Valid:** the line extends while price stays above it.
  2. **Retest:** the first candle that trades down to the level and closes at or above it ends the line.
  3. **Broken:** a candle that closes below the level does not delete it. The line keeps extending.
  4. **Reclaimed:** once a candle closes back above a broken level, the next candle that trades down to it and closes at or above it is the retest.

## How to Use

1. Copy `mod.pine` into TradingView's Pine Editor, save it, and add it to a 1h chart or a lower timeframe that divides an hour evenly (e.g. 1m, 5m, 15m). On a lower timeframe, the 1h candles are built from the chart's bars, so the same 1h order blocks are drawn and their lines extend with every bar. Above 1h it draws nothing and shows a notice.
2. Use **Show Setups** to show bullish order blocks, bearish order blocks, both or neither.
3. Raise **PDH/PDL Proximity** to accept order block candles further from the level, or lower it to be stricter.
4. Turn **Show Engulfing Order Blocks** off to only mark PDH/PDL breaks, and use **Engulfing Within** to set how many candles the engulfing close can come after the candle it engulfs.
5. Use **Order Block History** to set how many lines of each type stay on the chart.

## Features

- Bullish (green) and bearish (red) order blocks at PDH/PDL breaks, drawn after the 1h candle closes (no repainting), on 1h or lower timeframes
- Engulfing continuation order blocks after a respected 1h OB+ / OB-
- Lines survive a break and end on the first retest after a reclaim
- "1h OB+" / "1h OB-" text on the right end of each line
- Configurable proximity, history, colors and line width
