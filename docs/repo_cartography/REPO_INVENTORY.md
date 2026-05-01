# Repo Inventory: live/v1-runtime-hardening

Date: 2026-05-01
Stage: Stage 1 - Repo cartography

## Summary

`live/v1-runtime-hardening` preserves the live BTC runtime, operator console, Binance market data, Hyperliquid execution, persistence, and test coverage. It also still carries research modules and TradingView/parity material that must be gated or archived before live hardening can be considered complete.

Tracked file counts at Stage 1:

| Area | Count |
| --- | ---: |
| All tracked files | 135 |
| `src/**` | 67 |
| `tests/**` | 19 |
| `docs/**` | 31 |

## Package families

| Path | Classification | Notes |
| --- | --- | --- |
| `src/tradingbotsuite/` | Live/runtime package | Engine, market data, Hyperliquid execution, persistence, web app, operator UI, and preserved research modules. |
| `src/tradingbotsuite/adapters/` | Market data and execution adapters | Binance market data and Hyperliquid execution path. |
| `src/tradingbotsuite/core/` | Live runtime core | Signal handling, supervision, reconciliation, models, math, acceptance, security. |
| `src/tradingbotsuite/persistence/` | Runtime persistence | SQLite store for runtime state, jobs, positions, events, metrics. |
| `src/tradingbotsuite/web/` | FastAPI and operator UI | Webhook ingress, operator UI routes, templates. |
| `src/tradingbotsuite/research/` | Preserved research package | Dataset, model training, replay, entry-gate research, TradingView import. Must not run in live mode after Stage 10. |
| `src/tradingbot/` | LC/parity and legacy bot package | TradingView-compatible LC, parity tools, backtester, optimizer, local UI, legacy live shell. |
| `docs/tradingbotsuite_runtime/` | Runtime docs | Operator, reliability, testnet, preservation, and V2 research docs. |
| `tests/tradingbotsuite/` | Runtime and preserved research tests | Engine, config, operator UI, entry gates, TradingView import, research. |

## Entrypoints and launchers

| Path | Entrypoint | Classification |
| --- | --- | --- |
| `pyproject.toml` | `tradingbot = tradingbot.cli:main` | Legacy package console script. |
| `src/tradingbot/__main__.py` | `python -m tradingbot` | Legacy package launcher. |
| `src/tradingbotsuite/main.py` | `python -m tradingbotsuite.main ...` | Mixed live and research CLI; also creates FastAPI `app`. |
| `src/tradingbotsuite/main.py serve` | Runs `uvicorn.run("tradingbotsuite.main:app", ...)` | Live/operator server path. |

No root `run_*.py` launchers are tracked on this branch.

## Live runtime paths

| Path | Role |
| --- | --- |
| `src/tradingbotsuite/web/app.py` | FastAPI app, `/health`, `/health/details`, `/webhooks/tradingview`, background monitor loop. |
| `src/tradingbotsuite/runtime.py` | Builds `TradingEngine` with SQLite store, Binance client, execution adapter, optional research scorer. |
| `src/tradingbotsuite/core/engine.py` | Live decision pipeline, safety state, health checks, reconciliation, supervision, signal handling. |
| `src/tradingbotsuite/adapters/binance.py` | Binance candles, streams, microstructure, depth-health handling. |
| `src/tradingbotsuite/adapters/execution.py` | Shadow, paper, and Hyperliquid execution adapters; intent builders. |
| `src/tradingbotsuite/persistence/sqlite_store.py` | Runtime state, events, feed, jobs, positions, metrics. |
| `src/tradingbotsuite/config.py` | Environment config, runtime mode, Hyperliquid testnet credential fallback. |

## Order and execution flow

