# Data and coverage

Where every number in ErkeScan comes from, what is in the tradable universe, how often values
change, and the caveats that matter when you are about to risk money on a row in the table.

## One exchange, one contract type

The screener and the custom alerts cover **Binance USDⓈ-M perpetual futures quoted in USDT**,
and nothing else.

The symbol list is taken from Binance's own futures ticker feed and filtered to contracts whose
symbol ends in the literal string `USDT`. That filter excludes:

- USDC-margined pairs,
- dated quarterly contracts such as `BTCUSDT_260925`,
- spot markets,
- every other exchange.

Rows quoted in USDC, and USDC itself as a base asset, are dropped again in the browser before
the table renders.

{% hint style="warning" %}
There is no multi-exchange screener. If you trade the same coin somewhere else, the price,
volume and funding you see here are Binance perpetual figures and will not match your venue
exactly.
{% endhint %}

## How big the universe is, and what is in it

The list holds **roughly 670 contracts**, and it is not all crypto. Binance lists tokenized
equities and commodities as perpetual contracts too, and they sit in the same table with the
same columns — **around 140 of the rows** are these.

You will find names such as TSLA, NVDA and SPY on the equity side, and XAU (gold), CL (crude
oil) and NATGAS on the commodity side.

The list is rebuilt from Binance continuously, so the exact count moves as contracts are listed
and delisted. Never plan around a fixed number.

### The badge next to the ticker

- **STOCK** (blue, RU: **АКЦИЯ**) — a tokenized equity.
- **COMMODITY** (bronze, RU: **ТОВАР**) — a tokenized commodity.
- **A neutral grey tag** — a sector or category label such as Layer-1, Meme, AI or TradFi. Most
  coins carry one of these; some carry no badge at all.

No row is ever badged "CRYPTO". The asset-class feed behind the blue and bronze badges refreshes
about once an hour, and it fails quietly: if it is unavailable, a tokenized equity can fall back
to a plain grey tag, or to no badge, for a while. Judge an unfamiliar ticker by the ticker, not
only by the badge.

## How often the numbers change

All fields are recomputed together by a single merge pass, **at most once every two seconds**.

That is a floor, not a heartbeat. The merge runs when new data arrives from the exchange, so on
a quiet symbol at a quiet moment nothing recomputes for a while, and on a busy one you get a
recomputation about every two seconds and no faster.

Your browser receives each completed merge over a live stream. If the stream is unavailable it
falls back to fetching the same snapshot every three seconds — you will see the connection
indicator change, but the data keeps flowing.

The alert engine reads the same feed on its **own five-second cycle**. That is why an alert can
fire on a value a couple of seconds different from the one on your screen, and why a value that
flickers across your threshold may or may not be caught.

### Where the candles come from

Twenty candles are kept per interval, for each of 5m, 15m, 1h, 8h and 1d. That buffer of 20 is
the baseline behind every "average" in the table — RVOL, volatility and the smoothed RetailHeat
value all measure against it.

- **5m, 15m and 1h** stream live. The in-progress candle is overwritten continuously.
- **8h and 1d** do not stream. They are fetched once per bar, shortly after the bar opens, and
  then held unchanged for the whole 8 or 24 hours.

That is why an 8h or 1d column can sit at exactly the same value for hours. It is not frozen by
accident.

## "Last closed candle" — the idea that decides how you read the table

A candle that is still forming has only part of its final volume in it. A candle that has closed
is final and will never change again.

Most of the volume-family columns read the **last closed** candle:

- **Volume 5m** is the last closed 5-minute candle, not the one filling now.
- **Volume 15m** and **Volume 1h** are trailing sums of the last 3 and last 12 **closed
  5-minute candles** — windows that step forward every five minutes.
- **VDelta** mirrors the volume windows exactly.
- **RVOL 5m** is recomputed in your browser from closed 5-minute candles.

The practical consequence: these values are **stable between steps**. They change in a jump at
a 5-minute boundary and then hold. If you are staring at a Volume 5m figure waiting for it to
climb, it will not — it will jump when the next 5-minute candle closes.

{% hint style="info" %}
**RVOL 1h is the odd one out.** Its numerator is the same trailing sum of the last 12 closed
5-minute candles that feeds Volume 1h, while its baseline comes from the 1-hour candle buffer.
So it re-steps every **five minutes**, not once an hour, and because the two legs come from
different candle series it is an approximation. Read it as "is this hour busy or not", not as a
precise multiple. The column tooltip in the app calls it the last closed 1-hour candle; that
wording is wrong.
{% endhint %}

A smaller set of values does read the **forming** bar, and behaves completely differently:

- **Change 5m** and **Change 15m** measure the move since the last bar boundary, so at ten
  seconds past the hour they describe ten seconds of market, not five or fifteen minutes.
- **RVOL 15m** compares the current, still-filling 15-minute candle against the recent average,
  so it starts low every bar and climbs.
