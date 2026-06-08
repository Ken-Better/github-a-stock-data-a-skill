---
name: a-stock-data
description: Fetch and normalize public A-share market data for dashboards, monitors, and trading research, including Eastmoney sectors, top gainers, indices, northbound-style proxy signals, news inputs, and JSON schemas for downstream recommendation engines.
---

# A-Stock Data

Use this skill when a task needs A-share market data for a website, monitor, scanner, dashboard, or research script. Prefer the bundled script for deterministic data pulls instead of rewriting HTTP parsing each time.

## Workflow

1. Use `scripts/a_stock_data.py` as the data adapter.
2. Fetch a snapshot with:

```bash
python a-stock-data/scripts/a_stock_data.py snapshot --pretty
```

3. For a website or monitor, import the module and call:

```python
from a_stock_data import fetch_snapshot

data = fetch_snapshot()
```

4. Treat failed providers as partial data, not fatal errors. The adapter returns `errors` and keeps available fields populated.
5. For trading recommendations, combine this data with separate risk rules. Do not turn a single bullish event into an unconditional buy signal.

## AstraTrade Compatibility

This skill can feed an AstraTrade-style monitor:

- Use `scripts/a_stock_data.py rank` to produce a compact candidate pool.
- Candidate records follow the fields in `references/candidate_pool.md`.
- If `MX_APIKEY` is available, agents may enrich the public snapshot with Eastmoney MX-style natural-language data/search tools, but the public adapter must continue to work without secrets.
- Recommended dashboard sections: market state, hot sectors, candidate pool, alert schedule, evidence, and risk flags.

## Data Included

- Major A-share indices.
- Industry and concept sector performance.
- Top gainers and active stocks.
- Main-force flow fields where available from the public endpoint.
- Basic market session status for China time.
- Provider health and timestamp metadata.

## Output Contract

Read `references/schema.md` when you need exact field names. The high-level shape is:

```json
{
  "meta": {},
  "indices": [],
  "sectors": [],
  "gainers": [],
  "active": [],
  "signals": {},
  "errors": []
}
```

## Guardrails

- Public endpoints can throttle or change shape. Always code fallback paths.
- GitHub Actions scheduled workflows can be delayed by the platform. Store timestamps and show data freshness in the UI.
- This skill provides data plumbing, not financial advice.
