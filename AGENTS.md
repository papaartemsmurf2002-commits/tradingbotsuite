# Agent Guide

This branch is controlled by the orchestrator stage ledger.

## Branch role

`live/v1-runtime-hardening` is the live runtime hardening branch. It owns preflight, runtime safety, Binance market-data health, Hyperliquid execution safety, persistence, reconciliation, operator UI safety, and later shadow-only promotion loading.

## Active stage rules

- Check `docs/ORCHESTRATOR_STAGE_LEDGER.md` before starting work.
- Write a work packet before coding.
- Keep changes inside the allowed paths listed by the work packet.
- Update `docs/KNOWN_ISSUES.md` when a blocking risk is discovered.
- Do not advance a stage while any P0 issue is open or four or more P1 issues are unresolved.

## Live boundary

- Live mode must fail closed on unsafe configuration.
- Live mode must reject default secrets and disabled hard risk caps.
- Live mode must reject research jobs.
- Live mode must reject `research_only` or `observe_only` artifacts as live inputs.
- Research artifacts may be loaded only through an approved promotion validator, and initially only for shadow diagnostics.

## Validation baseline

Use focused validation for scoped work and broaden tests when shared contracts change:

```powershell
python -m compileall -q src/tradingbotsuite
$env:PYTHONPATH='src'; python -m pytest tests/contracts -q
```