- **Bar Vol Δ (5m), (15m) and (1h)** measure how far the current unfinished bar has filled
  versus the previous completed one. Every symbol starts each bar near −100% at the same
  moment. This is bar progress, not a market event, and the app renders it in neutral colour
  for exactly that reason. The 8h and 1d legs of that family are different — they compare two
  closed bars and do carry a real change in turnover.

{% hint style="warning" %}
Never build a trade or an alert threshold on a forming-bar column without knowing where you are
inside the bar. The same reading means opposite things at second 10 and second 290.
{% endhint %}

## Which windows are genuinely rolling

| Column | What the window really is |
|---|---|
| Change (1h) | True rolling 60 minutes — the price 60 minutes ago against the live price |
| Change (24h), Change$ (24h), Volume (24h) | True rolling 24 hours, taken from the exchange's own 24-hour ticker (its 24h open against the live price). That ticker row is re-fetched about once a minute |
| Volume / VDelta (15m), (1h) | Trailing sums of closed 5-minute candles, stepping every 5 minutes |
| Change (5m), (15m) | Since the last bar boundary — not rolling |
| Change (8h) | The **column** shows the last *closed* 8-hour bar against the one before it |
| Volatility (5m), (15m), (1h) | The label names the candle size, not the look-back: the window is 20 candles, so roughly 100 minutes, 5 hours and 20 hours |
| Ticks (5m), (15m), (1h) | True rolling wall-clock minutes, built from 5-second buckets, so accurate to about ±5 seconds |
| OI Change (5m) … (1d) | Elastic. Open interest is sampled every 5 minutes, so "OI Change 5m" can span anywhere from about 2.5 to 10.5 minutes, and "15m" from about 7.5 to 20.5 minutes |

{% hint style="warning" %}
**Change (8h) is the one place where a column and an alert disagree.** The column reads the
closed-bar value in the table above. An alert condition called *Change (8H)* reads the older
forming-bar value instead, which sits within a fraction of a percent of zero almost all the
time — so that alert will effectively never fire. Alert on Change (1H) or Change (24h) instead.
{% endhint %}

Full per-column detail is in the [column reference](../screener/column-reference.md).

## Two units that are easy to misread

**Funding rate** is published as a **percent with three decimals**, exactly as Binance settles
it for that contract, with no normalisation. `0.010` on screen means 0.01%. It is the rate for
one funding period on that specific contract — nothing in ErkeScan converts it to a daily or
annual figure, and you should not assume every contract settles on the same schedule. It
refreshes about once an hour.

**Ticks** count Binance aggregated trade events, not individual trades. One event bundles every
fill of a single taker order at one price level, so the count is systematically lower than a raw
trade count. RetailHeat, which is built on ticks, inherits the same property.

## What a missing value looks like

A cell with an em dash **—** means *no data*, never zero.

When a feed goes stale the affected fields are set to nothing rather than left showing an old
number, and the cell shows a dash. Rows with dashes sink to the bottom on both ascending and
descending sorts, so they can never masquerade as a 0.00 at the top of your ranking.

Where you will see dashes legitimately:

- A newly listed contract that has not accumulated enough candles yet.
- **VDelta** on a row served from the failover source described below — the underlying
  taker-buy figure is not available there.
- **RetailHeat** on a symbol whose last closed 5-minute volume is under $5,000. Between $5,000
  and $50,000 you get a dimmed value with an asterisk instead, computed against a longer volume
  average rather than the single closed candle.
- **OI Change** during the first minutes after a restart, before enough samples exist.

A whole row disappears if its price is missing or not a valid positive number, or if **either**
its 5-minute or its 15-minute candles are missing. And if a refresh comes back badly
incomplete, the previous good snapshot keeps serving rather than showing you a half-empty
table.

## Honest caveats

**The connection indicator is part of the data.** The screener watches two clocks: how long
since it accepted a fresh snapshot, and whether the newest price write anywhere in the universe
is still advancing. **Stale** is raised after **30 seconds** without an accepted snapshot, or
after **60 seconds** in which no price anywhere has moved forward; **error** after **120
seconds** with no accepted snapshot. Both put a warning strip above the table, not just a small
dot. A frozen price under a calm-looking layout is exactly the situation that costs money,
which is why the warning is loud. Do not trade a screen showing that banner.

**Price is the last traded price, not the mark price.** It comes from the exchange's live
ticker stream, with a bid/ask midpoint as a fallback. Your exchange's mark price, used for
liquidations and funding, will differ.

**There is a failover, but no blending.** If Binance's REST endpoints stop answering, a circuit
breaker can pull a few values from a secondary venue so rows keep serving. Data is never mixed
across exchanges within a single number, and rows served that way lose their VDelta values.

**Some definitions were corrected during 2026.** Volume 1h, the 8h/1d RVOL and volume-change
columns and the 8h change column all had their windows fixed to what their labels promise. A
threshold you wrote down, or a screenshot you saved, before those fixes may be on a different
scale. Re-check old thresholds against a live day before you rely on them.

**Live counts in any documentation age.** Symbol counts, how many coins clear a liquidity floor,
typical funding levels — all of that moves. Treat any number in this manual as a description of
how the system works, not as today's market state.

**Next:** [Glossary](../glossary.md)
