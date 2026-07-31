# Reading the table

The screener has a small visual language: a few colours, one number format per column type, a dash, an asterisk and a status dot. This page teaches all of it, so you can read a row at a glance instead of decoding it.

For what each individual column *measures*, go to the [Column reference](column-reference.md). This page is about how values are shown. Any term you do not recognise is in the [glossary](../glossary.md).

---

## Colour: green, red, grey — and nothing else

Colour in the table is **binary by sign**. Positive is green, negative is red, exactly zero is muted grey. That is the whole rule.

There is no heatmap, no colour intensity, no gradient that gets stronger as a number gets bigger. A +0.2% and a +25% are the same shade of green. If you want magnitude, read the number or sort the column.

### Which columns are coloured, and which never are

| Coloured green / red by sign | Always neutral |
|---|---|
| CHANGE (all five windows) | PRICE |
| CHANGE$ (all five windows) | VOLUME (all five windows) |
| VDELTA (all five windows) | VOLATILITY (5m / 15m / 1h) |
| FUNDING RATE | TICKS (5m / 15m / 1h) |
| OI CHANGE (all five windows) | OPENINTEREST |
| — | RETAILHEAT (5m) |
| BAR VOL Δ$ and Δ% on **8h** and **1d** | BAR VOL Δ$ and Δ% on **5m / 15m / 1h** |

Three columns follow their own rules rather than this one: **RVOL** and **BTC CORR**, both described just below, and **TREND**, which is a two-colour sparkline rather than a value.

That last table row is deliberate, not an oversight. The 5m/15m/1h Bar Vol columns measure how far the current unfinished bar has filled, so they sit deeply negative for the entire market at the start of every bar. Colouring them would paint the table red every five minutes for no market reason. The 8h and 1d versions compare two completed bars, so they are coloured.

### RVOL: a fixed five-step ladder

RVOL cells are the only place in the table with anything like intensity, and even there it is a fixed five-step ladder on the ratio itself, not a gradient:

| Value | How it looks |
|---|---|
| ≥ 2.00× | Green, bold |
| ≥ 1.50× | Green, semibold |
| ≥ 1.00× | Green, slightly dimmed |
| ≥ 0.50× | Muted grey |
| < 0.50× | Red |

Each RVOL cell also carries a small bar to the left of the number. It is purely proportional and saturates at **4.00×** — a 4× and a 40× draw the same full bar, so read the number for anything extreme. The bar is green from 1.00× upward and grey below.

### BTC Corr has its own four steps

| Value | How it looks |
|---|---|
| above +0.70 | Green |
| +0.30 to +0.70 | Normal body text |
| −0.30 to +0.30 | Muted grey |
| below −0.30 | Red |

### Gold means "active", never a value

The gold accent is reserved for interface state: the header of the column you are sorting by, active buttons, the favourites divider, the loading and polling indicators. No data value is ever gold.

When a value flips sign the cell fades between red and green rather than snapping. There is no flash or blink on update.

---

## How numbers are formatted

All numeric cells use a tabular monospace face, so digits line up vertically down a column and you can compare magnitudes by eye while scrolling.

### Money and large numbers (K / M / B)

Every dollar column is compacted the same way:

| Size | Rendered as | Example |
|---|---|---|
| ≥ 1,000,000,000 | `X.XXB` | `$1.24B` |
| ≥ 1,000,000 | `X.XXM` | `$8.51M` |
| ≥ 1,000 | `X.XXK` | `$412.30K` |
| ≥ 1 | two decimals | `$37.40` |
| between 0 and 1 | four significant digits | `$0.0004312` |
| exactly 0 | `0` | `$0` |

For dollar columns the minus sign goes **before** the dollar sign: `-$1.50M`.

### Price

The **PRICE** column uses its own ladder, so cheap coins keep their precision:

| Price | Decimals | Example |
|---|---|---|
| ≥ $1,000 | exactly 2, with thousands separators | `$64,215.30` |
| ≥ $1 | 2 to 4 | `$37.4021` |
| ≥ $0.01 | exactly 4 | `$0.0412` |
| below $0.01 | 4 significant digits | `$0.00005835` |
| exactly 0 | — | `$0` |

