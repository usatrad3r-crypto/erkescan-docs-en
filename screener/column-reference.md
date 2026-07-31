# Column reference

This is the dictionary. Every column in the screener, what it measures, in what unit, over exactly what window, and one line on how to read it.

Two rules make this page worth reading rather than skimming. First, columns in the same family do **not** all use the same kind of window — "Volume 1h" and "Volume 8h" are built differently. Second, a label naming a timeframe usually names the *candle size*, not the look-back. Where that matters, it is spelled out below, and the worst offenders are collected in [Traps worth knowing](#traps-worth-knowing) at the end.

There are **57 columns in 12 groups**, and all 57 are available in the **Columns** panel — nothing is withheld. **19 are visible by default:**

Symbol · Trend (4h) · Price · RVOL 5m · Change 5m · Change 24h · Change$ 5m · Volume 5m · Bar Vol Δ% 5m · Ticks 5m · RetailHeat (5m) · VDelta 5m · Volatility 15m · OI Change 5m · OI Change 1h · Funding Rate · BTC Corr 1h · Volume 1h · VDelta 1h

Headers below are written exactly as they appear on the table header row. The column picker sometimes uses a shorter label for the same column; where the two differ it is noted.

All values describe Binance USDT-margined [perpetual futures](../glossary.md). Every dollar figure is in the quote currency, USDT. Volume, VDelta, Bar Vol Δ$, Open Interest and OI Change are **turnover or position value in dollars**, never coin units; Price and Change$ are **dollars per coin**. Terms like funding rate, open interest, volume delta and RVOL are also defined in the [glossary](../glossary.md).

---

## Core

The five columns that identify a row and price it.

| Header | What it means | Unit | Window | How to read it |
|---|---|---|---|---|
| **SYMBOL** | The contract: coin icon, ticker, an optional sector or asset-class badge, and the favourite star | — | — | Sorts alphabetically rather than numerically. Click the ticker to open its chart; click the star to pin it to the top block. |
| **TREND** (picker: *Trend (4h)*) | A miniature price line built in your browser | — | Up to 4 hours; about 100 minutes on a freshly opened tab | Shape and direction only. Green if the last sample is at or above the first, red otherwise. Cannot be sorted. |
| **PRICE** | Last traded price | USD | Live — updates with every tick received | This is the last **traded** price, not the mark price. The header tooltip saying "mark price" is wrong. |
| **FUNDING RATE** | The current funding rate the exchange publishes for that contract | Percent **per funding period** | Refreshed once an hour | Positive means longs are paying shorts (crowded longs); negative means shorts are paying longs. `0.010` on screen is 0.01%. |
| **OPENINTEREST** (picker: *Open Interest*) | The dollar value of all open positions in that contract | USD | Refreshed every 5 minutes across the whole universe | Size of the field, not direction. Displayed without a sign. Pair it with OI Change to see whether positions are being built or closed. |

You can switch **Symbol** and **Trend** off in the **Columns** panel, but both are forced back on at the next page load. Treat hiding them as temporary. Full detail in [Make the screener yours](personalize.md).

{% hint style="warning" %}
The funding number is **per funding period exactly as the exchange publishes it** — it is not per hour, not per day and not annualised, and ErkeScan does not normalise it. Contracts do not all settle on the same schedule, so comparing raw funding between two contracts compares two different periods. Use it as a crowding indicator, not as a yield.
{% endhint %}

---

## Change %

Price change in percent. **These five columns do not share a window type** — two of them are rolling, two reset at a bar boundary, and one is a completed bar.

| Header | What it means | Unit | Window | How to read it |
|---|---|---|---|---|
| **CHANGE (5m)** | Move since the last 5-minute bar boundary | % | From the previous 5m close to the live price — **not** a rolling 5 minutes | At 12:00:10 this describes 10 seconds of market, not 5 minutes. It resets to near zero at every :00 / :05 / :10 and grows through the bar. |
| **CHANGE (15m)** | Move since the last 15-minute bar boundary | % | From the previous 15m close to the live price | Same behaviour as the 5m column, on a 15-minute clock. |
| **CHANGE (1h)** | A true rolling 60-minute change | % | The 5-minute close nearest to 60 minutes ago, compared with the live price | The most honest short-term change column. If no 5-minute candle within 15 minutes of the target exists, or fewer than 13 of them are held, it falls back to the 1-hour candle — and if that candle is itself more than 5 minutes stale, the cell shows a dash. |
| **CHANGE (8h)** | The last **completed** 8-hour bar, close to close | % | One finished 8h bar | Stable for the whole bar and up to 8 hours old at the end of it. It is not "the last 8 hours from now". |
| **CHANGE (24h)** | A true rolling 24-hour change | % | Live price against the price 24 hours ago, from the exchange's 24-hour ticker | A rolling window, **not** a calendar or UTC day. The 24-hour anchor refreshes every 60 seconds; the live side moves with every tick. |

---

## Change $

The same five labels as **Change %**, in dollars per coin instead of percent. Useful when a percentage flatters a very cheap coin.

**They are not simply the percent columns converted.** The 1h leg in particular is built from candles here, while the percent 1h leg is a true rolling window — see the row below and trap 8.

| Header | What it means | Unit | Window | How to read it |
|---|---|---|---|---|
| **CHANGE$ (5m)** | Absolute price move since the last 5m bar boundary | USD | Forming 5m candle close minus previous 5m close | Same bar-boundary behaviour as CHANGE (5m). |
| **CHANGE$ (15m)** | Absolute move since the last 15m bar boundary | USD | Forming 15m candle close minus previous 15m close | Same as above on a 15-minute clock. |
| **CHANGE$ (1h)** | Absolute move on the 1-hour candle series | USD | Forming 1h candle close minus previous 1h close | **Candle-based, not rolling** — unlike CHANGE (1h) in percent. The two 1h columns describe different windows. |
| **CHANGE$ (8h)** | The last completed 8h bar's move | USD | One finished 8h bar | The dollar sibling of CHANGE (8h). |
| **CHANGE$ (24h)** | Rolling 24-hour move | USD | Live price minus the price 24 hours ago | The dollar sibling of CHANGE (24h). |

---

## Volume

Dollar turnover. Always neutral in colour — volume has no direction. The five windows are built three different ways.

| Header | What it means | Unit | Window | How to read it |
|---|---|---|---|---|
| **VOLUME (5m)** | Turnover of the last **closed** 5-minute candle | USD | One finished 5m candle | Stable for the whole bar, which makes it comparable between symbols at any moment. |
| **VOLUME (15m)** | Turnover of the last **3 closed 5-minute candles** | USD | A trailing 15 minutes, excluding the bar in progress | It is a trailing sum of 5m candles, not "the 15-minute candle". It steps forward every 5 minutes. |
| **VOLUME (1h)** | Turnover of the last **12 closed 5-minute candles** | USD | A trailing 60 minutes, excluding the bar in progress | The practical liquidity column, and the one the chips use for their liquidity floor. Steps every 5 minutes. |
| **VOLUME (8h)** | Turnover of the last **closed** 8-hour candle | USD | One finished 8h candle | Refreshed once per bar, so it can be up to 8 hours old and will sit unchanged for hours. That is normal. |
| **VOLUME (24h)** | Rolling 24-hour turnover from the exchange's 24-hour ticker | USD | A true rolling 24 hours, refreshed every 60 seconds | The best single measure of how much market a contract really has. |

---

## RVOL

Relative volume: how the current volume compares with its own recent average. `1.00×` is a perfectly normal amount; `3.00×` is three times the usual. Each cell also draws a proportional bar that saturates at 4.00×.

**These five legs are not computed the same way.** Three of them are built from completed bars and are stable within the bar; one is built from the bar in progress and moves constantly.

| Header | What it means | Unit | Window | How to read it |
|---|---|---|---|---|
| **RVOL (5m)** | Last closed 5m candle against the average of the 18 candles before it | ratio (×) | One finished 5m candle vs. ~90 minutes of history | Stable within the bar. The dependable short-term "is this unusual?" column. |
| **RVOL (15m)** | The **current, unfinished** 15m candle against the average of the other retained 15m candles | ratio (×) | The bar in progress vs. ~5 hours of history | Reads near zero just after every 15-minute boundary and climbs through the bar. Only meaningful late in a bar, and never comparable between two symbols at different bar phases. |
| **RVOL (1h)** | The trailing-60-minute volume against a baseline drawn from the 1-hour candle buffer | ratio (×) | Numerator: the last 12 closed 5-minute candles. Baseline: the retained 1-hour candles | Re-steps every 5 minutes as each 5m candle closes. It is an approximation on both sides — see the trap below. |
| **RVOL (8h)** | Last closed 8h bar against the average of the bars before it | ratio (×) | One finished 8h bar vs. the retained 8h history | Updates once per bar. Good for "is today's session unusually busy". |
| **RVOL (1d)** | Last closed 1d bar against the average of the bars before it | ratio (×) | One finished daily bar vs. the retained daily history | Updates once per day. |

A dash appears rather than a number whenever an input is missing or the baseline is not positive — RVOL is never faked to `0.00`.

{% hint style="warning" %}
The **RVOL (1h)** header tooltip says "last CLOSED 1h candle vs the average of the ones before it". That description is wrong, and it is wrong in a way that matters: the numerator is the trailing 60 minutes assembled from 5-minute candles, while the baseline comes from the hourly candle buffer. Two different candle series are being divided, so the ratio is an approximation, and it re-steps every 5 minutes rather than holding still for an hour.
{% endhint %}

---

## VDelta

Volume delta: how much of a bar's turnover was net aggressive buying versus net aggressive selling. Positive means takers were net buyers, negative means net sellers. It is measured in **dollars, not coins**.

The windows mirror the Volume group exactly.

| Header | What it means | Unit | Window | How to read it |
|---|---|---|---|---|
| **VDELTA (5m)** | Net taker flow in the last closed 5m candle | USD, signed | One finished 5m candle | Compare with VOLUME (5m): the ratio of the two tells you how one-sided the bar was. |
| **VDELTA (15m)** | Net taker flow over the last 3 closed 5m candles | USD, signed | Trailing 15 minutes | Smooths out one violent candle. |
| **VDELTA (1h)** | Net taker flow over the last 12 closed 5m candles | USD, signed | Trailing 60 minutes | Persistent same-sign readings matter more than one large print. |
| **VDELTA (8h)** | Net taker flow in the last closed 8h candle | USD, signed | One finished 8h candle | Session-level pressure. Updates once per bar. |
| **VDELTA (1d)** | Net taker flow in the last closed 1d candle | USD, signed | One finished daily candle | Updates once per day. |

When a candle arrives without the taker-side breakdown, VDelta shows a dash rather than a number. It is never coerced to zero — that would fake a perfectly balanced bar, and it is never shown as a full negative, which would fake maximum selling.

---

## Bar Vol Δ $ and Bar Vol Δ %

Two groups of five, one in dollars and one in percent, measuring the change in turnover from one bar to the next. **The 5m/15m/1h legs and the 8h/1d legs measure fundamentally different things** — this is the single most misread part of the table.

### The 5m, 15m and 1h legs — bar progress

| Header | What it means | Unit | Window | How to read it |
|---|---|---|---|---|
| **BAR VOL Δ$ (5m)** / **BAR VOL Δ% (5m)** | How far the **current unfinished** 5m bar has filled versus the previous completed bar | USD / % | The bar in progress against the last finished bar | At the start of every 5-minute bar the Δ% leg sits near −100% for the entire market at once, climbing back toward 0 as the bar fills; the Δ$ leg starts at roughly minus the previous bar's whole turnover. |
| **BAR VOL Δ$ (15m)** / **BAR VOL Δ% (15m)** | Same, on the 15-minute clock | USD / % | Bar in progress vs. previous bar | Same sawtooth, on a 15-minute cycle. |
| **BAR VOL Δ$ (1h)** / **BAR VOL Δ% (1h)** | Same, on the hourly clock | USD / % | Bar in progress vs. previous bar | Same sawtooth, on an hourly cycle. |

These six are rendered in neutral grey rather than red/green precisely because their sign is a clock artefact, not a market event. Read them as "how far into this bar are we, relative to normal" — sorting them descending near the end of a bar finds symbols already trading above their previous bar's total.

### The 8h and 1d legs — real bar-over-bar change

| Header | What it means | Unit | Window | How to read it |
|---|---|---|---|---|
| **BAR VOL Δ$ (8h)** / **BAR VOL Δ% (8h)** | The last **completed** 8h bar's turnover against the bar before it | USD / % | Two finished bars | A genuine change in turnover between sessions. Coloured green/red because the sign means something. |
| **BAR VOL Δ$ (1d)** / **BAR VOL Δ% (1d)** | The last completed daily bar against the day before | USD / % | Two finished bars | Day-over-day turnover expansion or contraction. |

{% hint style="info" %}
In the **Columns** panel these four are labelled `Vol Δ$ 8h`, `Vol Δ$ 1d`, `Vol Δ% 8h` and `Vol Δ% 1d` — without the "Bar" prefix the table header uses, and in English even when the interface is set to Russian. Same columns, two labels.
{% endhint %}

---

## OI Change

Change in open interest — whether positions are being opened or closed. Each cell shows the dollar change followed by the percentage change in smaller dimmed text, for example `$1.20M (3.41%)`.

Open interest is sampled every 5 minutes, so **these windows are elastic**, not exact.

| Header | What it means | Unit | Actual window | How to read it |
|---|---|---|---|---|
| **OI CHANGE (5m)** | Change in open positions over roughly the last 5 minutes | USD and % | Anywhere from about 2.5 to 10.5 minutes | Fast build-ups and unwinds. Treat the timeframe as approximate. |
| **OI CHANGE (15m)** | Same over roughly 15 minutes | USD and % | About 7.5 to 20.5 minutes | — |
| **OI CHANGE (1h)** | Same over roughly an hour | USD and % | About 30 to 65 minutes | The leg behind the **OI Spike** and **Accumulation** chips. Rising OI with a flat price is the classic "positions being built" read; falling OI during a sharp move suggests positions being closed out. |
| **OI CHANGE (8h)** | Same over roughly 8 hours | USD and % | About 4 to 8 hours | Session-level positioning. |
| **OI CHANGE (1d)** | Same over roughly a day | USD and % | About 12 to 24 hours | Daily positioning. |

Both legs are emptied to a dash rather than shown as zero when there is not enough history — after a restart, for example. The percentage leg alone can be missing while the dollar leg is real, which happens when the starting open interest was exactly zero.

---

## Volatility

How much price moves inside each candle, on average. Always neutral in colour.

**The label names the candle size, not the look-back.** All three are computed over the full retained buffer of 20 candles.

| Header | What it means | Unit | Actual look-back | How to read it |
|---|---|---|---|---|
| **VOLATILITY (5m)** | Standard deviation of open-to-close moves across the retained 5-minute candles | % | About **100 minutes** | The compression / expansion measure on a comparable horizon to the other 5-minute columns. |
| **VOLATILITY (15m)** | Same, on 15-minute candles | % | About **5 hours** | A calmer, medium-horizon read. |
| **VOLATILITY (1h)** | Same, on hourly candles | % | About **20 hours** | Nearly a full day of context — do not read it as "volatility in the last hour". |

Low volatility is not automatically bullish or bearish; it describes a quiet market, which can precede a move or simply continue being quiet.

---

## Ticks (and RetailHeat)

This group has four columns: three trade-activity counts and the derived RetailHeat.

| Header | What it means | Unit | Window | How to read it |
|---|---|---|---|---|
| **TICKS (5m)** | Number of aggregated trade events | count | A true rolling wall-clock 5 minutes, in 5-second steps | Attention and participation, independent of size. |
| **TICKS (15m)** | Same over 15 minutes | count | Rolling 15 minutes | — |
| **TICKS (1h)** | Same over an hour | count | Rolling 60 minutes | Compare with TICKS (5m) to see whether activity is accelerating. |
| **RETAILHEAT (5m)** | Aggregated trade events per $1M of 5-minute volume — in effect the inverse of average trade size | events per $1M | Numerator: rolling last 5 minutes. Denominator: the last closed 5-minute candle, in dollars | High = many small trades per dollar, i.e. fragmented, retail-shaped flow. Low = fewer, larger trades, i.e. blocky flow. Shown as `value (pNN)`, where pNN is its percentile among symbols with a value. |

{% hint style="info" %}
A "tick" here is an **aggregated trade event**: every fill of one taker order at one price level is bundled into a single event. The count is therefore systematically lower than the raw number of trades, and the header tooltip's "number of trades executed" is loose wording. It is still a perfectly good comparative measure — just do not treat it as an exact trade count.
{% endhint %}

If the trade feed goes silent for two minutes, all three Ticks columns show a dash rather than zero. A live-but-quiet symbol correctly shows `0`. RetailHeat inherits both properties, plus its own asterisk and dash rules — see [Reading the table](reading-the-table.md#the-asterisk-on-retailheat).

RetailHeat's numerator and denominator are both about five minutes long, but they are not the *same* five minutes: the numerator is a rolling wall-clock window, the denominator is the last completed candle. On thin candles the denominator switches to a smoothed one and the value is marked with an asterisk — see [Reading the table](reading-the-table.md#the-asterisk-on-retailheat).

---

## BTC Corr

How closely a symbol's returns have tracked BTC's. A correlation of `1.00` means they moved together, `0.00` means no linear relationship, `-1.00` means they moved opposite.

Each leg is computed over the last **20 candles of that interval**, matched candle by candle, so the look-back is far longer than the label suggests.

| Header | Unit | Actual look-back | How to read it |
|---|---|---|---|
| **BTC CORR (5m)** | Pearson r, −1 to +1 | About 100 minutes | Short-term coupling. Useful for spotting a coin that has decoupled in the last couple of hours. |
| **BTC CORR (15m)** | Pearson r | About 5 hours | — |
| **BTC CORR (1h)** | Pearson r | About 20 hours | The default-visible leg, and the sensible general-purpose one. |
| **BTC CORR (8h)** | Pearson r | About a week | Structural relationship rather than a mood. |
| **BTC CORR (1d)** | Pearson r | About 20 days | The longest available context. |

BTC itself is fixed at `1.00`. A dash appears when fewer than three usable candle pairs exist. Values are cached for roughly 30 seconds, so they do not move on every tick.

A high correlation means a BTC move will probably drag the coin with it — position sizing and stops should account for that. A low or negative correlation is not automatically an edge; it can just as easily mean the coin is illiquid and moving on its own noise. There is no ETH correlation column.

---

## Traps worth knowing

Every item here has cost somebody a bad decision. Read the list once.

### 1. Bar Vol Δ on 5m / 15m / 1h is bar progress, not a market move

Those six columns compare the **unfinished** bar with the previous completed one. Right after every bar boundary the whole market sits near −100% on the Δ% legs at once, then climbs back toward zero as the bar fills. Sorting them for "collapsing volume" at 12:00:20 just finds a clock, not a market. The **8h** and **1d** legs are different: they compare two finished bars and carry a real change in turnover, which is why only those two are coloured.

### 2. RVOL (1h) is not "the last closed 1-hour candle"

The numerator is a trailing 60-minute window built from 5-minute candles; the baseline comes from the hourly candle buffer. Because the two sides come from different candle series, the value is an approximation on both legs, and it re-steps every 5 minutes as each new 5-minute candle closes. The tooltip on that column describes something else — trust this page.

### 3. RVOL (15m) is the odd one out

It is the only RVOL leg built from the bar in progress. It reads near zero just after every 15-minute boundary and climbs through the bar, so two symbols at different points in the bar are not comparable. RVOL 5m, 8h and 1d are built from completed bars and do not have this problem; RVOL 1h is stable within a 5-minute step but carries the mixed-series caveat in trap 2.

### 4. Change 24h is rolling, not a calendar day

It compares the live price with the price exactly 24 hours ago. It is not a daily candle and it does not reset at midnight anywhere. The same field sits behind the **Top Gainers 1D** and **Top Losers 1D** chips, whose "1D" name disagrees with the **CHANGE (24h)** header above the column they rank on. One rolling-24-hour number, two names. Never read "1D" as "today".

### 5. Change 5m and 15m are not rolling windows either

They measure from the last bar boundary to now. Ten seconds after a boundary, "Change 5m" describes ten seconds. Only **CHANGE (1h)** and **CHANGE (24h)** are true rolling windows.

### 6. Funding is per funding period, and nothing normalises it

It is a percent per settlement period exactly as the exchange publishes it — not per hour, not per day, not annualised. Contracts that settle on different schedules are therefore not directly comparable, and no code anywhere in ErkeScan adjusts for that. It is also the only percent column shown to three decimals.

### 7. Volume 15m and 1h are trailing sums of 5-minute candles

They are not "the 15-minute candle" and "the hourly candle". They step forward every 5 minutes and always exclude the bar in progress. Volume 5m and 8h are single completed candles; Volume 24h is the exchange's rolling ticker.

### 8. The two "1h" change columns disagree by design

**CHANGE (1h)** in percent is a true rolling 60 minutes. **CHANGE$ (1h)** in dollars is candle-based. They will not agree, and neither is broken.

### 9. Volatility labels name the candle, not the window

Volatility 1h looks back roughly 20 hours, Volatility 15m roughly 5 hours, Volatility 5m roughly 100 minutes. If you want a compression measure on the same horizon as the other 5-minute columns, use **VOLATILITY (5m)**.

### 10. OI Change windows are elastic

Open interest is sampled every five minutes, so "OI Change 5m" can actually span anywhere from about 2.5 to 10.5 minutes, and the longer legs stretch similarly. Treat them as approximate, never as an exact delta over an exact window.

### 11. The 8h and 1d columns update once per bar

Everything derived from 8-hour and daily candles is refreshed at the bar boundary and then held for the whole bar. A column that has not moved in three hours is behaving correctly, not stuck. The connection indicator, not a static 8h number, is what tells you the feed is alive.

### 12. A dash is not a zero

`—` means the value is unavailable. Rows showing a dash in the sorted column always sink to the bottom, in both sort directions. Nothing in the table fabricates `0.00` when a feed dies.

### 13. Not every column can be alerted on

Custom alerts cover Change, Funding Rate, Open Interest, OI Change, Price, Volatility, Ticks, VDelta and Volume. **RVOL, BTC Corr, Change$, Bar Vol Δ and RetailHeat have no alert condition** — you can screen on them, but you cannot be notified on them. See [How alerts work](../alerts/how-alerts-work.md).

### 14. An alert on Change (8H) does not match the column

The **CHANGE (8h)** column shows the last completed 8-hour bar. A custom alert on "Change (8H)" evaluates a different, near-zero internal field instead, so such an alert will almost never fire and will not agree with what you see in the table. Alert on 1h or 24h change instead.

### 15. Price is the last trade, not the mark price

The header tooltip says "mark price". It is wrong. The column shows the last traded price from the live ticker stream, falling back to the bid/ask midpoint and then to a 60-second refreshed ticker if no live tick has arrived. For liquidation levels and margin maths, use the exchange's own mark price.

---

## A closing note

Every column here is a measurement of what has already happened. None of them is a forecast, and no combination of them is a guarantee. Use them to shorten a list of ~670 contracts to the two or three worth a real chart, then make the trading decision yourself, with a stop and a position size you have chosen in advance.

---

**Next:** [Quick filters](quick-filters.md) — the 11 chips, the exact rule behind each, and when a chip is empty on purpose.
