# Session Highs/Lows

## Overview

This indicator marks the high and low of each trading session (Asia, London, New York AM and New York PM) and shows when price trades through them. Session highs and lows are common reference levels, and tracking which ones are still untouched is tedious by hand. This indicator draws them automatically and marks each one once price trades beyond it.

## Concepts

- Sessions use New York time:

  | Session | Time (New York) | Labels |
  | --- | --- | --- |
  | Asia | 20:00–00:00 | AS.H / AS.L |
  | London | 02:00–05:00 | LO.H / LO.L |
  | New York AM | 08:30–11:30 | NYA.H / NYA.L |
  | New York PM | 13:00–16:00 | NYP.H / NYP.L |

- While a session is trading, its line moves to each new high or low.
- A level that price hasn't traded beyond yet is labeled **(OPEN)**.
- Once price trades beyond a level, the line is cut off at that candle and **(OPEN)** is removed from the label.

## How to Use

1. Copy `mod.pine` into TradingView's Pine Editor, save it, and add it to an intraday chart (5m, 15m or 1H work well).
2. Set **Show Session Liquidity Sweeps** to show highs, lows, both or neither.
3. Set **Session Liquidity Labels** to **Name** (e.g. LO.H) or **Name and Date** (e.g. LO.H 10/27).
4. Use **Session Liquidity History (Highs)** and **(Lows)** to set how many levels stay on the chart.

## Features

- Highs and lows for the Asia, London, New York AM and New York PM sessions
- Levels update in real time while each session trades
- (OPEN) labels on levels price hasn't traded beyond yet
- Lines end where price trades through them
- Configurable labels and history
