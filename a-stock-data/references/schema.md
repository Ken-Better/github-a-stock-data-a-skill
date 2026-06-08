# A-Stock Data Schema

## Snapshot

```json
{
  "meta": {
    "version": "1.0.0",
    "provider": "eastmoney-public",
    "timestamp": "2026-06-08T10:00:00+08:00",
    "market_open": true
  },
  "indices": [
    {
      "code": "000001",
      "name": "上证指数",
      "price": 0,
      "change_pct": 0,
      "change": 0
    }
  ],
  "sectors": [
    {
      "code": "BK0000",
      "name": "板块名",
      "change_pct": 0,
      "main_flow_yuan": 0,
      "turnover_yuan": 0,
      "up_count": 0,
      "down_count": 0
    }
  ],
  "gainers": [
    {
      "code": "600000",
      "name": "股票名",
      "price": 0,
      "change_pct": 0,
      "turnover_yuan": 0,
      "volume": 0,
      "main_flow_yuan": 0
    }
  ],
  "active": [],
  "signals": {
    "breadth": 0,
    "risk_level": "normal",
    "top_sector": "",
    "top_gainer": ""
  },
  "errors": []
}
```

## Notes

- `main_flow_yuan` is provider-specific and can be missing or delayed.
- `market_open` is computed locally for China time and excludes lunch break.
- Consumers should render stale timestamps clearly.
