# Quick filters

The chip strip above the table is the fastest way to cut roughly 670 rows down to the handful worth looking at. This page explains all eleven chips: what each one hunts, the exact numeric rule behind it, what a match actually tells you, and why a chip sometimes comes back empty.

## How the chip strip behaves

The chips are **single-select**. Clicking one replaces the previous one — there is no way to combine two chips.

Picking any chip other than **All** clears whatever column sort you had and applies the chip's own ordering, so the most extreme match sits at the top. That ordering then wins for as long as the chip is active: clicking a sort caret does not visibly reorder the rows. To sort by a column of your own choosing, return to the **All** chip first.

The thresholds are fixed. There is no control for editing them, and there is no way to save a chip of your own — see [Build your own filters](build-your-own-filters.md) for the manual method.

Rows with no data in the gating metric never match. If a feed goes stale the affected columns become "—", and a dash is treated as *unknown*, never as zero — so a coin with a missing 1-hour change can never satisfy Accumulation's "price is flat" leg by accident.

Selecting any chip other than **All** also removes the greyed-out no-data block at the bottom of the table entirely.

The counter beside the chips changes meaning with the chip: on **All** it shows how many rows currently have data; on any other chip it shows matched rows out of that same total.

All eleven chips work on phones, along with the search box, the counter and favourites.

{% hint style="info" %}
The **Funding Rate** column is a percent per funding interval. A reading of `0.150` means 0.15%, not 0.0015. Both funding chips compare against that percent scale.
{% endhint %}

## The shared liquidity floor

Three chips — **Top Active 10**, **Top Gainers 1D** and **Top Losers 1D** — share the same two-part liquidity gate before their own rule is applied:

1. **Volume 1h ≥ $500,000.** Volume 1h is the sum of the last twelve *closed* 5-minute candles, in US dollars — a true trailing hour that steps forward every five minutes as each new candle closes.
2. **A primary-path RetailHeat value.** [RetailHeat](../glossary.md) is only computed on its primary path when the last *closed* 5-minute candle traded at least $50,000. Coins whose RetailHeat is shown with an asterisk (the smoothed fallback) are deliberately excluded, as are coins showing a dash.

That second gate is easy to miss: a coin can clear $500,000 an hour and still be shut out of all three chips because its most recent 5-minute candle was thin. Everywhere below, "the shared liquidity floor" means these two conditions together.

These three chips are also computed over the **whole market first**, before your search box is applied. If you type `sol` while **Top Gainers 1D** is active, you get SOL only if SOL is in the global top ten — you do not get "the top gainers among coins matching sol".

---

## 1. All

**What you're hunting:** everything. This is the unfiltered market and the state the table starts in.

**The rule:** no filter is applied.

**What a match means:** nothing in particular — you are looking at every contract the feed delivered. This is the only chip that also renders the greyed-out no-data rows below the divider.

**Empty when:** the table is empty only if the feed itself has delivered nothing. If you see **No results.** here, treat it as a data problem and check the connection indicator in the footer before you trade anything. See [Troubleshooting](troubleshooting.md).

## 2. High Volume

**What you're hunting:** coins whose most recent finished 5-minute candle traded far more than that coin normally trades. It is an attention detector, not a direction detector.

**The rule:** [RVOL](../glossary.md) 5m is strictly greater than **2.00**. RVOL 5m is the dollar volume of the last *closed* 5-minute candle divided by the average of the eighteen closed 5-minute candles before it. Because both sides of that ratio use finished candles, the value does not drift as the current bar fills.

**Sorted by:** RVOL 5m, highest first.

**What a match means:** the last finished five minutes were at least twice as busy as this coin's own recent normal. The chip says nothing about which way price went; read it alongside **Change (5m)** and **VDelta (5m)** to see the direction.

**Empty when:** the whole market is quiet. The list only updates as each 5-minute candle closes, so during a dead session it can sit empty for several bars in a row and then fill within one candle when activity returns.

## 3. OI Spike

**What you're hunting:** fresh positioning — new contracts being opened, not old ones being closed.

**The rule:** the percentage leg of **OI Change (1h)** is strictly greater than **+5%**. This is growth only and it is signed: a −20% unwind does not match.

**Sorted by:** OI Change 1h percent, highest first.

**What a match means:** [open interest](../glossary.md) — the total value of contracts outstanding — grew by more than 5% over roughly the past hour. New money took a position. The chip does not tell you which side. The usual rule of thumb — it is a heuristic, not a measurement — is that rising open interest with rising price points to new longs, and rising open interest with falling price to new shorts. Read it together with **Change (1h)** and **Funding Rate**.

**A note on the window:** the open-interest windows are elastic. Open interest is only sampled every five minutes, so the 1-hour reading compares the current value against the nearest stored sample between about 30 and 65 minutes old. Treat it as "about an hour", not as an exact 60 minutes.

**Empty when:** the market is drifting sideways with no new positioning, or the open-interest poll has gone stale for the coins you care about (their OI cells will show "—").

