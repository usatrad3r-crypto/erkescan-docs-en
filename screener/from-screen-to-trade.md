# From screen to trade

A row in the screener is not a trade. This page walks the chain that turns one into a decision: read the row properly, look at the chart, check the context, write a thesis, define what would prove it wrong, size against that point, and decide your exits before you are in.

{% hint style="danger" %}
**This page is education about using a data tool. It is not investment advice.** ErkeScan shows you market data; it does not tell you what to buy, when, or how much. The examples below use made-up numbers to demonstrate a process, not to recommend a trade. Nothing on the screener places an order — you execute on your exchange, and the decision, the position size and the loss are entirely yours.
{% endhint %}

## Step 1 — Read the row, and check it is trustworthy

Before you interpret anything, confirm the row is real data.

1. **Is the connection healthy?** If a warning strip is showing above the table, prices may be frozen. Do not read a frozen price as a live one. See [troubleshooting](troubleshooting.md).
2. **Is the row in the faded block at the bottom?** Rows below the hairline separator, rendered at 40% opacity, have no usable market data at all.
3. **Are your decision columns showing numbers?** A "—" means no data, not zero. If the column your thesis rests on is a dash, you do not have a thesis.
4. **Does RETAILHEAT carry an asterisk?** That value was smoothed because the last closed 5-minute candle was thin ($5,000–$50,000). Treat it as a hint at best.

Then read across the families below, in this order, because each one changes how you read the next. Any term that is new to you is defined in the [glossary](../glossary.md), and every column's exact window in the [column reference](column-reference.md).

| Read | Column | Question it answers |
|---|---|---|
| Liquidity | **VOLUME (1h)**, **VOLUME (24h)** | Can I actually trade this size? |
| Price | **CHANGE (1h)**, **CHANGE (24h)**, **TREND** | Has the move already happened? |
| Participation | **RVOL (5m)**, **VDELTA (5m/1h)**, **TICKS (5m)**, **RETAILHEAT (5m)** | Is anybody there, and on which side? |
| Positioning | **OPENINTEREST**, **OI CHANGE (1h)**, **FUNDING RATE** | Who is holding what, and who is paying? |
| Context | **BTC CORR (1h)** | Is this the coin's story or the market's? |

Two combinations do most of the interpretive work. Learn them well:

- **Price + open interest.** Rising price with rising open interest means new positions are being opened into the move. Rising price with falling open interest means positions are being closed — often shorts covering, and often late in a move.
- **Volume + VDelta.** Volume tells you how much traded; VDelta tells you how much of it was net taker buying (green) or selling (red), in dollars. Heavy volume with VDelta near zero is a battle, not a direction.

## Step 2 — Open the coin's chart

Click the **ticker text** in the Symbol cell. A TradingView chart opens in a modal over the table, showing the Binance perpetual for that coin on a 15-minute interval. Close it with **Escape**, the **×**, or a click on the dimmed backdrop. **Full Page →** opens the coin's own page in a new tab.

The screener tells you what is unusual *now*. The chart tells you what "now" is sitting on: a range edge, a prior high, a third consecutive push, the third failed attempt at the same level. A metric without that structure is a number without a location.

Details in [Coin view and the symbol page](coin-view.md).

## Step 3 — Cross-check the context on /charts

Go to [Charts](charts.md) and pick the cohort your coin belongs to — Top Gainers · 24h, Top Losers · 24h, Top Volume · 24h or Top Active · 5m — at the window that matches your horizon. Each cohort holds only a handful of names, so your coin may be in none of them; in that case pick the cohort closest to what it is doing and read the group as background rather than as a peer set.

Three questions to answer there, quickly:

- **Is my coin leading or following its cohort?** The price rotation spaghetti answers this in one glance.
- **Is the whole cohort doing this?** The return-bucket histogram shows whether the day is broad or narrow. If everything is up, you are trading market beta with extra steps.
- **Is my funding read unusual, or is the whole board stretched?** The funding table shows the twelve most extreme funding rates among liquid coins.

## Step 4 — Write the thesis in one sentence

The sentence must contain a **mechanism**, not just an observation. Compare:

- ❌ *"RVOL is 3.4× and VDelta is green."* — that is the screen output read back to you.
- ✅ *"Longs have crowded in over the last day, funding is paying heavily to hold them, and the last hour has gone against them with open interest falling — so this is more likely position-closing than new selling."*

