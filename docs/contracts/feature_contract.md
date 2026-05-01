# Feature Contract

Features used for live or shadow diagnostics must be point-in-time safe.

## Required manifest fields

```json
{
  "feature_set_id": "price_trend_wt3d_v1",
  "feature_set_version": "v1",
  "input_families": [],
  "feature_columns": [],
  "availability_columns": [],
  "point_in_time_safe": true,
  "max_feature_age_ms": null,
  "fit_scope": "train_only | stateless",
  "imputation_policy": "explicit_missingness_plus_train_only_neutral",
  "leakage_risks": [],
  "tests": []
}
```

## Live rules

- Live branch must not compute experimental research features inside execution safety code.
- Shadow feature loaders must report missingness and drift.
- Future-looking feature transforms are invalid for shadow or live use.
