# Work Packet: WP1-01-repo-inventory

Stage: Stage 1 - Repo cartography
Owner agent: Repo Cartographer Agent
Reviewer agent: Orchestrator Agent
Branch: `live/v1-runtime-hardening`
Allowed paths:

- `docs/repo_cartography/REPO_INVENTORY.md`
- `docs/KNOWN_ISSUES.md`
- `docs/ORCHESTRATOR_STAGE_LEDGER.md`
- `docs/stage_reports/STAGE_1_EXIT_REPORT.md`

Forbidden paths:

- `src/**`
- `tests/**`
- `configs/**`
- generated data, secrets, databases, logs, caches, and local artifacts

## Objective

Map the live branch without changing behavior.

## Required source files to read first

- `C:/Users/papaa/Downloads/AGENTIC_DEVELOPMENT_PLAN_TRADINGBOTSUITE.md`
- `README.md`
- `src/tradingbotsuite/main.py`
- `src/tradingbotsuite/runtime.py`
- `src/tradingbotsuite/core/engine.py`
- `src/tradingbotsuite/adapters/execution.py`
- `src/tradingbotsuite/web/operator.py`

## Implementation tasks

- Record package and file-family inventory.
- Record import and boundary risks.
- List root launchers and CLI entrypoints.
- List live runtime, order, execution, persistence, and operator UI paths.
- List research commands/modules still present.
- List tests that cover current runtime and research-preservation areas.

## Tests and validation commands

```powershell
git grep -n "subparsers.add_parser" live/v1-runtime-hardening -- src/tradingbotsuite/main.py src/tradingbot/cli.py
git grep -n "from tradingbotsuite.research\|import tradingbotsuite.research" live/v1-runtime-hardening -- src/tradingbotsuite
$env:PYTHONPATH='src'; python -m pytest tests/tradingbotsuite/test_config.py tests/tradingbotsuite/test_operator_ui.py -q
```

## Acceptance evidence

- `docs/repo_cartography/REPO_INVENTORY.md`
- `docs/stage_reports/STAGE_1_EXIT_REPORT.md`

## Handoff notes

Stage 10 must address live-mode rejection of research jobs and research-only artifacts.
