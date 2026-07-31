# The Charts page

The screener answers "what is unusual about this coin right now". **Charts** answers "what has a group of coins been doing over the last few hours or weeks". It is the context layer, and it is fed by the same live exchange data as the screener.

**Where:** **Charts** in the top navigation, at `/charts`. It requires an **active subscription** — a signed-in user without one sees the subscription screen instead of the charts.

## The controls

Two choices drive everything on the page.

**The cohort** — which group of coins is plotted:

| Cohort | Members |
|---|---|
| **Top Gainers · 24h** | The biggest risers over the rolling 24 hours |
| **Top Losers · 24h** | The biggest fallers over the rolling 24 hours |
| **Top Volume · 24h** | The largest turnover over the rolling 24 hours |
| **Top Active · 5m** | The most trading activity over the trailing five minutes |

**The time window** — how far back the charts look. The options are **1H**, **4H**, **1D**, **1W** and **1M**, and **4H is the default**.

The window also decides the resolution, which matters when you are judging how meaningful a wiggle is:

| Window | Built from |
|---|---|
| 1H | 1-minute candles |
| 4H | 5-minute candles |
| 1D | 15-minute candles |
| 1W | 1-hour candles |
| 1M | 4-hour candles |

So a 1M chart is a coarse shape and a 1H chart is close to raw tape. There is also a download button for saving a chart.

{% hint style="info" %}
Every cohort, and the funding table, uses the **same $500,000-of-volume-in-the-last-hour gate as the screener's top-N chips**. That is deliberate: the cohorts contain coins you could plausibly trade, not whatever moved most on no turnover. Each chart plots **six symbols** by default.
{% endhint %}

## The panels

### Trader summary

A compact summary strip at the top of the page. Treat it as orientation for what follows, not as a signal.

### Price rotation

The main chart: each coin in the selected cohort is drawn as its own line across the chosen window, so you can compare them directly instead of flipping between single charts.

What to look for:

- **Fan or bundle?** Lines spreading apart mean the cohort is differentiating and stock-picking within it is worth something. Lines moving as one bundle mean you are looking at a single market move wearing several tickers — check **BTC CORR (1h)** back on the screener to confirm.
- **Who turned first?** The line that changed direction before the others is the cohort's leader. Leaders and laggards behave differently on the next leg.
- **Where in the window did it happen?** A cohort that is +8% because of one candle four hours ago is a very different market than one grinding up all window.

### Open-interest rotation

The same chart shape for [open interest](../glossary.md) instead of price: one line per cohort member across the window.

One resolution detail: at the **1H** window the open-interest chart is built from 5-minute samples rather than the 1-minute candles the price chart uses, so it is the coarser of the two. From **4H** upwards both charts use the same resolution.

Read it *against* the price chart. That pairing is the whole reason both panels exist:

- Price up, open interest up → new positions opening into the move.
- Price up, open interest down → positions closing; frequently short covering, frequently late.
- Price flat, open interest up → somebody is building while nothing appears to happen.
- Price down, open interest down → an unwind rather than fresh selling.

### Return buckets

A histogram of the cohort's returns over the chosen window: returns are grouped into bands and the bars show how many of the cohort landed in each.

It answers one question the line charts cannot: **is this broad or narrow?** A cluster of bars sitting to one side is a cohort moving together. A single tall bar at one extreme with everything else near zero is one coin doing something and nine coins doing nothing — which is worth knowing before you conclude "the sector is running".

### Funding table

The **twelve coins with the most extreme funding rate by absolute value**, among coins passing the same liquidity gate. Rows with no usable funding number are left out.

The value is a percent per [funding](../glossary.md) period exactly as Binance publishes it for that contract — the same number the screener shows in **FUNDING RATE**. Positive means longs are paying shorts; negative means shorts are paying longs.

Use it as a positioning board: it is the fastest way to see whether one coin's stretched funding is genuinely unusual or whether the entire liquid board is leaning the same way.

## Using Charts with the screener

The two pages are built for a loop, not for browsing:

1. **Find a candidate in the screener** using a chip and a sort — see [Recipes](recipes.md).
2. **Open Charts** and select the cohort that candidate belongs to, at the window that matches your horizon.
3. **Ask the three context questions:** is my coin leading or following (price rotation), is the whole cohort doing this (return buckets), and is my positioning read specific or market-wide (funding table)?
4. **Go back to the screener row** to check the fine detail — RVOL, VDelta, open-interest change — now that you know whether you are looking at a coin or at market beta.

{% hint style="warning" %}
Cohort membership is computed from the current data, so it changes as the market changes. A coin can leave Top Gainers · 24h simply because two others overtook it, and the chart will silently be about a slightly different group the next time you open it. Nothing on this page is a signal, a recommendation or a forecast — it is a picture of what already happened.
{% endhint %}

**Next:** [Troubleshooting](troubleshooting.md) — empty tables, dashes, warning strips, and the settings that reset themselves.
