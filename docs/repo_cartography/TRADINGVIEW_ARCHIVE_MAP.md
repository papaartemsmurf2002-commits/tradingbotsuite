# TradingView Archive Map: live/v1-runtime-hardening

Date: 2026-05-01
Stage: Stage 1 - Repo cartography

## Summary

The live branch still contains the full TradingView/Pine/parity reference surface. Stage 1 does not move these files. It classifies them so Stage 2 can document legacy status and a later scoped archive move can occur safely.

## Active command surfaces to archive or freeze

| Path | Commands or role | Recommendation |
| --- | --- | --- |
| `src/tradingbot/cli.py` | `parity-check`, `merge-tv-exports`, `entry-parity`, `parity-dump`, `advanced-ta-compare`, `marker-research`, `serve-ui` | Freeze as legacy/reference; do not expand in live hardening. |
| `src/tradingbotsuite/main.py` | `import-tv-chart-export`, `research-entry-gates`, `optimize-entry-gates`, `preflight-entry-gates` | Keep only as preserved research until Stage 10 rejects live-mode use. |
| `src/tradingbotsuite/web/templates/research.html` | Operator-visible research controls | Must be guarded or hidden in live mode during Stage 10. |

## Pine and parity docs

| Path | Classification |
| --- | --- |
| `docs/PARITY_WORKFLOW.md` | Legacy parity workflow. |
| `docs/UI_VALIDATION.md` | Legacy local marker-validation UI docs. |
| `docs/lc_diagnostic_export_usage.md` | Legacy diagnostic export usage. |
| `docs/lc_lorentzian_diagnostic_ann_export.pine` | Pine diagnostic export script. |
| `docs/lc_lorentzian_diagnostic_core_export.pine` | Pine diagnostic export script. |
| `docs/lc_lorentzian_diagnostic_export.pine` | Pine diagnostic export script. |
| `docs/lc_parity_export_template.pine` | Pine export helper. |

## Code candidates for later archive or legacy package split

| Path | Classification |
| --- | --- |
| `src/tradingbot/features_tv.py` | Pine-compatible feature helpers. |
| `src/tradingbot/kernels_tv.py` | Pine-compatible kernel helpers. |
| `src/tradingbot/lorentz_tv.py` | TradingView LC classifier. |
| `src/tradingbot/parity.py` | TradingView export normalization/comparison. |
| `src/tradingbot/tv_backtest.py` | TradingView-style stats. |
| `src/tradingbot/lc_marker_research.py` | Marker-only research probes. |
| `src/tradingbot/ui.py` | Local marker validation UI. |
| `src/tradingbotsuite/research/tradingview_import.py` | TradingView chart-export importer. |
| `src/tradingbotsuite/research/entry_gate.py` | Chart-export entry-gate research. |

## References, examples, and fixtures

| Path | Classification |
| --- | --- |
| `references/lorentzian-classification/original_lorentzian_classification.pine` | Source reference. |
| `references/pine-libraries/*.txt` | Source library references. |
| `examples/btc_lc_*.yaml`, `examples/btc_tv_off_parity.yaml` | Legacy LC/parity examples. |
| `tests/fixtures/tv_lc/**` | Parity fixtures. |
| `tests/test_tv_parity.py` | Parity regression tests. |
| `tests/tradingbotsuite/test_tradingview_import.py` | Chart-export import regression tests. |

## Archive recommendation

Stage 2 documentation should state:

- TradingView/Pine/parity materials are legacy/reference on the live branch.
- They must not be expanded as part of live runtime hardening.
- Any later archive move should be its own work packet because it will affect tests, examples, docs, and CLI commands.
- Live runtime must not depend on TradingView parity workflows for safety decisions.

## Do not promote

- Marker-only parity results as strategy evidence.
- TradingView chart exports as canonical normalized market data.
- Pine scripts as runtime dependencies.
- Parity commands as active live branch operator workflows.
