# ErkeScan

ErkeScan is a live screener for Binance USDT-margined perpetual futures.

It puts price, volume, order flow, open interest, funding and volatility for roughly 670 contracts on one sortable screen.

You decide what to watch, filter it down, and set alerts that reach you in Telegram.

It is built for active futures traders who want to see where activity is concentrated across the whole market, not just on the two or three charts they happen to have open.

{% hint style="info" %}
ErkeScan is a paid product. There is no free tier and no trial. A signed-in account without an active subscription can reach the app, but the screener, the alerts page and the charts page show an upgrade panel instead of data.

Prices are $200 for one month, $468 for three months and $868 for twelve. The three plans differ only in length and price — every plan includes every feature.
{% endhint %}

## What you get

### The screener

The main screen, at **Screener**. One row per contract, updating continuously, with 57 columns you can switch on and off. The column picker sorts them into 12 groups: **Core**, **Change %**, **Change $**, **Volume**, **RVOL**, **VDelta**, **Bar Vol Δ $**, **Bar Vol Δ %**, **OI Change**, **Volatility**, **Ticks** and **BTC Corr**.

Nineteen columns are shown by default. You switch the rest on and drag the headers into the order you want. To sort, you click the small caret button beside a header — the header label itself is the drag handle, not a sort button.

Eleven **quick filters** sit above the table: All, High Volume, OI Spike, Big Movers, High Funding, Accumulation, Squeeze, Breakout, Top Active 10, Top Gainers 1D, Top Losers 1D. One click narrows ~670 rows to the handful that meet a specific numeric rule. You can also star contracts into a favourites block that stays pinned above everything else; that list lives in your browser, so it does not follow you to another device.

→ [Tour of the screener](screener/tour.md) · [Column reference](screener/column-reference.md) · [Quick filters](screener/quick-filters.md)

### Custom alerts

You build your own conditions on 29 numeric fields in seven groups — Change, OI Change, Volatility, Ticks, VDelta, Volume, and Others (price, funding rate, open interest). When a condition is met, a message arrives in Telegram listing each condition that matched and the value that triggered it. A 15-minute chart image is attached when it can be fetched; if that fetch fails, the alert still arrives as plain text.

After an alert fires on a contract, that same alert stays quiet on that same contract for a cooldown period, so one condition cannot flood your chat. It can still fire on a different contract immediately.

The limit is **200 alerts per account**, and it is the same on every plan.

Telegram delivery needs your Telegram account linked to your ErkeScan account. The link is created when you complete a payment inside **@erkescan_premium_bot**, when you redeem a premium-signal link, or when a Discord link is confirmed in that bot.

→ [How alerts work](alerts/how-alerts-work.md) · [Create an alert](alerts/create-an-alert.md) · [Connect Telegram](getting-started/connect-integrations.md)

### The charts page

**Charts** takes the same feed and shows it as pictures instead of rows. Five panels: a trader summary strip, a price-rotation chart, an open-interest rotation chart, a return-distribution histogram, and a funding table listing the 12 contracts with the largest funding rate in either direction.

You pick one of four cohorts — Top Gainers · 24h, Top Losers · 24h, Top Volume · 24h, Top Active · 5m — and one of five time windows: 1H, 4H, 1D, 1W, 1M. 4H is the default. The cohorts and the funding table only consider contracts that clear the same liquidity floor the quick filters use, so thin markets never fill the picture.

→ [The charts page](screener/charts.md)

### Premium signal channels

The strategy pages under **Signals** are public: each one publishes its own record of completed signals. What your subscription unlocks is the live side — the **Entry**, **Stop**, **Target 1** and **Target 2** rows of a signal that is running right now. Without a subscription those four rows are blurred out and the contract is never named.

→ [Premium signals overview](premium/overview.md)

## What ErkeScan covers

The screener, the alerts engine and the charts page all read one feed: **Binance USDT-margined perpetual futures**.

That is roughly 670 contracts. About 140 of them are not coins — Binance lists tokenized stocks and commodities as perpetual contracts (TSLA, NVDA, SPY, gold, crude oil, natural gas and others), and they sit in the same table with the same columns. Most of them carry a **STOCK** or **COMMODITY** badge next to the ticker. The list is rebuilt from Binance about every 60 seconds, so new listings appear on their own and the exact count moves.

Contracts quoted in USDC and dated quarterly contracts are not included.

Three things people expect and will not find:

- **No market-cap data.** There is no market-cap column, no market-cap filter and no market-cap alert condition anywhere in the product.
- **No ETH correlation.** Correlation is measured against BTC only, on five windows (5m, 15m, 1h, 8h, 1d).
- **No spot markets.** Perpetual futures only.

→ [Data and coverage](reference/data-and-coverage.md)

## Start here

1. **[Create your account](getting-started/create-your-account.md)** — sign up at [app.erkescan.com/sign-up](https://app.erkescan.com/sign-up), and see exactly what an account without a subscription can and cannot reach.
2. **[Choose a plan](getting-started/choose-a-plan.md)** — Monthly, Quarterly or Annual. All three unlock the identical feature set; only the term length and the price differ.
3. **[Connect your integrations](getting-started/connect-integrations.md)** — get Telegram delivery working, and link Discord if you have community access.
4. **[Your first 15 minutes](getting-started/first-steps.md)** — a guided first session that ends with one working filter and one working alert.

## Links

| What | Where |
|---|---|
| Web app | [app.erkescan.com](https://app.erkescan.com) |
| Screener | [app.erkescan.com/screener](https://app.erkescan.com/screener) |
| Plans and prices | [app.erkescan.com/pricing](https://app.erkescan.com/pricing) |
| Sign up | [app.erkescan.com/sign-up](https://app.erkescan.com/sign-up) |
| Support (Telegram) | [@ErkeScanSupportbot](https://t.me/ErkeScanSupportbot) |
| Support (email) | support@erkescan.com |
| Public site | [erkescan.com](https://erkescan.com) |

{% hint style="warning" %}
Use `app.erkescan.com/pricing` for prices. The older `erkescan.com/pricing` address is switched off and returns an error page.
{% endhint %}

The **Contact us** button in the top right of every app page opens the same support bot as the Telegram link above. There is no chat widget on the website — support runs through Telegram and email.

→ [Support channels and what to include in a report](reference/support.md)

---

ErkeScan is a data tool. It shows you what the market is doing; the decision, the position size and the stop are yours. Nothing in this manual is financial advice, and no filter, column or signal is a guaranteed edge.

**Next:** [What ErkeScan is](what-is-erkescan.md)