## 4. Big Movers

**What you're hunting:** coins that have actually moved in the last hour, in either direction.

**The rule:** the absolute value of **Change (1h)** is strictly greater than **3%**. It is bi-directional — a −6% hour qualifies exactly as much as a +6% hour.

**Sorted by:** the size of the 1-hour move, largest first, ignoring the sign. Winners and losers are interleaved.

**What a match means:** a real 1-hour move is in progress. Change (1h) is a true rolling 60-minute change built from 5-minute candles plus the live price, so it does not reset on the hour — the number you see is genuinely "versus one hour ago".

**Empty when:** the market is calm. On a flat weekday afternoon it is normal for this chip to return two or three rows, or none at all.

{% hint style="warning" %}
A big mover is not automatically a trade. By the time a coin clears +6% in an hour, much of the move is behind you and the risk of buying the top is at its highest. Use it as a shortlist to research, not as an entry signal.
{% endhint %}

## 5. High Funding

**What you're hunting:** contracts where one side of the book is paying heavily to stay in its position — a crowding signal.

**The rule:** the absolute **Funding Rate** is strictly greater than **0.1** (that is, 0.1% per funding interval). Bi-directional: both extreme positive and extreme negative funding match.

**Sorted by:** absolute funding, highest first.

**What a match means:** positive funding means longs are paying shorts, so the long side is crowded; negative funding means shorts are paying longs. Funding is published per funding interval by the exchange and is shown exactly as published, with no annualisation and no per-period normalisation — different contracts can settle on different schedules.

**Empty when:** funding across the market has normalised. Note that the Funding Rate column is refreshed roughly once an hour, so this chip's membership changes slowly — it will not react to something that happened five minutes ago.

## 6. Accumulation

**What you're hunting:** the pattern where positions are being built while price stays quiet — the "someone is loading up" screen.

**The rule:** all three must hold at once.

- **OI Change (1h)** greater than **+3%** (growth only, signed)
- **RVOL 1h** greater than **1.5**
- absolute **Change (1h)** less than **1%**

**Sorted by:** OI Change 1h percent, highest first.

**What a match means:** open interest is growing and turnover is above this coin's own normal, yet price has gone nowhere for an hour. That combination is often read as large participants building a position into passive liquidity before a move. It is an interpretation, not a proof — the same footprint appears when two large players simply disagree.

**About the RVOL 1h leg:** this is an approximation on both sides. The numerator is the last 60 minutes of turnover assembled from twelve closed 5-minute candles, which re-steps every five minutes rather than once an hour; the baseline comes from the retained hourly candles. Read it as "is this hour busier than usual for this coin", not as an exact multiple.

**Empty when:** most of the time. It is the strictest of the eleven chips after Squeeze, because it demands two readings to be high while a third stays low. Empty is its normal state; a handful of matches is a genuinely interesting list.

## 7. Squeeze

**What you're hunting:** a crowded side that is already being punished — the setup where forced liquidations feed the move.

**The rule:** both must hold.

- absolute **Funding Rate** greater than **0.15** (0.15% per funding interval), and
- price moving against the crowded side by more than 1% over the past hour: funding positive (longs crowded) with **Change (1h)** below **−1%**, or funding negative (shorts crowded) with **Change (1h)** above **+1%**.

**Sorted by:** absolute funding, highest first.

**What a match means:** the side that was paying to hold its position is now underwater. Longs paying premium into a falling price are candidates for a long squeeze; shorts paying premium into a rising price are candidates for a short squeeze. The move can accelerate as positions are closed out — and it can also stop dead the moment the crowd is flushed.

**Empty when:** most of the time. Two independent extremes have to line up at once, and funding of 0.15% per interval is already a rare reading on its own. Empty here means "no squeeze right now", which is a useful answer.

{% hint style="warning" %}
Squeezes are the fastest-moving rows on the screener and the easiest place to lose money. Size small, decide your invalidation before you enter, and remember the chip tells you a squeeze is *possible*, not that it will continue.
{% endhint %}

## 8. Breakout

**What you're hunting:** compression with one-sided flow — a coin that has been unusually quiet but whose last finished candle was busy and strongly directional.

**The rule:** all four must hold.

- **Volatility (5m)** greater than 0 **and** strictly below the median Volatility (5m) of the whole streamed market (the compression leg)
- **RVOL 5m** at least **1.20**
- **Volume (5m)** at least **$50,000** — dollars traded in the last *closed* 5-minute candle, the same basis RetailHeat uses
- absolute **VDelta (5m)** divided by **Volume (5m)** greater than **0.20** — more than a fifth of the bar's turnover was net directional

**Sorted by:** that VDelta-to-volume ratio, highest first.

