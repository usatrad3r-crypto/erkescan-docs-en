# What ErkeScan is

This page explains what the product actually does, where the numbers come from, and — just as importantly — what it does not do. Read it before you start clicking, so you know what you are looking at.

## The problem it solves

Binance lists roughly 670 USDT-margined [perpetual futures](glossary.md) contracts, and they all trade at once. You cannot hold 670 charts in your head, and by the time a move is obvious on a chart, the part you wanted is often already priced in.

The things that describe a move are not the price line. They are turnover, [relative volume](glossary.md), the direction of the order flow ([VDelta](glossary.md)), whether [open interest](glossary.md) is growing or unwinding, whether [funding](glossary.md) is punishing one side, and how many separate trades the turnover is split across.

Every one of those numbers exists on the exchange. The problem is that they live in different endpoints, on different time windows, for hundreds of symbols, and nobody is going to assemble them by hand every five minutes.

ErkeScan assembles them. It is one table, one row per contract, with every metric on a stated window, so you can sort ~670 contracts by the number that matters to the question you are asking and be left with five rows to look at.

{% hint style="info" %}
No metric or filter here predicts anything. What the screener gives you is a shorter list to investigate. The Accumulation filter, for example, encodes a common reading — open interest up more than 3% over the past hour, relative volume above 1.5, and price moved less than 1% in that hour — but that reading is a heuristic, not a forecast, and it is wrong often enough to need a stop.
{% endhint %}

## How the data reaches your screen

### One exchange, one feed

Everything in the screener, the alerts engine and the charts page comes from **Binance USDT-margined perpetual futures**, and nothing else.

The tradable list is rebuilt from Binance about every 60 seconds, so newly listed contracts appear on their own and delisted ones drop out. Only symbols quoted in USDT are kept: USDC-quoted pairs and dated quarterly contracts (the ones with an expiry in the name) never reach your table.

Roughly 140 of those contracts are not coins. Binance lists tokenized stocks and commodities as perpetuals, and they arrive through the same pipe with the same columns; most of them show a **STOCK** or **COMMODITY** badge beside the ticker.

### From exchange to table

1. Candles for the 5m, 15m and 1h intervals stream in over a live WebSocket connection. The 8h and 1d candles are fetched over REST once per bar, shortly after the bar closes, and then stay fixed until the next one.
2. Trade events stream in continuously and are counted into 5-second buckets. These are Binance *aggregated* trades — fills from one taker order at one price arrive as a single event — and they are what feeds the Ticks columns and the RetailHeat column.
3. Funding is refreshed about hourly, and open interest for the whole universe about every 5 minutes.
4. Twenty candles are retained per interval per contract. Everything derived — relative volume, volatility, BTC correlation — is computed from those buffers. This is why a column's name is not its window: "Volatility 5m" is the spread of twenty 5-minute candles, about 100 minutes, not the last five. The [column reference](screener/column-reference.md) states the true window of every metric.
5. One merge pass recomputes the whole snapshot. It runs **at most once every ~2 seconds, and only when new data has actually arrived** from the exchange. There is no fixed heartbeat, so quiet periods produce fewer updates.
6. Your browser receives finished snapshots over a live stream. If that stream is not available, the page falls back to fetching a fresh snapshot every 3 seconds instead — you keep the data either way.
7. The alerts engine reads the same snapshots on its own cycle, roughly every 5 seconds, independently of whether your browser is open.

### When something upstream breaks

Missing data is shown as missing. If a candle feed goes stale or a value never arrived, the cell renders a dash (`—`) — the product does not fabricate a `0.00` to fill the gap, and dashes always sort to the bottom of the table on both ascending and descending sorts.

A contract missing its 5m or 15m candles is withheld from the table entirely rather than shown half-empty.

The **connection indicator** in the header has six states: connected, polling, reconnecting, loading, stale and error. Stale means no accepted snapshot for more than 30 seconds, or that the newest price update across the entire universe has not advanced for more than 60 seconds. Error means more than 120 seconds with no accepted snapshot.

{% hint style="warning" %}
In the stale and error states a warning strip appears above the table. It is there because prices can freeze while the page still looks alive. Never size a trade off a frozen quote — refresh and confirm on the exchange first.
{% endhint %}

→ [Reading the table](screener/reading-the-table.md) · [Data and coverage](reference/data-and-coverage.md)

## What ErkeScan is not

**It is not a trading bot or an auto-trader.** Nothing in the product connects to your exchange account, places an order, sets a stop or closes a position. There is no execution path anywhere in it. Every trade you take from something you saw here, you place yourself on the exchange.

**It is not a multi-exchange aggregator.** The screener universe, the 29 alert conditions and the charts page are Binance USDT perpetuals only. If a Binance REST endpoint stops answering, a backup venue can temporarily stand in for those specific REST values so the table keeps updating — but two venues are never mixed inside one number, and the order-flow columns go to a dash rather than guess when the backup does not supply what they need.

**It is not a signals-only service.** The strategy pages under **Signals** are part of what you get, and your subscription is what reveals the live levels on them — but they are not the product. The product is the screener you drive yourself; the signals sit beside it.

**It is not a fundamentals tool.** There is no market-cap data anywhere — no column, no filter, no alert condition. There is no ETH correlation either; correlation is measured against BTC only, on 5m, 15m, 1h, 8h and 1d windows. If your process starts with "show me mid-caps under $500M", this is not the tool for that step.

**It is not advice.** ErkeScan reports what the market did. It does not tell you what to do, and no number on the screen carries a guarantee.

## Who gets the most out of it

You will get a lot out of ErkeScan if you:

- **trade Binance USDT perpetuals** on intraday to multi-day horizons, and want the whole board rather than a watchlist of ten favourites;
- **work from flow and positioning** — volume, order-flow delta, open-interest change and funding — rather than from indicators alone;
- **want to be told, not to watch** — up to 200 custom alerts on 29 fields, delivered to Telegram, with a 15-minute chart image attached whenever it can be fetched;
- **like reading numbers.** The table rewards someone who will learn what each window actually measures, because the windows are deliberately not uniform and the difference matters.

You will get less out of it if you trade spot only, trade on an exchange other than Binance, hold positions for months, or want something that trades for you.

## Languages

The interface is available in **English** and **Russian**. Your language on a first visit is taken from your browser: Russian if your browser's top language starts with `ru`, English otherwise. You change it with the **EN | RU** pill in the top right of the header, on any page.

All 57 column headers and all 57 column tooltips have a Russian version, as do the quick-filter chips and the rest of the screener. Four chips in the column picker — the 8h and 1d entries under **Bar Vol Δ $** and **Bar Vol Δ %** — stay in English for Russian users; the matching table headers are translated normally.

Switching language does not change the URL of an app page. There is no separate Russian address to bookmark or send to someone — each person sets their own language, and the choice is remembered in that browser for a year.

App pages are also excluded from search-engine indexing, so you will not find your screener or billing page through a web search. Use the links in this manual or the app's own navigation.

---

**Next:** [Create your account](getting-started/create-your-account.md)