If you cannot name a mechanism, you do not have a trade. You have a coincidence with good colour coding.

## Step 5 — Define invalidation before you enter

Write two invalidation conditions, both before entry:

- **A price level.** A place on the chart where your read of the structure is simply wrong. This is your stop.
- **A data condition.** Something in the screener that, if it changes, kills the mechanism even if price has not hit your stop. "Open interest stops falling." "VDelta flips positive for two consecutive candles." "Funding normalises." This is the one most traders skip, and it is the one that gets you out early with a small loss.

{% hint style="warning" %}
Set the price stop on your exchange. A data-condition exit lives in your own discipline — ErkeScan can watch a level for you with a [custom alert](../alerts/create-an-alert.md), but it will not close anything.
{% endhint %}

## Step 6 — Size against the stop, not against the idea

Position size falls out of the stop, not out of how much you like the trade. The arithmetic:

```
units = (money you decided to risk) ÷ (distance from entry to stop, per unit)
notional = units × entry price
```

You choose the risk figure. That is a decision about your own account and it is not something a manual can make for you. What the arithmetic guarantees is that a wide stop gives you a small position and a tight stop gives you a large one, so the loss is the same either way — which is the point.

Two things the screener cannot show you and you must budget for anyway: the **spread** you cross on entry and exit, and the **slippage** on a fast tape. The PRICE column is the last traded price, not a quote you are entitled to.

## Step 7 — Decide your exits in advance

Write down, before entry:

- **The invalidation exit** — price stop, non-negotiable.
- **The thesis exit** — the data condition from step 5. It usually fires before the stop.
- **The target**, and what would make you take part of it early.
- **The time stop.** Every recipe in [Recipes](recipes.md) has a natural horizon. A 5-minute-trigger idea that has done nothing in two hours is a different trade than the one you entered.

---

## Worked example 1 — a squeeze read

**The row.** You are on the **Squeeze** chip. One row reads:

| Column | Value |
|---|---|
| PRICE | $0.4820 |
| FUNDING RATE | 0.184% |
| CHANGE (1h) | -1.62% |
| CHANGE (24h) | 11.40% |
| OI CHANGE (1h) | -$4.20M (-3.11%) |
| VOLUME (1h) | $6.40M |
| VDELTA (1h) | -$1.10M |
| BTC CORR (1h) | 0.18 |

**Reading it.** Funding is 0.184% per funding period and positive, so longs are paying to hold — they are the crowded side. Price has fallen 1.62% over the rolling hour against them. Open interest is down 3.11% and $4.20M in the same hour, so positions are being *closed*, not merely marked down. VDelta is negative: $1.10M more taker selling than taker buying across the last twelve closed 5-minute candles. Liquidity clears the $500,000-per-hour floor comfortably. BTC correlation is 0.18 — in the muted band the table renders grey, so this is not simply a market-wide move.

**Chart check.** You open the chart and find the price is coming back into a range it broke out of two days ago, with the day's rally starting from the bottom of that range.

**Context check.** On /charts, the Top Gainers · 24h cohort at the 1D window shows most of the cohort still rising. This coin is the odd one out — consistent with a positioning unwind rather than a sector rotation.

**Thesis.** *"A crowded long book built during a +11% day is unwinding into the range it broke out of; if open interest keeps falling, the unwind continues toward the range low."*

**Invalidation.**
- Price: back above $0.4995, above the recent swing that defines the failed breakout.
- Data: OI CHANGE (1h) turning positive, or funding falling back near zero — either means the crowded book is gone and the mechanism is spent.

**Sizing.** Suppose you decided in advance to risk $200 on this idea. Entry $0.4820, stop $0.4995, so the distance is $0.0175 per unit — 3.63% of the entry price.

```
units    = 200 ÷ 0.0175   ≈ 11,430
notional = 11,430 × 0.4820 ≈ $5,510
```

**Exits.** Thesis exit if open interest stabilises for two consecutive readings. Target at the range low. Time stop: if nothing has resolved in six hours, funding will have settled and the trade is no longer the one you took.

**What actually goes wrong here:** funding stays elevated because the crowd is stubborn, price grinds sideways, and you pay the spread twice for a flat result. That is the good outcome. The bad one is a squeeze that resolves *upward* because the shorts that arrived to fade it were the real crowd.

---

## Worked example 2 — a compression read