**What a match means:** the coin has been calmer than the median contract over roughly the last 100 minutes (Volatility 5m is a standard deviation of returns across the last 20 five-minute candles), and then a single finished 5-minute candle came in with above-normal volume that was heavily one-sided. The sign of **VDelta (5m)** tells you which way that pressure leaned: positive is net taker buying, negative is net taker selling.

**Empty when:** often, because four conditions must hold together and the $50,000 single-candle floor is strict. Note also that the compression bar moves: it is the median of the whole streamed market, recalculated on every update. On a violent day the median rises and more coins count as "quiet"; on a dead day it falls and fewer do — so a coin can enter or leave this chip without changing at all.

## 9. Top Active 10

**What you're hunting:** where the crowd is right now, measured by raw trade count rather than dollars.

**The rule:** from the coins that pass the shared liquidity floor, take the ten with the highest **Ticks (5m)**, highest first.

**Sorted by:** Ticks 5m, highest first.

**What a match means:** Ticks (5m) counts aggregated trade events over the trailing five real-time minutes — a rolling wall-clock count, not a candle. A high count with modest dollar volume means many small orders; a high count with huge dollar volume means the whole market is engaged. The companion **RetailHeat (5m)** column turns the same two numbers into a ratio: aggregated trade events per $1 million of the last *closed* 5-minute candle's dollar volume. High means fragmented, retail-sized flow; low means fewer, larger trades.

**Empty or short when:** this chip can legitimately return fewer than ten rows. On a calm day only a handful of contracts clear both parts of the shared liquidity floor, and the list is never padded out to ten. A coin with an asterisked RetailHeat is excluded even if it is genuinely busy.

## 10. Top Gainers 1D

**What you're hunting:** the day's strongest liquid movers.

**The rule:** from coins that pass the shared liquidity floor, keep those whose **Change (24h)** is at least **+1.5%**, then take the top ten by that change, highest first.

**Sorted by:** Change 24h, highest first.

**What a match means:** these are the biggest 24-hour winners among contracts that actually trade. The number is a **rolling** 24 hours taken from the exchange's 24-hour ticker plus the live price — not a calendar day and not a daily candle. The chip is labelled "1D" while the matching column is headed **CHANGE (24h)**; they are the same number.

**Empty or short when:** fewer than ten liquid coins are up 1.5% or more. That is common in a flat or falling market and is not a bug.

## 11. Top Losers 1D

**What you're hunting:** the day's weakest liquid movers.

**The rule:** identical to Top Gainers 1D, with the direction reversed: **Change (24h)** at most **−1.5%**, then the ten most negative.

**Sorted by:** Change 24h, lowest first.

**What a match means:** the biggest 24-hour losers among contracts that actually trade — the shortlist for continuation shorts, for mean-reversion longs, and for finding what is dragging a sector down. As with gainers, the window is rolling 24 hours, not a calendar day.

**Empty or short when:** fewer than ten liquid coins are down 1.5% or more.

---

## All eleven rules at a glance

| # | Chip | Exact rule | Chip's own ordering |
|---|---|---|---|
| 1 | **All** | No filter. Only chip that shows the no-data block. | none (your sort) |
| 2 | **High Volume** | RVOL 5m > 2.00 | RVOL 5m, high → low |
| 3 | **OI Spike** | OI Change 1h % > +5 (growth only) | OI Change 1h %, high → low |
| 4 | **Big Movers** | \|Change 1h\| > 3% | size of 1h move, high → low |
| 5 | **High Funding** | \|Funding Rate\| > 0.1% | \|funding\|, high → low |
| 6 | **Accumulation** | OI Change 1h % > +3 **and** RVOL 1h > 1.5 **and** \|Change 1h\| < 1% | OI Change 1h %, high → low |
| 7 | **Squeeze** | \|Funding\| > 0.15% **and** price moved > 1% against the crowded side over 1h | \|funding\|, high → low |
| 8 | **Breakout** | Volatility 5m > 0 and below the market median **and** RVOL 5m ≥ 1.20 **and** Volume 5m ≥ $50,000 **and** \|VDelta 5m\| ÷ Volume 5m > 0.20 | VDelta ratio, high → low |
| 9 | **Top Active 10** | Volume 1h ≥ $500,000 **and** primary-path RetailHeat → top 10 by Ticks 5m | Ticks 5m, high → low |
| 10 | **Top Gainers 1D** | Same floor **and** Change 24h ≥ +1.5% → top 10 | Change 24h, high → low |
| 11 | **Top Losers 1D** | Same floor **and** Change 24h ≤ −1.5% → top 10 | Change 24h, low → high |

{% hint style="warning" %}
Every chip is a screening tool, not a recommendation. A match means a numeric condition is currently true — nothing more. Decide your entry, your stop and your invalidation before you act on any row, and never trade a row whose prices are frozen (see the connection states in [Reading the table](reading-the-table.md)).
{% endhint %}

For what each metric means in full — unit, exact time window and the traps — see the [Column reference](column-reference.md).

**Next:** [Make the screener yours](personalize.md) — columns, order, density, favourites and language.