### Percentages

Percent columns show **2 decimals** — CHANGE, VOLATILITY, BAR VOL Δ%, and the percentage leg inside OI CHANGE.

**FUNDING RATE is the exception: 3 decimals.** It is the only three-decimal percent in the table, because funding numbers are small and the third decimal carries real information. `0.010` means 0.01%.

### Ratios, counts and correlations

| Column type | Format | Example |
|---|---|---|
| RVOL | ratio, 2 decimals, with `×` | `1.84×` |
| TICKS | whole number, thousands separators | `12,480` |
| BTC CORR | exactly 2 decimals, signed | `0.74`, `-0.31` |
| RETAILHEAT | 1 decimal, then a percentile in brackets | `149.8 (p87)` |

### OI Change: two numbers in one cell

The **OI CHANGE** columns pack two values into one cell: the dollar change, then the percentage change in smaller, dimmed type in brackets — for example `$1.20M (3.41%)`.

The colour of the cell follows the **percentage** leg, falling back to the sign of the dollar leg if the percentage is unavailable. Either leg can show its own dash independently of the other.

---

## The em dash "—"

A right-aligned, muted **—** means **no data**. It never means zero.

It appears when the value behind that cell is missing: the feed for that interval has gone stale, a required input was not delivered, or the calculation is undefined (for example a percentage change against a previous bar of zero).

This distinction is enforced deliberately upstream. When a data feed dies, the affected fields are emptied rather than frozen at their last value, so you see a dash instead of a stale number that looks alive. A dead feed will never produce a fabricated `0.00`.

Two consequences worth remembering:

- **Dashes sink.** Rows showing a dash in the column you sorted by go to the bottom in **both** ascending and descending order. They never masquerade as `0.00` at the top of an ascending sort.
- **A dash is not a quiet market.** A symbol genuinely trading nothing shows a real `0`; a symbol whose feed you cannot see shows `—`.

