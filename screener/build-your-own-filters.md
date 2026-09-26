# Build your own screen

ErkeScan offers fixed quick filters, sorting, symbol search, favourites and a saved column layout. It does not currently offer a saved builder for arbitrary numeric screener rules. This page shows how to make a repeatable manual screen.

## A repeatable procedure

1. Write the observation you want, for example: “Compare contracts with rising open interest and small hourly price changes.”
2. Choose a time window. Check the [column reference](column-reference.md): price changes are rolling; Volume 5m is a completed candle; Volatility 1h covers a series of hourly candles, not just one hour.
3. Open **Columns** and show the required metrics. Keep the values you need next to each other.
4. Choose a [quick filter](quick-filters.md) if its fixed rule fits. Otherwise choose **All** and apply your thresholds by reading the rows.
5. Sort with the header caret. A sort applied after a quick filter changes the order inside the matching set. It does not add a second threshold.
6. Check missing values and the connection status. A dash cannot be interpreted as zero.
7. Star the rows you want to revisit. Favourites do not bypass search or filter rules.
8. Record the filter, columns, sort, observation time and manual thresholds. Only the layout and favourites persist in this browser; the active filter and sort do not.

## Example: compare open-interest growth

Select **OI Spike**, which requires OI Change 1h above +5%. Show OI Change 1h, Change 1h, Volume 1h and VDelta 1h. Read the percentage leg of OI Change for the filter rule; its dollar leg is a different unit. Sort Volume 1h if you want to compare turnover among these matches.

This screen finds a numeric combination. It does not show the number of traders, whether they are institutions, or which participant initiated a new position. Dollar open interest also changes with price, whereas OI Change percent is based on open-contract quantity.

## Example: compare funding

Select **High Funding**. It includes both signs when absolute funding exceeds 0.1% per funding period. Show Funding Rate, Change 1h and Volume 1h. Record the sign separately: positive funding means longs pay shorts; negative means the reverse.

Funding periods can differ across contracts. A raw rate comparison is not a comparison of annual returns or a prediction of direction.

## What a manual threshold can and cannot do

An example turnover threshold such as 500,000 USDT narrows a list; it does not certify available order-book depth. RVOL compares activity with a recent baseline, while absolute volume measures turnover. Neither alone answers how an order of a given size would fill.

RetailHeat is events per turnover with partly different numerator and denominator windows. It does not identify retail or institutional accounts. A low BTC correlation means a weak linear relationship in the sampled window, not statistical independence or future protection from a BTC move.

Bar Vol Δ compares turnover with the previous candle. The 5m/15m/1h legs include the forming bar, so comparisons depend on bar progress. They can still differ across contracts at the same moment; they are not simply a timer.

## Move a condition to an alert

Custom alerts support a subset of columns. RVOL, RetailHeat, BTC correlation, Change$ and Bar Vol Δ are not alert conditions. A raw Volume or Ticks threshold answers a different question and is not an equivalent replacement for a ratio.

An alert checks the whole supported universe. It does not inherit a chip, search result or favourites. Several conditions use AND on the same contract; separate alerts provide separate rules, not a single combined OR notification. [Create an alert](../alerts/create-an-alert.md).

Next: [Example screens](recipes.md).
