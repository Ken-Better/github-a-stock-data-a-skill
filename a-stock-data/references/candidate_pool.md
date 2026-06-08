# Candidate Pool Schema

Inspired by AstraTrade `stock-ranker`, but simplified for a static cloud dashboard.

Each candidate should be complete and evidence-backed:

```json
{
  "rank": 1,
  "code": "600000",
  "name": "股票名",
  "score": 82.5,
  "action": "watch",
  "position_pct": 5,
  "entry": "放量突破或回踩确认",
  "stop_loss": "-5%",
  "take_profit": "+8% to +12%",
  "evidence": [
    "板块涨幅靠前",
    "成交额活跃",
    "新闻事件映射"
  ],
  "risk_flags": [],
  "factors": {
    "trend": 0,
    "flow": 0,
    "event": 0,
    "sector": 0,
    "risk": 0
  }
}
```

Rules:

- Output at most five high-quality candidates for the top panel.
- If evidence is empty, do not output the candidate.
- If risk cannot be estimated, output `watch` with `position_pct` 0.
- This is a monitor candidate pool, not an order list.