Whole rows with no usable data at all are moved into the faded block at the bottom of the table, described in [the tour](tour.md#the-three-row-sections).

---

## The asterisk on RetailHeat

**RETAILHEAT (5m)** counts aggregated trade events per $1M of 5-minute volume. Its denominator needs a meaningful amount of volume to be worth anything, so the column has three states. Which one you get depends on how much the **last closed 5-minute candle** traded, in US dollars:

| Last closed 5m candle traded | What you see | Meaning |
|---|---|---|
| ≥ $50,000 | `149.8 (p87)` in normal text | Primary value — trade events of the last rolling 5 minutes, divided by that candle's volume |
| $5,000 – $50,000 | `210.4* (p93)` dimmed, with an asterisk | Smoothed — the denominator becomes the average of the last 20 retained 5-minute candles (~100 minutes), because the last candle alone was too thin |
| below $5,000 | `—` | Not enough volume to compute anything honest |

The cell is also a dash whenever the trade-event count is missing, and in the middle band whenever the ~100-minute volume sum is unavailable. A missing feed is treated as no data, never as "zero trades".

Hovering an asterisked value on desktop shows the note "Smoothed over the ~100-min window (last 5m candle was thin)". That hint is a plain browser tooltip, so it does not appear on touch screens — the asterisk itself is your cue.

{% hint style="info" %}
Asterisked coins are deliberately excluded from the **Top Active 10**, **Top Gainers 1D** and **Top Losers 1D** chips. Those three chips only rank symbols with a primary-path value, so everything in them is measured on the same basis. A coin can therefore show a RetailHeat number in the table and still never appear in those chips.
{% endhint %}

### What `(pNN)` means

The bracketed number is the percentile rank of that symbol's RetailHeat among all symbols that produced a value on that data tick. `p87` means roughly 87% of the ranked symbols had a lower value.

Primary and smoothed values are ranked together in one pool, ties share the lower rank, and raw values are never capped — a single extreme outlier only adds "one more value above", it does not distort everyone else's rank.

---

## The badge next to the ticker

Some tickers carry a small badge. There are two different kinds, and no row is ever labelled "crypto".

| Badge | Colour | What it is |
|---|---|---|
| A sector or category word — `Layer-1`, `Meme`, `AI`, `TradFi`, and similar | Neutral grey | A category tag for that coin. Missing on symbols with no known tag, which is normal. |
| **STOCK** | Blue | A tokenized equity perpetual — a contract on a share, not a coin. |
| **COMMODITY** | Bronze | A tokenized commodity perpetual — gold, crude, natural gas and the like. |

The blue and bronze badges come from an exchange feed refreshed hourly, and they are best-effort: if that feed is briefly unavailable the badge falls back to the grey category tag, or disappears. Treat the badge as a helpful hint, not a guarantee — if a ticker looks like a share, it is a share.

The coin icon beside the ticker is loaded from third-party image sources. When none of them has an image you get a two-letter avatar instead. That is a cosmetic fallback, not a data problem.

---

## The 4-hour Trend sparkline

The **TREND** column draws a tiny line chart of recent price. It is a single flat colour: **green when the last price in the buffer is at or above the first, red otherwise**. There is no neutral state, no axis and no fill — it shows shape and direction, nothing more. It cannot be sorted.

The line is built in your browser, not on the server, and this has consequences worth knowing:

- Samples are taken **once every 30 seconds**, up to 480 of them — that is 4 hours once the buffer is full.
- On page load the buffer is seeded from the retained 5-minute closes, which is up to 20 candles, roughly **100 minutes**.
- So a tab you just opened shows about 100 minutes, and only reaches a true 4-hour window after the tab has been open for about 4 hours. Refreshing the page resets it back to the ~100-minute seed.
- With fewer than two points the cell shows a dim `--`.

---

## The connection indicator

The dot and word in the footer tell you whether what you are looking at is live. There are six states.

| Indicator | How it appears | What it means |
|---|---|---|
| **Loading market data...** | Gold dot, pulsing | The first snapshot has not arrived yet. |
| **Connected** | Green dot, pulsing | The live stream is delivering data normally. |
| **Connected** | **Gold** dot | Degraded: the live stream is unavailable and the app is polling on a timer instead. Hovering shows **Polling**. |
| **Reconnecting...** | Gold dot, ping animation | A new live connection is being opened. Polling continues meanwhile. |
| **Stale** | Plus a warning strip above the table | Data has stopped advancing. See below. |
| **Error** | Plus a warning strip above the table | No accepted snapshot for over two minutes. |

{% hint style="warning" %}
**The word "Connected" alone is not proof of fresh data.** In the polling fallback the word stays "Connected" and only the dot colour changes from green to gold. Gold plus the "Polling" tooltip means you are on the slower path — prices still update, just less often.
{% endhint %}

### Stale and error: the warning strip

When data stops advancing the screener does not leave you to spot it in a footer dot. It renders an explicit warning strip **above the table**, announced to screen readers.

Two independent conditions raise the **stale** state:

- No accepted snapshot has arrived for more than **30 seconds**, or
- Snapshots keep arriving but the newest price write across the entire universe has not moved for more than **60 seconds** — the "the pipe is open but the data is frozen" case.

If more than **120 seconds** pass with no accepted snapshot, the state escalates to **error**.

{% hint style="danger" %}
Do not act on a price while the warning strip is showing. A frozen quote under a calm-looking indicator is one of the most expensive things a screen can do to a trader — that is precisely why this strip exists. Wait for it to clear, reload the page, and confirm the price on the exchange or on the [coin chart](coin-view.md) before you commit money.
{% endhint %}

Behind the scenes: data arrives over a live stream; if that stream fails the app falls back to polling every 3 seconds and keeps retrying the stream with a backoff that tops out at 30 seconds. You do not need to do anything to recover — but you do need to look at the indicator before you trade.

---

## One thing the table cannot tell you

Everything on this screen is a measurement, not a recommendation. Green does not mean buy, a high RVOL does not mean a move is coming, and a chip match is not a signal. The table narrows a universe of ~670 contracts down to a handful worth opening a chart on. What you do after that, and how much you risk, is your decision — see [From screen to trade](from-screen-to-trade.md).

---

**Next:** [Column reference](column-reference.md) — every column, its unit, and its exact time window.
