# Work Packet: WP1-02-tradingview-archive-map

Stage: Stage 1 - Repo cartography
Owner agent: Documentation Agent
Reviewer agent: Orchestrator Agent
Branch: `live/v1-runtime-hardening`
Allowed paths:

- `docs/repo_cartography/TRADINGVIEW_ARCHIVE_MAP.md`
- `docs/KNOWN_ISSUES.md`
- `docs/ORCHESTRATOR_STAGE_LEDGER.md`
- `docs/stage_reports/STAGE_1_EXIT_REPORT.md`

Forbidden paths:

- `src/**`
- `tests/**`
- `configs/**`
- generated data, secrets, databases, logs, caches, and local artifacts

## Objective

Classify TradingView, Pine, marker-parity, and chart-export material for later archive or legacy marking.

## Required source files to read first

- `README.md`
- `docs/PARITY_WORKFLOW.md`
- `docs/UI_VALIDATION.md`
- `src/tradingbot/cli.py`
- `src/tradingbot/parity.py`
- `src/tradingbotsuite/research/tradingview_import.py`

## Implementation tasks

- Identify TradingView/Pine/parity files.
- Identify active command surfaces that still expose parity workflows.
- Identify tests and fixtures that preserve parity behavior.
- Define Stage 2 archive/legacy recommendations.

## Tests and validation commands

```powershell
git grep -n "TradingView\|Pine\|parity\|tv_\|lorentz_tv\|features_tv\|kernels_tv\|lc_marker" live/v1-runtime-hardening -- .
$env:PYTHONPATH='src'; python -m pytest tests/test_tv_parity.py tests/tradingbotsuite/test_tradingview_import.py -q
```

## Acceptance evidence

- `docs/repo_cartography/TRADINGVIEW_ARCHIVE_MAP.md`
- `docs/stage_reports/STAGE_1_EXIT_REPORT.md`

## Handoff notes

No files are moved during Stage 1. Stage 2 should document legacy status before any archive move is attempted.
