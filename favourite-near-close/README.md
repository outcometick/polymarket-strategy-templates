# Favourite near close · 临近结算吃单

In the last minute, buy the side the settlement feed says is winning, if the book still sells it below a ceiling. Hold to settlement.

最后一分钟里，按结算流判断哪一边在领先；盘口卖价还低于上限时买入这一边，持有到结算。

Runs locally on the free sample day, and on the hosted backtest.
Data: settlement, book · intervals: 5m.

## Run it

Python 3.14 — `python/strategy.py`:

```bash
ot check favourite-near-close/python
# the free sample day (one download, no key)
curl -L https://github.com/outcometick/polymarket-tick-data-samples/releases/latest/download/polymarket-data-samples.tar.gz | tar xz
ot run favourite-near-close/python --data ./polymarket-data-samples
```

Node.js 24 — `nodejs/strategy.mjs`:

```bash
ot check favourite-near-close/nodejs
# the free sample day (one download, no key)
curl -L https://github.com/outcometick/polymarket-tick-data-samples/releases/latest/download/polymarket-data-samples.tar.gz | tar xz
ot run favourite-near-close/nodejs --data ./polymarket-data-samples
```

## Parameters

Edit them in `outcometick.json`; the strategy reads them as `ctx.p`.

| param | default |
| --- | --- |
| `enter_at_s` | `60` |
| `min_lead_bps` | `2` |
| `px_min` | `0.55` |
| `px_max` | `0.95` |
| `notional` | `50` |

A starting point, not a proven edge. One sample day says nothing about next month: backtest it over the
full window before trusting any number it prints.
