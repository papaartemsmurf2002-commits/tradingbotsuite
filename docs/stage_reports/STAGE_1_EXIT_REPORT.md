# Stage 1 Exit Report

Stage: Stage 1 - Repo cartography
Branch: `live/v1-runtime-hardening`
Decision: complete
Date: 2026-05-01
Orchestrator: Codex

## Completed work packets

- WP1-01-repo-inventory
- WP1-02-tradingview-archive-map

## Validation commands run

```powershell
git ls-tree -r --name-only live/v1-runtime-hardening
git grep -n "subparsers.add_parser" live/v1-runtime-hardening -- src/tradingbotsuite/main.py src/tradingbot/cli.py
git grep -n "from tradingbotsuite.research\|import tradingbotsuite.research" live/v1-runtime-hardening -- src/tradingbotsuite
git grep -n "TradingView\|Pine\|parity\|tv_\|lorentz_tv\|features_tv\|kernels_tv\|lc_marker" live/v1-runtime-hardening -- .
python -m compileall -q src/tradingbotsuite
$env:PYTHONPATH='src'; python -m pytest tests/tradingbotsuite/test_config.py tests/tradingbotsuite/test_operator_ui.py -q
```

## Results

- File inventory: 135 tracked files; 67 under `src/**`; 19 under `tests/**`; 31 under `docs/**`.
- Live runtime paths, order/execution flow, operator UI, research modules, TradingView/parity material, and tests were mapped.
- `python -m compileall -q src/tradingbotsuite`: passed.
- `$env:PYTHONPATH='src'; python -m pytest tests/tradingbotsuite/test_config.py tests/tradingbotsuite/test_operator_ui.py -q`: passed, 24 tests.

## Artifacts produced

- `docs/repo_cartography/REPO_INVENTORY.md`
- `docs/repo_cartography/TRADINGVIEW_ARCHIVE_MAP.md`
- `docs/work_packets/WP1-01-repo-inventory.md`
- `docs/work_packets/WP1-02-tradingview-archive-map.md`
- `docs/stage_reports/STAGE_1_EXIT_REPORT.md`

## Known issues

- ISSUE-L1-001: Live runtime imports research scorer and config.
- ISSUE-L1-002: Operator UI exposes research jobs beside live controls.
- ISSUE-L1-003: TradingView parity material remains active in live branch.

## Carry-forward debt

- Stage 2 must document live/research command ownership and artifact contracts.
- Stage 10 must enforce fail-closed live preflight and reject live-mode research jobs.
- A later scoped archive packet should move or freeze TradingView parity material after contracts are documented.

## Decision rationale

Stage 1 is complete because cartography is documented and no P0 issue is open. The two P1 risks are below the stop-rule threshold and are assigned to later live-hardening work.
