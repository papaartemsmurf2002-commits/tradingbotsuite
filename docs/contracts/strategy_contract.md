# Strategy Contract

Strategy artifacts are research outputs unless a promotion validator accepts them for shadow-only use.

## Plugin shape

```python
class StrategyPlugin:
    strategy_id: str
    strategy_version: str
    allowed_holding_periods: tuple[str, ...]
    required_feature_sets: tuple[str, ...]

    def prepare(self, train_context): ...
    def predict(self, feature_frame): ...
    def explain(self, prediction_frame): ...
```

## Live rules

- Live runtime must not import experimental strategy plugins directly.
- Strategy output must not control live order placement at this stage.
- Risk governor remains live-owned and cannot be controlled by model output.
- Shadow diagnostics may display strategy output only after promotion validation.
