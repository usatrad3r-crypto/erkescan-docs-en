# Troubleshooting the screener

Start with the visible connection status, the active filter and search text. An empty result and missing data are different states.

| What you see | What to check |
| --- | --- |
| No rows | Select **All**, clear search, then check access and connection status. A restrictive chip or unmatched search can legitimately return nothing. |
| Fewer than ten rows in a top filter | Only qualifying rows are included; hourly turnover, primary RetailHeat availability and, for movers, minimum directional change all matter. Ten is a maximum, not a target. |
| **—** in a cell | The value is unavailable or lacks a usable baseline. It is not zero. Newly listed instruments may lack history. |
| Values stop changing | Closed-candle metrics hold between closes. Check a live metric and the status indicator before diagnosing a failure. |
| Stale or connection warning | Wait for recovery and inspect timestamps. A displayed last good snapshot is not a promise that the exchange is still at those prices. Reload once if necessary. |
| Unexpected sort order | Use the separate sort caret, not the filter control. Favourites appear in a separate block. Selecting another chip resets the previous sort; an explicit sort then orders its matching rows. |
| Symbol or Trend cannot be hidden | Both are permanently visible. The column picker controls the other columns. |
| A hidden setting returns after reload | See the persistence table in [Personalize](personalize.md). Search, chip selection and sort are temporary controls. Browser storage may be cleared or unavailable. |
| A favourite is missing | Search and filtering still affect the result; confirm the instrument remains available. Favourites are local to this browser. |
| A chart will not load | Check the ticker, venue and external chart availability. A widget failure alone is not a delisting notice. |

## Values that look inconsistent

**Change 5m, 15m and 8h:** these are rolling comparisons, including alert conditions. They are not measured only since the latest candle boundary. Stored observations and fallback candle references may make the base approximate.

**RVOL 15m:** this uses a closed 15-minute candle. A constant reading inside the next candle is expected. RVOL 1h is different: its numerator steps with closed five-minute candles and uses an hourly-series baseline.

**Bar Vol Δ:** the 5m, 15m and 1h versions compare an unfinished candle with a completed one. An early negative value is partly an effect of elapsed time. The 8h and 1d versions compare completed candles.

**Funding:** `0.010%` is one hundredth of a percent for the contract's funding period. It is not 1%, an annual rate, or necessarily an eight-hour rate.

**OI:** total dollar-valued OI and OI Change % are not interchangeable. Price can increase the dollar valuation while the quantity of open positions is unchanged.

**VDelta 1D versus Volume 24h:** these use different windows. Do not treat them as a same-period fraction.

**RetailHeat and Ticks:** aggregated events are not traders. The asterisk identifies a smoothed RetailHeat calculation. Top Active ranks Ticks 5m, with additional inclusion rules; sorting RetailHeat will not reproduce that ranking.

See [Column reference](column-reference.md) for all windows and units. For delivery problems use [Managing alerts](../alerts/managing-alerts.md).

## Report a reproducible problem

Include the page, interface language, ticker, exact column, time with timezone, connection status, active chip and search, and the action that produced the problem. A screenshot can help; hide account information. Do not send passwords, tokens or exchange API keys. Compare against the same instrument and window when supplying an exchange reference.
