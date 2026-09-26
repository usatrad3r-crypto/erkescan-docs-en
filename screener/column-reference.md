# Column reference

The table below covers all 57 columns. Symbol and Trend stay visible; the picker controls the other 55. Nineteen columns are visible by default. Header abbreviations can differ between the table and the picker.

Dollar-labelled market values are quoted in **USDT**. A percent, a percentage-point change, a multiple and a dollar amount are different units. An unavailable value is shown as a dash.

## All columns

| Column | Unit | Calculation window or basis |
| --- | --- | --- |
| SYMBOL | — | Contract identifier and optional category |
| TREND | — | Browser price buffer, up to the available history |
| PRICE | USDT/unit | Latest available traded price; midpoint can be used as a fallback |
| FUNDING RATE | % / funding period | Published contract funding rate; not annualised |
| OPENINTEREST | USDT | Open-contract quantity valued at the current price |
| CHANGE (5m) | % | Rolling price change; reference-source caveats below |
| CHANGE$ (5m) | USDT/unit | The same price window in USDT |
| CHANGE (15m) | % | Rolling price change; reference-source caveats below |
| CHANGE$ (15m) | USDT/unit | The same price window in USDT |
| CHANGE (1h) | % | Rolling price change; reference-source caveats below |
| CHANGE$ (1h) | USDT/unit | The same price window in USDT |
| CHANGE (8h) | % | Rolling price change; reference-source caveats below |
| CHANGE$ (8h) | USDT/unit | The same price window in USDT |
| CHANGE (24h) | % | Rolling price change; reference-source caveats below |
| CHANGE$ (24h) | USDT/unit | The same price window in USDT |
| VOLUME (5m) | USDT | Last closed 5m candle |
| VOLUME (15m) | USDT | Last 3 closed 5m candles |
| VOLUME (1h) | USDT | Last 12 closed 5m candles |
| VOLUME (8h) | USDT | Last closed 8h candle |
| VOLUME (24h) | USDT | Rolling 24h ticker turnover |
| RVOL (5m) | × | Last closed 5m volume / mean of 18 preceding bars when the 20-bar buffer is full |
| RVOL (15m) | × | Last closed 15m bar / mean of preceding retained closed 15m bars |
| RVOL (1h) | × | Trailing closed-candle hour / approximate baseline from the hourly buffer |
| RVOL (8h) | × | Last closed 8h bar / preceding closed-bar average |
| RVOL (1d) | × | Last closed daily bar / preceding closed-bar average |
| VDELTA (5m) | USDT ± | Last closed 5m candle |
| VDELTA (15m) | USDT ± | Last 3 closed 5m candles |
| VDELTA (1h) | USDT ± | Last 12 closed 5m candles |
| VDELTA (8h) | USDT ± | Last closed 8h candle |
| VDELTA (1d) | USDT ± | Last closed daily candle; unlike rolling Volume 24h |
| BAR VOL Δ$ (5m) | USDT ± | Forming candle against preceding completed candle |
| BAR VOL Δ% (5m) | % | Forming candle against preceding completed candle |
| BAR VOL Δ$ (15m) | USDT ± | Forming candle against preceding completed candle |
| BAR VOL Δ% (15m) | % | Forming candle against preceding completed candle |
| BAR VOL Δ$ (1h) | USDT ± | Forming candle against preceding completed candle |
| BAR VOL Δ% (1h) | % | Forming candle against preceding completed candle |
| BAR VOL Δ$ (8h) | USDT ± | Two completed candles |
| BAR VOL Δ% (8h) | % | Two completed candles |
| BAR VOL Δ$ (1d) | USDT ± | Two completed candles |
| BAR VOL Δ% (1d) | % | Two completed candles |
| OI CHANGE (5m) | USDT and % | Approximate interval from OI samples; not a price-candle return |
| OI CHANGE (15m) | USDT and % | Approximate interval from OI samples; not a price-candle return |
| OI CHANGE (1h) | USDT and % | Approximate interval from OI samples; not a price-candle return |
| OI CHANGE (8h) | USDT and % | Approximate interval from OI samples; not a price-candle return |
| OI CHANGE (1d) | USDT and % | Approximate interval from OI samples; not a price-candle return |
| VOLATILITY (5m) | % | Sample standard deviation of candle returns; about 100m |
| TICKS (5m) | events | Rolling wall-clock interval |
| VOLATILITY (15m) | % | Sample standard deviation of candle returns; about 5h |
| TICKS (15m) | events | Rolling wall-clock interval |
| VOLATILITY (1h) | % | Sample standard deviation of candle returns; about 20h |
| TICKS (1h) | events | Rolling wall-clock interval |
| RETAILHEAT (5m) | events / $1M | Ticks 5m / closed-candle turnover; smoothed baseline is possible |
| BTC CORR (5m) | −1…+1 | Return correlation; up to 20 candles, about 100m |
| BTC CORR (15m) | −1…+1 | Return correlation; up to 20 candles, about 5h |
| BTC CORR (1h) | −1…+1 | Return correlation; up to 20 candles, about 20h |
| BTC CORR (8h) | −1…+1 | Return correlation; up to 20 candles, about 160h |
| BTC CORR (1d) | −1…+1 | Return correlation; up to 20 candles, about 20d |

