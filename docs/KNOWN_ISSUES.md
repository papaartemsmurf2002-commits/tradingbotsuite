# Known Issues

Last updated: 2026-05-01

This registry is the blocking issue source for orchestrator stage gates.

Severity levels:

- P0: safety, data leakage, live trading risk, corrupt data, branch boundary violation.
- P1: invalid backtest assumption, non-deterministic experiment, broken artifact contract, severe performance blocker.
- P2: incomplete docs, minor missing tests, non-blocking refactor debt.
- P3: polish and convenience.

Stage advancement stop rule:

- Any open P0 blocks stage advancement.
- Four or more unresolved P1 issues block stage advancement.
- P2/P3 can carry forward only with explicit orchestrator note and owner.

## Current summary

| Severity | Open | In progress | Resolved | Accepted debt |
| --- | ---: | ---: | ---: | ---: |
| P0 | 0 | 0 | 0 | 0 |
| P1 | 2 | 0 | 0 | 0 |
| P2 | 1 | 0 | 0 | 0 |
| P3 | 0 | 0 | 0 | 0 |

## ISSUE-L1-001: Live runtime imports research scorer and config

Severity: P1
Stage discovered: Stage 1 - Repo cartography
Owner: Live Safety Agent
Status: open
Paths affected: `src/tradingbotsuite/core/engine.py`, `src/tradingbotsuite/runtime.py`, `src/tradingbotsuite/research/inference.py`, `src/tradingbotsuite/research/config.py`

### Problem

The live branch runtime can load research acceptance scoring through direct imports. This needs hard preflight and artifact validation before any live mode can treat research output as an input.

### Evidence

Stage 1 cartography found `src/tradingbotsuite/core/engine.py` importing `tradingbotsuite.research.config` and `tradingbotsuite.research.inference`, and `src/tradingbotsuite/runtime.py` loading `AcceptanceScorer` when an artifact manifest path exists.

### Required resolution

Stage 10 must reject `research_only` and `observe_only` artifacts as live inputs and fail closed on unsafe promotion state. Stage 11 must replace direct live influence with a promotion/shadow-only bridge.

### Resolution notes

Open as of 2026-05-01.

## ISSUE-L1-002: Operator UI exposes research jobs beside live controls

Severity: P1
Stage discovered: Stage 1 - Repo cartography
Owner: Live Safety Agent / Operator UI Agent
Status: open
Paths affected: `src/tradingbotsuite/operator_console.py`, `src/tradingbotsuite/web/operator.py`, `src/tradingbotsuite/web/templates/research.html`, `src/tradingbotsuite/main.py`

### Problem

The operator UI and CLI expose research jobs on the live branch. Existing guardrails are not a complete live-mode ban for research jobs.

### Evidence

Stage 1 cartography found research CLI commands and operator routes for `build-dataset`, `train-model`, `calibrate-model`, `replay-eval`, and `research-entry-gates`.

### Required resolution

Stage 10 must reject research jobs in live mode and ensure operator UI routes cannot bypass engine safety.

### Resolution notes

Open as of 2026-05-01.

## ISSUE-L1-003: TradingView parity material remains active in live branch

Severity: P2
Stage discovered: Stage 1 - Repo cartography
Owner: Documentation Agent
Status: open
Paths affected: `src/tradingbot/*`, `docs/lc_*.pine`, `docs/PARITY_WORKFLOW.md`, `docs/UI_VALIDATION.md`, `references/**`, `examples/btc_lc_*.yaml`, `tests/fixtures/tv_lc/**`

### Problem

TradingView/Pine/parity material remains in active source and command paths on the live branch. It is valuable historical/reference material, but it is not the active live hardening path.

### Evidence

Stage 1 cartography found parity commands in `src/tradingbot/cli.py`, Pine export docs under `docs/`, source references under `references/`, and parity fixtures under `tests/fixtures/tv_lc/`.

### Required resolution

Stage 2 documentation should mark these as legacy/reference. Later cleanup may move them under `legacy/tradingview_parity_archive/` after tests and owners are explicitly assigned.

### Resolution notes

Open as of 2026-05-01.

## Issue template

```markdown
## ISSUE-ID: Short title

Severity: P0/P1/P2/P3
Stage discovered:
Owner:
Status: open | in_progress | resolved | accepted_debt
Paths affected:

### Problem

### Evidence

### Required resolution

### Resolution notes
```
