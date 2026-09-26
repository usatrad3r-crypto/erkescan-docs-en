# From a screener row to a checked observation

The screener helps organise market observations. A row, colour or filter match does not decide an order, a position size or an exit. The screener and custom-alert workflow described here does not place trades.

## Check the observation

1. Read the connection state and any freshness warning.
2. Confirm the contract and venue. Similar tickers on another venue can describe a different instrument.
3. Read the exact metric and window. Change 5m is rolling, while Volume 5m is the last completed candle; the two are not the same five-minute interval.
4. Keep units separate. Price is USDT per unit; Volume is turnover; OI Change shows a quantity-based percentage and a dollar-valued change; Funding is percent per funding period.
5. Treat missing values as unavailable. A missing VDelta is not balanced buying and selling.

## Open the chart

Click the ticker on desktop or the card on mobile. Confirm the instrument and interval displayed by TradingView. The chart and the screener have separate update paths, so compare timestamps as well as numbers. If the chart is unavailable for an instrument, do not infer that the screener value is automatically invalid or that a different instrument is equivalent.

The [Charts page](charts.md) provides group context. Its normalized lines start at 0% at the first usable observation in the selected window. A line at +4% means a 4% change from that starting observation, not a $4 price or a four-percentage-point funding change.

## Record facts separately from interpretation

Example using invented numbers:

| Observation | What it supports | What it does not prove |
| --- | --- | --- |
| Change 1h = +3.2% | Price increased relative to the hourly reference | That the increase will continue |
| OI Change 1h = +4% | Open-contract quantity increased over the sample window | That only longs were opened or that new cash of a known amount entered |
| VDelta 5m = +80,000 USDT | Buyer-initiated turnover exceeded seller-initiated turnover | The identity or intention of participants |
| Funding = +0.02% | Positive payment direction for the displayed funding interval | The next price direction or your realized funding payment |

Several facts can be consistent with multiple explanations. RetailHeat is not an account classifier; correlation is not causation; turnover is not order-book depth.

## Save a reproducible note

Record the symbol, venue, date and timezone, selected filter, units, relevant values, missing fields and chart interval. Later you can compare observations without relying on memory.

If you want a reminder when a supported numeric condition holds, create an [alert](../alerts/create-an-alert.md). It checks the whole supported universe, including unstarred contracts, and can fire again after its cooldown while a condition remains true. It is not a price-crossing detector or an order instruction.

Next: [Coin view](coin-view.md).