## Price-change windows

Change 5m, 15m and 8h in the table and in custom alerts refer to rolling windows. They do not reset to zero at a candle boundary, and Change 8h is an available alert condition. The corresponding Change$ columns use the same intended window in quote-currency units.

Five- and fifteen-minute price references normally come from recorded price samples; candle references can be used when that history is unavailable. Eight-hour change uses an hourly candle reference near eight hours ago. These are sampled comparisons, not a guarantee of an observation at the exact millisecond requested. Hourly change normally uses a five-minute reference near one hour ago; a fresh hourly-candle fallback can be used during incomplete history. Missing or stale reference data can leave a dash.

Change 24h and Change$ 24h use the exchange's rolling ticker reference and the latest available price. They are not changes since local midnight. Quote updates, candle closes and ticker refreshes arrive at different times.

## Volume, RVOL and VDelta

Volume is quote turnover. VDelta is buyer-initiated quote volume minus seller-initiated quote volume over its stated window. It measures taker direction, not the number of long versus short positions. VDelta 1d uses a daily candle, while Volume 24h is rolling; those two should not be divided as if their windows matched.

RVOL is a multiple of a historical volume baseline. RVOL 5m and 15m use completed candles and normally hold between their respective closes. RVOL 1h is different: the numerator sums twelve closed 5m candles, while the baseline comes from a retained hourly volume sum. It steps with 5m closes and is an approximation, not a clean single hourly-bar comparison.

Bar Vol Δ$ is current comparison volume minus reference volume. Bar Vol Δ% divides that difference by reference volume and multiplies by 100. A zero reference makes the percentage undefined. For 5m/15m/1h, the current candle is incomplete; for 8h/1d, both comparison bars are completed. Bar progress can influence the fast values, but contracts can still have different readings at the same time.

## Open interest

Open Interest is open quantity valued at the current price. OI Change percent uses the change in quantity relative to its historical quantity. Its dollar component values that quantity change at the current price. Therefore an increase in dollar Open Interest alone does not prove new positions were added: a price increase can raise the dollar value.

OI samples are collected periodically. The label describes an approximate observation interval; newly listed symbols and incomplete history can have no usable comparison. OI does not reveal which participant opened a position, leverage, deposits or future direction.

## Volatility, correlation and activity

Volatility is the **sample standard deviation** of open-to-close candle returns. It is not the average size of a candle and not the largest move. The timeframe label names the candle interval; a full buffer contains 20 candles.

BTC correlation compares paired returns over the chosen interval. Near zero means little measured linear association in that sample, not statistical independence or proof of a coin-specific cause. Short histories and incomplete pairs limit the result.

Ticks count aggregated exchange trade events, not users, orders or individual fills. RetailHeat relates that count to quote turnover; its numerator and denominator windows can differ. `*` indicates smoothing, not a participant classification. See [Reading the table](reading-the-table.md) for its thresholds and percentile.

Next: [Quick filters](quick-filters.md).
