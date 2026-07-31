# Coin view and the symbol page

There are two ways to look at a single coin's price action inside ErkeScan: a chart that opens over the table, and a full page for that symbol. This page covers both, and what each is good for.

## The chart modal

On desktop, click the **ticker text** inside the Symbol cell — for example the word `BTC`. A chart opens in a panel over the table.

- It is a **TradingView** chart of the **Binance perpetual** for that coin, opened on the **15-minute** interval, in dark theme.
- Close it with **Escape**, the **×** button, or a click anywhere on the dimmed background.
- **Full Page →** opens the coin's own symbol page in a new browser tab, leaving your screener exactly as you left it.

Only the ticker text opens the chart. The rest of the row does nothing when clicked, and the favourite checkbox beside the ticker is a separate control — ticking it stars the coin and does not open anything.

Because the chart is the Binance perpetual, it is the same contract the screener's numbers describe. What you see on the chart and what the row says are about the same market.

{% hint style="info" %}
The chart is for price structure — where the move sits relative to ranges, highs and prior reactions. It does not carry any of the screener's metrics. For [RVOL](../glossary.md), [VDelta](../glossary.md), [open interest](../glossary.md), [funding](../glossary.md) and the rest, go back to the row. The two together are the point; see [From screen to trade](from-screen-to-trade.md).
{% endhint %}

## On mobile

Below 768 pixels the table is replaced by cards, and the whole card is a link: tapping it navigates to that coin's symbol page. The star button in the card's top-right corner is excluded — tapping the star adds or removes a favourite without navigating away.

## The symbol page

Each coin has its own page at `/symbols/<SYMBOL>`, reached from **Full Page →** in the modal, from a tap on a mobile card, or by typing the URL.

**What it needs.** An active subscription. A signed-in user without one sees the subscription screen instead of the chart.

**What it accepts.** The ticker in the URL is normalised, so several spellings resolve to the same page — `trb`, `TRB`, `TRB-USDT` and `BTCUSDT.P`-style forms all land correctly. Empty or nonsense values, and the bare word `USDT`, return a 404 immediately.

**What it shows.** A TradingView chart for that symbol, plus a breadcrumb to get back.

**How it validates.** The page checks your ticker against the live Binance futures universe and returns a 404 for symbols that are not in it. That check **fails open**: if the universe feed is unreachable at that moment, the page renders the chart anyway. So a rendered chart is not by itself proof that a contract is currently listed.

{% hint style="warning" %}
There is **no `/symbols` index page**. Visiting `/symbols` on its own returns a 404. The symbol page is something you arrive at from a row, not a directory you browse. To find a coin, use the screener's **Search...** box.
{% endhint %}

## Which one to use

| Situation | Use |
|---|---|
| Quick structural check while working the table | The chart modal — it closes with Escape and keeps your place |
| Studying one coin for a while, drawing on the chart | The symbol page in its own tab |
| Comparing several coins over a window | Neither — use [Charts](charts.md) |

**Next:** [The Charts page](charts.md) — the five panels that put a coin in the context of its cohort.