| Step | Path |
| --- | --- |
| Webhook ingress | `src/tradingbotsuite/web/app.py` `/webhooks/tradingview` |
| Payload adaptation | `src/tradingbotsuite/core/models.py` and engine signal handling |
| Decision and supervision | `src/tradingbotsuite/core/engine.py` |
| Intent construction | `src/tradingbotsuite/adapters/execution.py` `build_open_intents`, `build_close_intents`, `build_protective_intents` |
| Adapter execution | `ShadowExecutionAdapter`, `PaperExecutionAdapter`, `HyperliquidExecutionAdapter` |
| Operator command wrappers | `src/tradingbotsuite/operator_commands.py` |
| Persistence/reconciliation | `src/tradingbotsuite/persistence/sqlite_store.py`, `src/tradingbotsuite/core/engine.py` |

## Operator UI paths

| Path | Role |
| --- | --- |
| `src/tradingbotsuite/web/operator.py` | Operator routes and APIs. |
| `src/tradingbotsuite/operator_console.py` | Operator service and job queue. |
| `src/tradingbotsuite/web/templates/*.html` | Overview, control, timeline, research, analysis, predictions, guides, login. |
| `tests/tradingbotsuite/test_operator_ui.py` | UI route, auth, command, and research-job tests. |

## Research still present on live branch

| Surface | Paths |
| --- | --- |
| CLI commands | `build-dataset`, `import-tv-chart-export`, `train-model`, `calibrate-model`, `replay-eval`, `research-entry-gates`, `optimize-entry-gates`, `preflight-entry-gates` in `src/tradingbotsuite/main.py`. |
| Research modules | `src/tradingbotsuite/research/config.py`, `dataset.py`, `entry_gate.py`, `evaluation.py`, `inference.py`, `modeling.py`, `tradingview_import.py`, `workflow.py`. |
| Operator research jobs | `src/tradingbotsuite/operator_console.py`, `src/tradingbotsuite/web/operator.py`, `src/tradingbotsuite/web/templates/research.html`. |
| Configs | `configs/v2_btc_research.json`, `configs/tradingbotsuite/v2_btc_research.json`. |
| Tests | `tests/tradingbotsuite/test_research.py`, `test_entry_gate.py`, `test_tradingview_import.py`. |

## Import and boundary map

| Importing path | Imported research path | Risk |
| --- | --- | --- |
| `src/tradingbotsuite/core/engine.py` | `tradingbotsuite.research.config`, `tradingbotsuite.research.inference` | Live runtime can use research plan/scorer. |
| `src/tradingbotsuite/runtime.py` | `tradingbotsuite.research.inference` | Runtime loads scorer when artifact manifest is configured. |
| `src/tradingbotsuite/main.py` | `tradingbotsuite.research.*` | Research modules imported at top level in live CLI module. |
| `src/tradingbotsuite/operator_console.py` | `tradingbotsuite.research.*` | Operator service can queue research jobs. |
| `src/tradingbotsuite/web/operator.py` | `tradingbotsuite.research.entry_gate` | Operator UI exposes research controls. |

## Test coverage map

| Area | Tests |
| --- | --- |
| Live engine and execution | `tests/tradingbotsuite/test_engine.py` |
| Binance and microstructure | `tests/tradingbotsuite/test_binance.py`, `test_microstructure_prediction.py` |
| Config and math | `tests/tradingbotsuite/test_config.py`, `test_math.py` |
| Operator UI | `tests/tradingbotsuite/test_operator_ui.py` |
| Preserved research | `tests/tradingbotsuite/test_research.py`, `test_entry_gate.py`, `test_tradingview_import.py` |
| LC/parity/backtest/UI | `tests/test_tv_parity.py`, `test_strategy_flow.py`, `test_data_manager.py`, `test_indicators.py`, `test_ui_diagnostics.py` |

## Stage 1 conclusions

- This branch is suitable as the live hardening base.
- Stage 10 must harden preflight, reject unsafe live config, reject research jobs in live mode, and reject research-only artifacts as live inputs.
- Stage 2 should document live/research command ownership before implementation changes start.
- TradingView/Pine/parity material should be marked legacy/reference before any archive move.
