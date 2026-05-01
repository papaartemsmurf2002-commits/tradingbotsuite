# Branch Purpose: live/v1-runtime-hardening

This branch is the live runtime hardening branch for TradingBotSuite.

## Source

- Created from: `main`
- Created for: Stage 0 governance and later Stage 10 live hardening work.

## Purpose

This branch preserves and hardens the live BTC runtime, operator console, Binance market-data reliability, Hyperliquid execution path, persistence, reconciliation, and testnet validation stack.

## Boundaries

- Live code must fail closed on unsafe configuration.
- Live code must reject research jobs in live mode.
- Live code must reject `research_only` or `observe_only` artifacts as live order inputs.
- Live code must not import experimental research modules except through an approved promotion artifact validator.
- Research output is not a live signal on this branch.

## Next eligible work

Stage 1 repo cartography must run before live hardening implementation begins. After Stage 1 completes, Stage 10 can proceed partly in parallel with the research branch, subject to the orchestrator ledger.
