# Spread quote (market making) · 双边挂单（做市）

Rest a bid for UP at the best bid and a bid for DOWN at one minus the best ask. A filled pair is worth $1 at settlement, so each pair earns the spread. The side you are long of is capped (pairs are hedged), quotes are pulled near the close, and the report's maker panel shows fill rate and markouts.

在买一挂 UP 的买单、在 1 − 卖一挂 DOWN 的买单。两边各成交一份就凑成一对，到结算值 1 美元，赚的就是价差。持有较多的那一边有上限（凑成对的部分是对冲的），临近收盘撤掉报价；报告的挂单面板给出成交率和成交后的价格走势。

Runs locally on the free sample day, and on the hosted backtest.
Data: settlement, book, trades · intervals: 5m.

## Run it

Python 3.14 — `python/strategy.py`:

```bash
ot check spread-quote/python
# the free sample day (one download, no key)
curl -L https://github.com/outcometick/polymarket-tick-data-samples/releases/latest/download/polymarket-data-samples.tar.gz | tar xz
ot run spread-quote/python --data ./polymarket-data-samples
```

Node.js 24 — `nodejs/strategy.mjs`:

```bash
ot check spread-quote/nodejs
# the free sample day (one download, no key)
curl -L https://github.com/outcometick/polymarket-tick-data-samples/releases/latest/download/polymarket-data-samples.tar.gz | tar xz
ot run spread-quote/nodejs --data ./polymarket-data-samples
```

## Parameters

Edit them in `outcometick.json`; the strategy reads them as `ctx.p`.

| param | default |
| --- | --- |
| `size` | `20` |
| `max_inventory` | `100` |
| `min_spread` | `0.01` |
| `px_min` | `0.1` |
| `px_max` | `0.9` |
| `requote_ms` | `1000` |
| `stop_quoting_s` | `30` |

A starting point, not a proven edge. One sample day says nothing about next month: backtest it over the
full window before trusting any number it prints.
