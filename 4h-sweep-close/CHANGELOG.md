# Changelog

All notable changes to this indicator are documented here. The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and versions follow [Semantic Versioning](https://semver.org/) and match `SCRIPT_VERSION` in `mod.pine`.

## [1.1.1] - 2026-10-28

### Fixed

- 4H and 1H sweep lines on lower charts now start at the lower-timeframe candle that made the swept high/low, instead of at the swept candle's open.

### Added

- `SCRIPT_VERSION` constant.

## [1.1.0] - 2026-10-08

### Added

- 4H sweeps shown on the 30m, 15m, 5m, 4m and 3m charts.
- 1H sweeps shown on the 30m, 15m, 5m, 4m and 3m charts.
- Alerts for 1H sweeps on lower charts.

### Changed

- Replaced the "Show on 1 hour", "Show on 4 hour" and "Show 4H sweeps on the 1 hour chart" inputs with "Show 4H sweeps" and "Show 1H sweeps".

## [1.0.0] - 2026-10-08

### Added

- Bearish and bullish sweep/close setups on the 1H and 4H charts.
- 4H sweeps shown on the 1H chart.
- Close modes: beyond prior close, inside prior body, beyond prior open.
- Minimum sweep (ticks) and minimum prior body (%) filters.
- Lines, labels and optional candle highlights, with configurable colors and label text.
- Alerts for sweeps on the chart timeframe and 4H sweeps on the 1H chart.
