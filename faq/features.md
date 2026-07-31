# Features and tools

What the screener, the alerts, the Charts page and the premium channels actually give you — and
what they do not.

### What can I filter on in the screener

Four tools, used together:

- **11 quick-filter chips** above the table: All, High Volume, OI Spike, Big Movers, High
  Funding, Accumulation, Squeeze, Breakout, Top Active 10, Top Gainers 1D, Top Losers 1D. One at
  a time. Each has a fixed rule, listed in [quick filters](../screener/quick-filters.md).
- **Sorting** on any of the 57 columns, using the caret button beside the header.
- **The search box**, for narrowing to a ticker or a handful of them.
- **Favourites**, to pin the coins you are actually watching to the top.

The method for combining them into a real screen is in
[build your own filters](../screener/build-your-own-filters.md).

### Can I save my own custom filter

No. There is no saved-filter or filter-builder feature. What persists in your browser is your
column layout, your density setting and your favourites — so in practice you rebuild a screen by
picking a chip and a sort, and that takes a couple of seconds.

### Can I screen or alert by market cap

No. Market cap does not exist anywhere in ErkeScan: not as a column, not as a filter, not as an
alert condition. Every metric here comes from futures market activity — price, volume, open
interest, funding, trade flow.

### Is there an ETH correlation column

No. Correlation is measured against **BTC only**, on five windows (5m, 15m, 1h, 8h, 1d). BTC
Corr 1h is visible by default; the rest are in the column picker.

### How do I sort a column

Click the **small caret button** beside the header label. The label itself is the drag handle
for reordering columns, so clicking it moves the column instead of sorting it. This is worth
learning early — the in-app tour text on this point is wrong.

### How many alerts can I create

**200 per account**, the same on every plan. Attempt number 201 returns "Alert limit reached
(max 200). Delete unused alerts to create new ones." Details in
[how alerts work](../alerts/how-alerts-work.md).

### Which metrics can I set alerts on

29 conditions in 7 groups:

| Group | Fields |
|---|---|
| Change | 5m, 15m, 1h, 8h, 24h |
| OI Change | 5m, 15m, 1h, 8h, 1d |
| Volume | 5m, 15m, 1h, 8h, 24h |
| VDelta | 5m, 15m, 1h, 8h, 1d |
| Volatility | 5m, 15m, 1h |
| Ticks | 5m, 15m, 1h |
| Others | Price, Open Interest, Funding Rate |

The Volatility, Ticks and VDelta groups — 11 conditions in total — sit behind a **Show advanced
fields** toggle that is collapsed by default.

Some screener columns cannot be alerted on at all: RVOL, BTC Correlation, the Change $ family,
Bar Vol Δ, and RetailHeat. If a column is not in the table above, you cannot build an alert on
it.

{% hint style="warning" %}
Avoid **Change (8H)**. That condition reads a different value from the column of the same name —
one that sits within a fraction of a percent of zero nearly all the time — so the alert will
effectively never fire. Use Change (1H) or Change (24h).
{% endhint %}

### Can I choose the chart timeframe in the alert message

No. Every alert message carries a **15-minute** chart image; there is no per-alert choice. If the
image cannot be fetched, the alert still arrives as text.

### Can I duplicate an existing alert

Not reliably — build the second one the same way you built the first. It takes about the same
time and you will not end up with a half-filled form.

### Do my columns and favourites follow me to another device

No. Column visibility, column order, density and favourites are stored in the browser you set
them in. A different browser, a different machine or a cleared cache starts from the default
19-column layout with no favourites.

### What is on the Charts page

Five panels, fed by the same live data as the screener: a trader summary strip, a price rotation
chart, an open-interest rotation chart, a return-distribution histogram, and a funding table of
the twelve coins with the largest absolute funding rate.

You pick one of four cohorts — **Top Gainers 24h, Top Losers 24h, Top Volume 24h, Top Active
5m** — and one of five windows: 1H, 4H, 1D, 1W, 1M, with 4H as the default. Six symbols are
plotted per chart by default.

Every cohort and the funding table apply the same liquidity floor as the screener chips:
$500,000 of hourly volume. Details in [charts](../screener/charts.md).

### Can I look at a single coin's chart

Two ways. Clicking a ticker in the table opens a TradingView chart for that Binance perpetual in
a modal, which you close with Escape, the ×, or a click outside. Or open
`app.erkescan.com/symbols/<TICKER>` for a full page — an active subscription is required, and
there is no browsable index of symbols. See [coin view](../screener/coin-view.md).

### Do stocks and commodities really appear in a crypto screener

Yes, because Binance lists them as perpetual futures. Roughly 140 of the contracts are tokenized
equities and commodities — TSLA, NVDA, SPY, gold, crude oil, natural gas and similar — and they
carry a **STOCK** or **COMMODITY** badge next to the ticker.

They behave differently from coins: different sessions, different liquidity patterns. Filter them
out or in deliberately rather than by accident.

### Does ErkeScan cover spot markets or other exchanges

No. Binance USDT-margined perpetuals only. See
[data and coverage](../reference/data-and-coverage.md).

### What do I get besides the screener

Custom Telegram alerts, the Charts page, the premium signal strategies with their Telegram
delivery, and access to the private community. All of it is included in every plan — see
[premium overview](../premium/overview.md).

**Next:** [Technical questions](technical.md)
