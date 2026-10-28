# Breakers

## Overview

This indicator marks bullish and bearish breaker formations. Breakers are easy to miss when price moves quickly or when you're watching several timeframes. This indicator finds the swing points, labels them and draws a box over the breaker block, on whatever timeframe the chart is on.

## Concepts

- **Bullish breaker (BRKR +):** a swing low (L), a swing high (H), a lower low (LL), then a higher high (HH): an up-close candle that closes above the open of the first down-close candle after the H. The box covers the up-close candles between the L and the H.
- **Bearish breaker (BRKR -):** a swing high (H), a swing low (L), a higher high (HH), then a lower low (LL): a down-close candle that closes below the open of the first up-close candle after the L. The box covers the down-close candles between the H and the L.
- Swing points are pivots: a candle whose high (or low) is beyond the candles on either side of it, up to the swing length.
- A formation is only drawn when the box has at least one qualifying candle. Formations with no up-close (bullish) or down-close (bearish) candles in that range are skipped.

## How to Use

1. Copy `mod.pine` into TradingView's Pine Editor, save it, and add it to a chart. It works on any timeframe.
2. Use **Show Setups** to show bullish breakers, bearish breakers, both or neither.
3. Set **Swing Length** for each side. Higher values use larger swings and mark fewer formations.
4. Set **Breaker Confirmation Type** for each side:
   - **Candle Close:** the LL/HH is compared using candle bodies (opens and closes).
   - **Candle Wick:** the LL/HH is compared using wicks (highs and lows).
5. Use **Breaker History** to set how many formations of each type stay on the chart.

## Features

- Bullish and bearish breakers drawn after candle close (no repainting)
- L, H, LL and HH labels on each formation, plus a BRKR +/- box over the breaker block
- Separate swing length, confirmation type and box color for bullish and bearish setups
- Configurable history, with older formations removed automatically
