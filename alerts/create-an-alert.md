# Create an alert

You need an active subscription and a linked Telegram account for delivery. On the Alerts or Integrations page, use **Connect Telegram**, open the offered bot link, complete the bot confirmation and return to the app. If the popup is blocked, use the visible fallback link. Confirm the connected state, then use **Test Telegram Bot**. Saving a rule and receiving a test message are different checks.

## Create and verify

1. Open **Alerts** and create a new alert, or choose a preset to prefill a draft.
2. Give it a recognisable name of 2–255 characters.
3. For each required metric, choose an operator and enter a number. Leave unused rows empty.
4. Open the advanced fields for **Volatility**, **Ticks** and **VDelta** when needed.
5. Review every condition, the interpreted number and the units. All conditions must match the same contract.
6. Save. Read any warning about Telegram, paused delivery or queueing; a saved card alone does not prove delivery.
7. Confirm the rule is active and inspect the saved conditions. Keep it paused if it is only a practice example.

Presets are editable starting points, not recommendations. The six presets use OI ±5% over 15m, price +3% over 1h, price −3% over 5m, funding >0.05%, and OI 1h >3% together with price 1h <2%. That last condition does not require a flat or positive price.

## Enter numbers in the interface locale

In the **English interface**, `1.5` is one and a half; `50,000` is fifty thousand; `1,234.5` is one thousand two hundred thirty-four and a half. `1,5` is not a valid English decimal. In the **Russian interface**, `1,5` is one and a half and `50 000` is fifty thousand. A decimal point is also accepted there. **Russian `50,000` means fifty, not fifty thousand.**

Plain numbers such as `50000` avoid grouping ambiguity. Negative values are valid for signed metrics. Do not append `%`, `$` or unit words. For input containing separators, read the value echoed by the form before saving.

Percentage thresholds use percentage units: enter `3` for 3%, and `0.1` for 0.1% funding. Enter `500000` for 500,000 USDT volume. These are not decimal fractions such as `0.03` for 3%.

Operators are `>`, `<`, `>=`, `<=` and `=`. Greater/less operators exclude equality; their inclusive versions include it. Equality allows a small numerical tolerance: the difference must be less than the larger of 0.01% of the threshold and 0.000001 in the metric's units. Use an inequality for a practical threshold rather than relying on rounded displayed equality.

## All 29 conditions

The names below identify the fields; the interface may translate them.

| Condition | Unit | Window and meaning |
| --- | --- | --- |
| Change (5m) | % | Rolling price change; reference observations may be approximate |
| Change (15m) | % | Rolling price change; reference observations may be approximate |
| Change (1H) | % | Rolling price change; reference observations may be approximate |
| Change (8H) | % | Rolling price change; reference observations may be approximate |
| Change (24h) | % | Rolling price change; reference observations may be approximate |
| OI Change (5m) | % | Change in OI quantity from a periodic historical snapshot |
| OI Change (15m) | % | Change in OI quantity from a periodic historical snapshot |
| OI Change (1H) | % | Change in OI quantity from a periodic historical snapshot |
| OI Change (8H) | % | Change in OI quantity from a periodic historical snapshot |
| OI Change (1D) | % | Change in OI quantity from a periodic historical snapshot |
| Volume (5m) | USDT | Last closed 5m candle |
| Volume (15m) | USDT | Last 3 closed 5m candles |
| Volume (1H) | USDT | Last 12 closed 5m candles |
| Volume (8H) | USDT | Last closed 8h candle |
| Volume (24h) | USDT | Rolling exchange 24h ticker |
| Volatility (5m) | % | Sample standard deviation of 20 candle returns; about 100m |
| Volatility (15m) | % | Sample standard deviation of 20 candle returns; about 5h |
| Volatility (1H) | % | Sample standard deviation of 20 candle returns; about 20h |
| Ticks (5m) | events | Rolling count of aggregate trade events |
| Ticks (15m) | events | Rolling count of aggregate trade events |
| Ticks (1H) | events | Rolling count of aggregate trade events |
| VDelta (5m) | USDT | Last closed 5m candle |
| VDelta (15m) | USDT | Last 3 closed 5m candles |
| VDelta (1H) | USDT | Last 12 closed 5m candles |
| VDelta (8H) | USDT | Last closed 8h candle |
| VDelta (1D) | USDT | Last closed daily candle; not rolling 24h |
| Funding Rate | % | Per contract funding period |
| Open Interest | USDT | OI quantity × current price |
| Price | USDT | Price per quoted instrument unit |

Change 5m, 15m and 8h use the same target rolling windows as the corresponding screener columns. They do not reset at candle boundaries. OI windows depend on available periodic samples and may not span an exact number of minutes.

RVOL, RetailHeat, BTC correlation, Bar Vol Δ and screener favourites are not alert conditions. You cannot reproduce every quick filter exactly. There is no symbol selector, OR, metric-to-metric division or two-sided range on a single field.

## A neutral practice rule

Name: `Hourly change observation`. Conditions: **Change (1H) > 3** and **Volume (1H) > 500000**. This asks for a positive hourly change above 3% and enough observed hourly turnover. It does not predict continuation or guarantee that a particular instrument will match. Compare the same two columns in the screener, then save only if that observation is useful to you.

If saving fails, read the error: common causes are an incomplete condition, invalid number, inactive access, an expired session, the 200-alert limit or too many edits in a short period. Correct the indicated issue and retry; repeated clicks do not improve delivery.

Next: [Alert recipes](alert-recipes.md) and [Managing alerts](managing-alerts.md).
