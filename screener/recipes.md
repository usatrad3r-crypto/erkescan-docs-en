# Example screens

These examples show how to ask the data a defined question. They are not entry rules, forecasts or evidence of a trading advantage. Exact built-in thresholds are listed once in [Quick filters](quick-filters.md).

| Observation | Start with | Add or inspect | Important limit |
| --- | --- | --- | --- |
| Unusual short-term turnover | High Volume | Volume 5m, VDelta 5m, Change 5m | RVOL measures a closed candle; Change 5m is rolling |
| Large hourly moves | Big Movers | Change 1h, Volume 1h, OI Change 1h | Both positive and negative moves qualify |
| OI growth with a small price change | Accumulation | OI Change 1h, Change 1h, RVOL 1h | A name for a combination, not proof of accumulation |
| OI growth above a fixed level | OI Spike | OI percentage and dollar legs | Growth only; falling OI does not match |
| Low sampled volatility with directional taker flow | Breakout | Volatility 5m, RVOL 5m, VDelta 5m, Volume 5m | A below-median value does not confirm a price breakout |
| Funding and price moving in opposing directions | Squeeze | Funding, Change 1h, OI Change 1h | Does not measure forced liquidations |
| Large funding rates | High Funding | Funding sign and interval, Volume 1h | Compare payment periods as well as rates |
| Most aggregate-trade activity among eligible symbols | Top Active 10 | Ticks 5m, RetailHeat, Volume 5m | Ranking is Ticks, not RetailHeat |
| Largest daily percentage changes | Top Gainers/Losers 1D | Change 24h, Change 1h | 24h is rolling, not a calendar day |
| Compare a contract with BTC | All, then search | BTC Corr 1h and 1d | Low correlation does not establish independence |
| Build a list to revisit | All or a relevant filter | Star chosen rows | Favourites are local and do not scope alerts |
| Compare turnover during broad market activity | A relevant filter, then Volume 1h sort | Volume 24h and data status | Turnover is not a fill-quality guarantee |

## Walkthrough: observe price and volume

1. Select High Volume and show RVOL 5m, Volume 5m, VDelta 5m and Change 5m.
2. Read the units: RVOL `2.4×` is a ratio; Volume `500K` is 500,000 USDT; Change `2%` is a price return.
3. Check the sign of VDelta, which identifies net taker buying or selling over its own window. It does not establish whether those trades opened or closed positions.
4. Open a symbol chart and compare the same contract. Record the time, because the screener and external chart update independently.
5. If any input is missing or stale, record that limitation instead of substituting zero.

## Walkthrough: observe a changing shortlist

Select Top Gainers 1D and note the current eligible symbols. Sort Volume 1h with the caret to compare turnover inside the set. Star any rows you want to revisit. A row can leave the filter because another contract overtook it or eligibility changed; it need not have fallen in price.

To find a starred symbol that disappeared, select All and clear search. For unattended observation, create a separate alert on supported metrics. It will watch the whole supported market, including contracts that are not starred.

## Keep examples reproducible

Record the date, selected filter, sort, columns and units. Repeat with the same setup when comparing sessions. Message frequency and the number of matches depend on the market; no example guarantees a certain number of matches per day.

Next: [From a row to a checked observation](from-screen-to-trade.md).
