# Boundary and Command Contract

## Branch ownership

`live/v1-runtime-hardening` owns live runtime safety. `research/v3-experimental-engine` owns experimental research.

## Live import rules

- Future `src/tradingbotsuite/live/**` modules must not import research experiment modules.
- The only allowed bridge is a promotion artifact validator under `src/tradingbotsuite/promotion/**`.
- Live execution adapters must not import strategy research modules.
- Operator UI routes must call live-owned safety services for live commands.

## Command ownership

Live commands:

- `serve`
- `manual`
- `smoke-live`

Research commands still present on this branch are preserved only until Stage 10 can reject live-mode use:

- `build-dataset`
- `import-tv-chart-export`
- `train-model`
- `calibrate-model`
- `replay-eval`
- `research-entry-gates`
- `optimize-entry-gates`
- `preflight-entry-gates`

## Legacy status

TradingView, Pine, and parity material is legacy/reference material on this branch. It must not be expanded as part of live hardening and must not drive live runtime safety decisions.
