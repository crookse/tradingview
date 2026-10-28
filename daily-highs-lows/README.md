# Daily Highs/Lows

See [CHANGELOG.md](CHANGELOG.md) for the version history.

## Overview

This indicator draws the high and low of previous days. Marking these levels by hand every day is tedious. This indicator draws them automatically and keeps them updated, on the daily chart and every lower timeframe.

## Concepts

- **PDH / PDL:** Previous Day High and Previous Day Low (yesterday's session).
- **PDH*n* / PDL*n*:** older days, where *n* counts back from yesterday. PDH1/PDL1 is the day before yesterday, PDH2/PDL2 the day before that, and so on.
- The current day's high and low are tracked as the day trades, then become PDH/PDL when the next session starts.
- Days follow the symbol's trading session, so a "day" starts at the session open rather than at midnight.

## How to Use

1. Copy `mod.pine` into TradingView's Pine Editor, save it, and add it to a chart on the daily timeframe or lower.
2. Set **Number of Days to Show** (1–20) to choose how many previous days are drawn.
3. Adjust **Line Width** and **Line Style** (solid, dashed or dotted).
4. Turn on **Show High Price** / **Show Low Price** to add the price to each label.
5. Turn on **Show Dates** to label each level with its date (e.g. PDH 10/27) instead of a number.

## Features

- PDH/PDL and older daily levels drawn as lines with labels
- Lines extend to the current bar and update in real time
- Configurable number of days, line width and line style
- Optional prices and dates in the labels
