# Data & coverage

The screener and custom alerts are organised around supported **USDT-quoted perpetual futures**, with Binance futures as the primary market universe. This is a derivatives view, not a spot-market directory. Do not assume that an identically named instrument on another venue has the same price, funding or volume.

## Which instruments are included

The symbol universe is refreshed from exchange data and changes with listings, delistings and data availability. Use the current application list instead of a fixed contract count. The screener excludes USDC-quoted rows and dated contracts from this USDT perpetual view.

Some supported derivatives may reference equities, indices or commodities. **STOCK / АКЦИЯ** and **COMMODITY / ТОВАР** are classification badges. Such a label does not establish that the instrument is a tokenized share, confers shareholder rights or represents ownership of the underlying asset. Check the exchange's instrument specification. Sector badges such as AI or Meme are categories, not trading guarantees. Classification availability can lag the trading data; a missing badge does not change the contract specification.

## Freshness has several stages

The service receives trades, prices, candles, funding and OI on different schedules. It combines available inputs into snapshots. The browser uses a live stream when available and can fall back to snapshot polling. A complete snapshot does not mean every underlying metric was measured at the same instant.

Alert scheduling reads shared market data independently of your browser and passes matches to a delivery queue. These are separate stages; a data refresh interval is not an alert latency promise. The screen and a Telegram message can legitimately describe different observation times.

Read the connection indicator and any stale-data warning. When fresh inputs are unavailable, the service can retain a previous usable snapshot or leave individual values missing. **—** means unavailable, not zero. Do not infer live market availability solely from a rendered row or chart.

## Windows determine meaning

| Metric family | What its window means |
| --- | --- |
| Change and Change$ 5m / 15m / 1h / 8h | Rolling comparisons using stored observations or available candle references; the reference time can be approximate |
| Change / Change$ / Volume 24h | Rolling exchange-ticker window, not a calendar day |
| Volume / VDelta 5m | Last completed five-minute candle |
| Volume / VDelta 15m / 1h | Last 3 / 12 completed five-minute candles, stepping on candle closes |
| Volume / VDelta 8h | Last completed eight-hour candle |
| VDelta 1d | Last completed daily candle; different from rolling Volume 24h |
| RVOL 5m / 15m / 8h / 1d | Completed-candle turnover relative to a historical baseline |
| RVOL 1h | Trailing closed-five-minute turnover with a baseline from the hourly series; approximate |
| Bar Vol Δ 5m / 15m / 1h | Current unfinished candle versus a previous completed candle |
| Bar Vol Δ 8h / 1d | Two completed candles |
| Volatility / BTC correlation | Candle-return statistics over a buffer of 20 candles at the named interval; partial history can reduce coverage |
| Ticks | Aggregate trade-event counts over trailing wall-clock windows |
| OI Change | Comparisons with periodic historical OI samples; approximate lookbacks |

Completed-candle metrics normally hold between closes. Forming-candle volume is incomplete and usually small near the opening of a bar. Neither behaviour should be confused with rolling price changes.

## Units and interpretation

Prices and turnover are in the contract's quote currency, USDT in this view; `$` is the product's shorthand. A USDT notional is not a cash balance or an execution estimate. Volume measures turnover, not capital newly invested.

Percentage values use percent units. A move from 100 to 103 is +3%. A funding rate changing from 0.01% to 0.02% has risen by **0.01 percentage points**, or doubled in relative terms. Funding is shown per contract funding period, not annualised; settlement intervals can differ.

OI dollar value equals open quantity valued at the current price. OI Change % compares quantities, and its dollar companion values the quantity difference at the current price. Neither identifies deposits, leverage or which side initiated positions. VDelta identifies the taker-side turnover difference, not net long positions. Ticks are aggregated events, not unique people or individual executions.

RetailHeat relates event count to turnover, with primary and smoothed paths. Its inputs can use different windows, so it is not an exact inverse average trade size or a classification of retail versus institutional traders.

## Compare like with like

When checking another source, match venue, full contract, quote currency, price type, metric definition, window and timestamp. External TradingView or Coinglass charts may use different market mappings or aggregated indicators. A backend fallback does not turn this into a user-selectable multi-exchange screener; data provenance matters when exact venue identity is material.

Detailed definitions: [Column reference](../screener/column-reference.md), [Alert condition reference](../alerts/create-an-alert.md), [Glossary](../glossary.md).
