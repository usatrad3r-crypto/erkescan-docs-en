# Charts page

Open **Charts** at `/charts` to compare recent price and open-interest changes across a selected group. An active subscription is required.

## Choose the group and window

| Cohort | Ranking |
| --- | --- |
| Top Gainers · 24h | Largest positive rolling 24h price changes |
| Top Losers · 24h | Largest negative rolling 24h price changes |
| Top Volume · 24h | Largest rolling 24h turnover |
| Top Active · 5m | Most aggregate trade events over the trailing five minutes |

Cohorts pass an hourly turnover floor of 500,000 USDT. Gainers, losers and active cohorts also use the screener's primary RetailHeat availability gate; gainers and losers require at least 1.5% movement in the corresponding direction. The volume cohort does not use those additional gates. Unsupported chart tickers or missing series can reduce the number of lines. Turnover is a selection rule, not a guarantee of order-book liquidity or execution quality.

The default window is **4H**. Select **1H**, **4H**, **1D**, **1W** or **1M**. These control the plotted history, independently of the cohort's ranking window.

| Window | Price sampling | OI sampling |
| --- | --- | --- |
| 1H | 1 minute | 5 minutes |
| 4H | 5 minutes | 5 minutes |
| 1D | 15 minutes | 15 minutes |
| 1W | 1 hour | 1 hour |
| 1M | 4 hours | 4 hours |

## Read the panels

**Trader summary** summarises the displayed group. It is descriptive context, not an independent forecast.

**Price rotation** rebases each available series to **0% at its first plotted point**. A line at +5% means an increase of 5% from that baseline; it does not mean a price of $5 or necessarily the screener's 24h change. Compare changes and timing, checking the chart's timestamps when history differs.

**Open-interest rotation** also rebases each series to 0% at its first point. The chart shows changes in the provided OI series, not net inflows or a direct count of bullish versus bearish traders. In particular, changes in dollar-valued OI can include the effect of changing prices. Price and OI together do not identify which side opened, closed or was liquidated.

**Return buckets** group returns over the chosen window. The horizontal axis is the return range; the height is the number of available cohort members in that range. Read the actual number of plotted members rather than assuming a fixed ten-instrument sample.

**Funding table** shows up to twelve valid rates ranked by absolute size after the hourly turnover filter. Rates are percentages for each contract's own funding period. Positive means longs pay shorts; negative means shorts pay longs. Different settlement intervals make direct rate comparisons incomplete. The table is separate from the selected cohort and does not measure trader counts.

Use the download control to save a chart. Record the window and current cohort when sharing it: membership changes with current rankings, and historical lines are shown for today's selected members. This is not a historical backtest of a fixed strategy.

## A practical review

1. Find an instrument in the screener and note the metric and window that caught your attention.
2. Select a relevant cohort and chart window. Your instrument may not be a member; cohort selection is not a manual symbol watchlist.
3. Compare relative changes and their timing, without inferring the next move from who moved first.
4. Return to the row for exact metric units, OI change, VDelta and freshness.

Next: [Troubleshooting](troubleshooting.md).
