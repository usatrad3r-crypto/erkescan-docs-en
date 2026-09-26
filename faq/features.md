# Features & tools

What the screener, the alerts, the Charts page and the premium channels actually give you — and what they do not.

### What can I filter on in the screener

Four tools, used together:

* **11 quick-filter chips** above the table: All, High Volume, OI Spike, Big Movers, High Funding, Accumulation, Squeeze, Breakout, Top Active 10, Top Gainers 1D, Top Losers 1D. One at a time. Each has a fixed rule, listed in [quick filters](../screener/quick-filters.md).
* **Sorting** on supported columns, using the caret button beside the header. Trend has no sort control.
* **The search box**, for finding a symbol by a case-insensitive substring; this is not a comma-separated multi-symbol selector.
* **Favourites**, to pin the coins you are actually watching to the top.

The method for combining them into a real screen is in [build your own filters](../screener/build-your-own-filters.md).

### Can I save my own custom filter

No. There is no saved-filter or filter-builder feature. What persists in your browser is your column layout, your density setting and your favourites — so in practice you rebuild a screen by picking a chip and a sort, and that takes a couple of seconds.

### Can I screen or alert by market cap

No. The screener and its custom-alert form do not provide a market-cap field: not as a column, not as a filter, not as an alert condition. Every metric here comes from futures market activity — price, volume, open interest, funding, trade flow.

### Is there an ETH correlation column

No. Correlation is measured against **BTC only**, on five windows (5m, 15m, 1h, 8h, 1d). BTC Corr 1h is visible by default; the rest are in the column picker.

### How do I sort a column

Click the **small caret button** beside the header label. The label itself is the drag handle for reordering columns, so clicking it moves the column instead of sorting it. Choose a quick filter first and then sort the remaining rows; selecting another filter resets the sort.

### How many alerts can I create

**200 per account**, the same on every plan. Attempt number 201 returns "Alert limit reached (max 200). Delete unused alerts to create new ones." Details in [how alerts work](../alerts/how-alerts-work.md).

### Which metrics can I set alerts on

29 conditions in 7 groups:

| Group      | Fields                             |
| ---------- | ---------------------------------- |
| Change     | 5m, 15m, 1h, 8h, 24h               |
| OI Change  | 5m, 15m, 1h, 8h, 1d                |
| Volume     | 5m, 15m, 1h, 8h, 24h               |
| VDelta     | 5m, 15m, 1h, 8h, 1d                |
| Volatility | 5m, 15m, 1h                        |
| Ticks      | 5m, 15m, 1h                        |
| Others     | Price, Open Interest, Funding Rate |

The Volatility, Ticks and VDelta groups — 11 conditions in total — sit behind a **Show advanced fields** toggle that is collapsed by default.

Some screener columns cannot be alerted on at all: RVOL, BTC Correlation, the Change $ family, Bar Vol Δ, and RetailHeat. If a column is not in the table above, you cannot build an alert on it.

{% hint style="warning" %}
**Change (8H)** uses rolling eight-hour percentage change. Like the other Change conditions, it is usable; choose a threshold appropriate to that window and check all conditions together.
{% endhint %}

### Can I choose the chart timeframe in the alert message

There is no per-alert timeframe choice. The service attempts to attach a **15-minute** chart; if the image is unavailable, a text-only message can still be delivered.

### Can I duplicate an existing alert

Yes. Use the alert's Copy action, then click the pencil on the new Draft card. This opens a new-alert form populated from the original. Check the name and conditions, then save the new alert; the original remains separate.

### Do my columns and favourites follow me to another device

No. Column visibility, column order, density and favourites are stored in the browser you set them in. A different browser, a different machine or cleared site data starts from the default 19-column layout with no favourites.

### What is on the Charts page

Five panels, fed by the same live data as the screener: a trader summary strip, a price rotation chart, an open-interest rotation chart, a return-distribution histogram, and a funding table of the twelve coins with the largest absolute funding rate.

You pick one of four cohorts — **Top Gainers 24h, Top Losers 24h, Top Volume 24h, Top Active 5m** — and one of five windows: 1H, 4H, 1D, 1W, 1M, with 4H as the default. Six symbols are plotted per chart by default.

Charts cohorts and the funding table require at least $500,000 of hourly turnover. The three top-ten screener filters also use this floor; it is not a rule shared by every quick filter. Details in [charts](../screener/charts.md).

### Can I look at a single coin's chart

Two ways. Clicking a ticker in the table opens a TradingView chart for that Binance perpetual in a modal, which you close with Escape, the ×, or a click outside. Or open `app.erkescan.com/symbols/<TICKER>` for a full page — an active subscription is required, and there is no browsable index of symbols. See [coin view](../screener/coin-view.md).

### Do stocks and commodities really appear in a crypto screener

Yes, because Binance lists them as perpetual futures. The available list can include equity- and commodity-related perpetuals, identified by a **STOCK** or **COMMODITY** badge where classified. The live contract list changes; these instruments do not give ownership of the underlying shares or commodities.

Check the exchange’s specification for each contract’s trading arrangements, price source and liquidity. Do not assume that a perpetual follows the trading hours of the underlying stock or commodity.

### Does ErkeScan cover spot markets or other exchanges

The screener and its custom alerts cover Binance USDT perpetuals. Other ErkeScan tools have their own sources and markets, including Bybit for Vertex copy trading. For the screener, see [data and coverage](../reference/data-and-coverage.md).

### What do I get besides the screener

Custom alerts, Charts and the [signal catalogue](../premium/overview.md) sit alongside [Copy trading](../copy-trading/overview.md), [Trading Journal](../journal/overview.md) and [GEX](../gex/overview.md). Each product explains its access and setup requirements. Community membership is a separate route; a normal subscription is not course enrolment.

**Next:** [Technical questions](technical.md)
