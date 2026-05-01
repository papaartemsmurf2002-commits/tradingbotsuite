# Backtest Contract

Backtests are research evidence, not live authorization.

## Required research outputs

- `backtest_manifest.json`
- `trades.parquet`
- `signals.parquet`
- `equity_curve.parquet`
- `metrics.json`
- `config_resolved.json`
- optional `debug_trace.parquet`

## Live interpretation rules

- Backtest metrics must include fees, slippage, and funding before they can be reviewed for promotion.
- Live branch must not treat a backtest manifest as a live signal input.
- Backtest results can enter live only through the promotion candidate process and only for shadow diagnostics first.
