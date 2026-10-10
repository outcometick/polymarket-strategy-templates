<!-- Generated from templates/ in the outcometick monorepo by scripts/publish-templates-repo.mjs. Edits here are overwritten. -->
# Polymarket strategy templates

Working backtest strategies for Polymarket and Predict.fun crypto Up/Down markets (5m, 15m), each in
Python and Node.js, for the [outcometick](https://outcometick.com) backtester: replayed against the real
order book and the Chainlink stream each market settles on.

| template | name | what it does | runs |
| --- | --- | --- | --- |
| [`binance-lead`](binance-lead/) | Binance lead · 喂价套利 | Chainlink's settlement TWAP follows Binance spot with a lag. When spot has already moved since the market opened and the book has not priced it, take that side. Reads each coin's own Binance spot feed (declare one per coin; no HYPE). | hosted |
| [`favourite-near-close`](favourite-near-close/) | Favourite near close · 临近结算吃单 | In the last minute, buy the side the settlement feed says is winning, if the book still sells it below a ceiling. Hold to settlement. | local + hosted |
| [`spread-quote`](spread-quote/) | Spread quote (market making) · 双边挂单（做市） | Rest a bid for UP at the best bid and a bid for DOWN at one minus the best ask. A filled pair is worth $1 at settlement, so each pair earns the spread. The side you are long of is capped (pairs are hedged), quotes are pulled near the close, and the report's maker panel shows fill rate and markouts. | local + hosted |

## Quick start

```bash
npm i -g outcometick          # the ot CLI (Node 24)
ot init my-strategy --template favourite-near-close --lang python
ot check my-strategy
curl -L https://github.com/outcometick/polymarket-tick-data-samples/releases/latest/download/polymarket-data-samples.tar.gz | tar xz
ot run my-strategy --data ./polymarket-data-samples
```

Or clone this repository and point `ot` at a template directory. Each template has its own README.

- SDK reference: https://outcometick.com/docs/sdk
- Hosted backtest: https://outcometick.com/backtest
- From an AI coding tool: the npm package includes an MCP server (`ot mcp`) — https://outcometick.com/docs

## 中文

[outcometick](https://outcometick.com/zh) 回测用的策略模板，适用于 Polymarket 与 Predict.fun 的加密货币涨跌市场（5 分钟、15 分钟），
每个模板都有 Python 和 Node.js 两个版本，按真实盘口与市场自己的 Chainlink 结算流重放。

- `binance-lead` 喂价套利：Chainlink 结算 TWAP 跟随币安现货但有滞后。现货自开盘以来已经明显移动、盘口还没跟上时，买入这一边。每个币读自己的币安现货流（每个币都要声明；HYPE 没有）。
- `favourite-near-close` 临近结算吃单：最后一分钟里，按结算流判断哪一边在领先；盘口卖价还低于上限时买入这一边，持有到结算。
- `spread-quote` 双边挂单（做市）：在买一挂 UP 的买单、在 1 − 卖一挂 DOWN 的买单。两边各成交一份就凑成一对，到结算值 1 美元，赚的就是价差。持有较多的那一边有上限（凑成对的部分是对冲的），临近收盘撤掉报价；报告的挂单面板给出成交率和成交后的价格走势。

用法见上面的 Quick start；`ot init` 会把模板复制到新目录。模板是起点，不是已被验证的优势。

License: MIT.
