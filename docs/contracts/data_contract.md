# Data Contract

Live runtime may consume market data from approved live adapters and may inspect research manifests only as metadata.

## Research manifest requirements

Research datasets must include:

```json
{
  "manifest_version": "data-manifest-v1",
  "research_only": true,
  "source_name": "binance_vision | binance_rest | crypto_lake | hyperliquid_archive",
  "source_type": "archive | rest | websocket_capture | local_file",
  "symbol": "BTCUSDT",
  "data_family": "kline | trade | agg_trade | book_ticker | depth_snapshot | funding_rate | open_interest | premium_index | liquidation | user_fill | order_event | position_snapshot",
  "event_time_field": "event_time_ms",
  "receive_time_field": "receive_time_ms",
  "receive_time_unavailable_reason": null,
  "start_time_ms": 0,
  "end_time_ms": 0,
  "row_count": 0,
  "schema_version": "family-schema-v1",
  "content_hash": "sha256",
  "normalized_fields": [],
  "missing_fields": [],
  "quality_flags": [],
  "non_promotable_reasons": []
}
```

## Live rules

- Live order decisions must use live market-data health, stale-feed checks, account state, and reconciliation.
- Archive data is not live fillability evidence.
- Missing receive-time evidence blocks live-like latency claims.
- Missing market context must be explicit missingness, not silent zero-fill.