**The row.** You are on the **Breakout** chip. One row reads:

| Column | Value |
|---|---|
| PRICE | $2.1440 |
| VOLATILITY (5m) | 0.31% |
| RVOL (5m) | 1.84× |
| VOLUME (5m) | $310.00K |
| VDELTA (5m) | $96.00K |
| CHANGE (1h) | 0.42% |
| VOLUME (1h) | $2.90M |
| OI CHANGE (1h) | $820.00K (1.90%) |

**Reading it.** The coin qualifies because its VOLATILITY (5m) sits below the market median while the last closed 5-minute candle traded 1.84× the average of the eighteen candles before it, with 31% of that candle's turnover net directional and positive ($96.00K of $310.00K). Price has barely moved over the hour, so the buying has been absorbed rather than chased. Open interest is up 1.90% — new positions, not just churn. Hourly volume clears the $500,000 floor.

**Chart check.** The 15-minute chart shows a tight two-hour range directly under a level that rejected price twice yesterday.

**Thesis.** *"Persistent one-sided buying is being absorbed just under a known resistance; if the level goes, the absorbed supply is gone and there is little above it."*

**Invalidation.**
- Price: back below $2.0980, the bottom of the tight range — the absorption story is dead if the range breaks the other way.
- Data: VDELTA (5m) turning negative on two consecutive closed candles while volume stays elevated, meaning the aggressor changed sides.

**Sizing.** Say you decided to risk $150. Entry $2.1440, stop $2.0980 — distance $0.0460, 2.15% of entry.

```
units    = 150 ÷ 0.046    ≈ 3,260
notional = 3,260 × 2.144  ≈ $6,990
```

**Exits.** Take part of it on the first close above the level with RVOL 5m still elevated. Thesis exit on the VDelta flip. Time stop of about an hour — compression setups that do not expand promptly usually just decompress into chop.

**What actually goes wrong here:** the Breakout chip's compression test is against the *universe median*, which moves. On a day when the whole market goes quiet, half the board qualifies and "unusually quiet" means nothing. Check whether the chip returned 4 rows or 90 before you believe the compression is specific to this coin.

---

## Worked example 3 — the row you should not trade

**The row.** Top of the table after sorting **CHANGE (1h)** descending:

| Column | Value |
|---|---|
| PRICE | $0.001482 |
| CHANGE (1h) | 19.60% |
| VOLUME (1h) | $86.00K |
| VOLUME (5m) | $4.90K |
| VDELTA (5m) | — |
| RETAILHEAT (5m) | — |
| OI CHANGE (1h) | — |

**Reading it.** The largest hourly move on the entire board, and every column you would use to confirm it is empty. The last closed 5-minute candle traded $4.90K, below the $5,000 floor under which ErkeScan will not compute RetailHeat at all. VDelta is a dash — one of the candles in the window was missing its buy/sell breakdown, so you have no idea who was buying. Open interest change is a dash too. Hourly volume of $86.00K is about a sixth of the $500,000 the product's own top-N chips require.

**The decision.** There is no thesis to write. A 19.6% move on that turnover is not information about demand; it is information about the order book being thin. The correct action is to move on — and, if you want to watch it, star it and check whether liquidity ever arrives.

**The lesson.** The biggest number in a sorted column is very often the least trustworthy row in the table, because extremes and thin liquidity are the same phenomenon. Sorting shows you extremes. Liquidity floors are what turn extremes into candidates.

---

## A checklist you can actually use

1. Connection healthy, row not faded, decision columns not dashes.
2. VOLUME (1h) above your floor.
3. Trigger metric confirmed by a second family.
4. Chart opened; the metric has a location on the price structure.
5. Cohort checked on /charts — leading, following, or just beta?
6. Thesis written in one sentence, with a mechanism.
7. Price invalidation and data invalidation both written down.
8. Size computed from the stop distance, not from conviction.
9. Exits — target, thesis exit, time stop — decided before entry.
10. Note kept, so the screen can be judged later rather than remembered fondly.

{% hint style="warning" %}
A process does not make a trade profitable. It makes a losing trade small and a mistake findable. Most rows that survive all ten steps will still not work out, and no combination of columns in this product has been shown to predict a market. Trade only money you can lose, and own the decision.
{% endhint %}

**Next:** [Coin view and the symbol page](coin-view.md) — the chart that opens over the table, and the full page behind it.
