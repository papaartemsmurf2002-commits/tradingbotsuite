# Artifact Contract

Live branch must reject research artifacts as live inputs.

## Required research boundary fields

```json
{
  "research_only": true,
  "observe_only": true,
  "promotion_ready": false,
  "live_signal_input": false,
  "position_sizing_input": false,
  "operator_control_input": false,
  "live_execution_input": false,
  "runtime_control_input": false
}
```

## Live rejection rules

- Missing boundary fields fail validation.
- `research_only: true` fails validation for live signal input.
- `observe_only: true` fails validation for live signal input.
- `promotion_ready: false` blocks promotion review.
- Any artifact that sets live control fields to true without promotion approval is invalid.
