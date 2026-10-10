# Binance lead · 喂价套利

Chainlink's settlement TWAP follows Binance spot with a lag. When spot has already moved since the market opened and the book has not priced it, take that side. Reads each coin's own Binance spot feed (declare one per coin; no HYPE).

Chainlink 结算 TWAP 跟随币安现货但有滞后。现货自开盘以来已经明显移动、盘口还没跟上时，买入这一边。每个币读自己的币安现货流（每个币都要声明；HYPE 没有）。

Runs on the hosted backtest only.
Data: settlement, book, binance:btcusdt:spot:1s · intervals: 5m.

## Run it

Python 3.14 — `python/strategy.py`:

```bash
ot check binance-lead/python
# reads the Binance reference feed, which only the hosted backtest has.
# needs a backtest key; one market-day = one credit
export OT_BACKTEST_KEY="bt_…"
ot submit binance-lead/python --assets btc --days 7
```

Node.js 24 — `nodejs/strategy.mjs`:

```bash
ot check binance-lead/nodejs
# reads the Binance reference feed, which only the hosted backtest has.
# needs a backtest key; one market-day = one credit
export OT_BACKTEST_KEY="bt_…"
ot submit binance-lead/nodejs --assets btc --days 7
```

## Parameters

Edit them in `outcometick.json`; the strategy reads them as `ctx.p`.

| param | default |
| --- | --- |
| `window_s` | `180` |
| `stop_s` | `10` |
| `min_move_bps` | `5` |
| `max_px` | `0.65` |
| `notional` | `50` |

A starting point, not a proven edge. One sample day says nothing about next month: backtest it over the
full window before trusting any number it prints.
