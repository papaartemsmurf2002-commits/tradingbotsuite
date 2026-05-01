# Work Packet: WP0-01-branch-and-ledger-setup

Stage: Stage 0 - Governance and branches
Owner agent: Orchestrator Agent
Reviewer agent: QA Agent
Branch: `live/v1-runtime-hardening`
Allowed paths:

- `docs/ORCHESTRATOR_STAGE_LEDGER.md`
- `docs/KNOWN_ISSUES.md`
- `docs/BRANCH_PURPOSE.md`
- `docs/work_packets/WP0-01-branch-and-ledger-setup.md`
- `docs/stage_reports/STAGE_0_EXIT_REPORT.md`

Forbidden paths:

- `src/**`
- `tests/**`
- `configs/**`
- generated data, secrets, databases, logs, caches, and local artifacts

## Objective

Create the live branch governance baseline required before any implementation work.

## Required source files to read first

- `C:/Users/papaa/Downloads/AGENTIC_DEVELOPMENT_PLAN_TRADINGBOTSUITE.md`
- `README.md`
- existing `docs/tradingbotsuite_runtime/**` references as needed for later stages

## Implementation tasks

- Create `live/v1-runtime-hardening` from `main`.
- Create the orchestrator stage ledger.
- Create the known issues registry.
- Add branch-purpose documentation.
- Write the Stage 0 exit report.

## Tests and validation commands

```powershell
git branch --list live/v1-runtime-hardening --verbose --no-abbrev
python -m compileall -q src/tradingbotsuite
$env:PYTHONPATH='src'; python -m pytest tests/tradingbotsuite/test_config.py -q
```

## Acceptance evidence

- Branch exists locally and remotely.
- Governance documents exist on the branch.
- No open P0 or P1 issues are recorded.
- Validation command results are recorded in `docs/stage_reports/STAGE_0_EXIT_REPORT.md`.

## Handoff notes

Stage 1 should inventory root launchers, live order paths, research commands, and import boundaries before Stage 10 edits begin.
