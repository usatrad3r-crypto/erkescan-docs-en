# Reading the table

Read the number, its unit and its time window together. Colour helps locate a value; it does not determine a trade. The [column reference](column-reference.md) defines every metric.

## Formats and units

| Display | Meaning |
| --- | --- |
| Price or Change$ | USDT per unit of the contract's underlying quotation |
| Volume, VDelta, Open Interest, OI dollar change | USDT turnover or position value; not a count of coins |
| K / M / B | Thousand / million / billion; `1.20M` is 1,200,000 |
| Change or OI Change `3.5%` | A 3.5% change from the relevant reference |
| Funding `0.010%` | 0.01% per funding period, not 1% or an annual rate |
| RVOL `2.00×` | Twice the relevant volume baseline |
| Ticks | Number of aggregate-trade events |
| BTC Corr `0.74` | A correlation coefficient, not 74% price growth |
| RetailHeat `149.8 (p87)` | Events per $1M equivalent turnover, with a percentile rank |

Percentage and percentage points are different. A funding rate moving from 0.01% to 0.02% rises by **0.01 percentage points**, or **100% relative to its previous value**. An alert on Funding `> 0.02` tests the rate itself; it does not test either change.

OI Change contains a dollar change and a percentage, such as `$1.20M (3.41%)`. Its dollar part values the change in contract quantity at the current price; it is not necessarily the difference between two historical dollar OI totals. Read the percentage for OI-change alert thresholds.

## Colour

Signed changes, VDelta, funding and OI change use positive/negative colouring. Price, unsigned volume, open interest and counts have no buy/sell direction. RVOL and BTC correlation have their own presentation rules. Trend is green when its last buffered price is at least its first, otherwise red. Read labels and signs as well as colours.

The fast Bar Vol Δ fields compare an unfinished candle with a completed one. A negative reading there can simply reflect an incomplete bar; it is not a negative price return.

## Dash, zero and asterisk

**—** means unavailable or undefined. It must not be replaced with zero. A genuine zero can be a valid observation. Missing values are kept at the end of a numeric sort; favourites remain a separate block, so this is not a single global ordering.

RetailHeat uses a primary calculation when the last closed 5m candle has at least 50,000 USDT of turnover and a usable Ticks count. Between 5,000 and 50,000 USDT it may use a smoothed denominator and show `*`. Below 5,000 USDT, or with unusable inputs, it shows a dash. Exactly 50,000 belongs to the primary path; exactly 5,000 can use the smoothed path.

The numerator counts rolling five-minute events; the primary denominator is a completed candle. They need not cover the same five minutes. RetailHeat is not a direct measure of average order size and cannot identify retail or institutional traders. Its percentile includes all usable primary and smoothed values; ties share the fraction of values strictly below them.

## Labels and Trend

Sector labels describe a category. **STOCK** and **COMMODITY** describe a stock/index-linked or commodity-linked perpetual derivative; they do not mean that holding the contract owns a share, a fund unit or physical commodity. Verify unfamiliar instruments against the exchange's contract specification. A missing logo or badge is not proof of missing market data.

Trend is a small browser-built price line. It starts from a shorter candle seed, accumulates observations while the tab is open and resets on reload. It is not a guaranteed four-hour chart immediately after opening the page. Open the [symbol chart](coin-view.md) for axes and interval controls.

## Connection and freshness

The footer distinguishes streaming, polling, reconnecting, stale and error states. Polling can still display **Connected**, with a gold indicator and a **Polling** tooltip. Stale/error also raises a warning above the table.

The application monitors accepted snapshots and overall progress of price updates. These are shared health checks, not proof that every individual field has just changed. A stable completed-candle value can be correct; a frozen live price needs investigation. [Troubleshooting](troubleshooting.md) explains the checks.

Next: [Column reference](column-reference.md).
