# Glossary

Every term used in this manual, in plain language. Where ErkeScan's meaning is narrower than the
general trading one, that is spelled out.

## A

**Accumulation** — Generally, quietly building a position without pushing price. In ErkeScan it
is a [quick filter](screener/quick-filters.md): open interest up more than 3% over the last hour,
RVOL 1h above 1.5, and the hourly price move under 1% in either direction.

**Active subscription** — See *Premium*.

**Advanced fields** — The collapsed section at the bottom of the alert form holding the 11
Volatility, Ticks and VDelta conditions. Open it with **Show advanced fields**.

**aggTrade event** — One Binance aggregated trade record. It bundles every fill of a single taker
order at one price level into a single event. ErkeScan's *Ticks* and *RetailHeat* count these
events, so they run lower than a raw trade count.

**Alert** — A rule of one or more conditions that sends you a Telegram message when it is met.
An alert is **not tied to a symbol**: it is checked against every contract in the universe and
fires per matching contract, one message each. Multiple conditions are combined with AND and
must all hold on the same contract in the same pass. You can hold up to **200** alerts at a
time, on any plan. See [how alerts work](alerts/how-alerts-work.md).

**Asset class** — Whether a contract is a coin, a tokenized equity or a tokenized commodity.
Equities and commodities carry a **STOCK** or **COMMODITY** badge next to the ticker.

## B

**Bar** — See *Candle*.

**Bar progress** — How far the current unfinished candle has filled compared with the previous
completed one. The **Bar Vol Δ** columns for 5m, 15m and 1h measure exactly this, so every symbol
reads close to −100% at the start of each bar. It is not a market move. The 8h and 1d legs of the
same family are different: they compare two closed bars.

**Bar Vol Δ$ / Δ%** — See *Bar progress*. The dollar leg is the change in turnover, the percent
leg the same change as a proportion.

**Basis** — The gap between a futures or perpetual price and the spot price of the same asset. A
general market term; ErkeScan does not show a basis column.

**Big Movers** — A quick filter: absolute price change over the last hour above 3%, in either
direction.

**Breakout** — A quick filter looking for compression before expansion: 5-minute volatility above
zero but below the universe median, RVOL 5m at 1.2 or higher, last closed 5-minute volume of at
least $50,000, and absolute VDelta above 20% of that volume.

**BTC correlation** — How closely a symbol's returns have tracked Bitcoin's, from −1 to +1,
measured on the last 20 candles of the chosen interval. Available on 5m, 15m, 1h, 8h and 1d.
There is no ETH correlation in the product.

## C

**Candle** — One bar of price history covering a fixed period: 5 minutes, 15 minutes, 1 hour, 8
hours or 1 day. ErkeScan keeps the last 20 candles of each interval.

**Change $** — A price move expressed in dollars per unit rather than in percent.

**Change %** — A price move in percent. Read the window carefully: 5m and 15m measure the move
since the last bar boundary, while 1h and 24h are true rolling windows.

**Change (8h)** — The column compares the last closed 8-hour bar with the one before it. The
alert condition of the same name reads a different, forming-bar value that stays near zero, so
an alert on it will effectively never fire.

**Cooldown** — The wait before the same alert can fire again on the same contract: **60 minutes**
by default, and not adjustable in the form. It is per alert *and* per contract, so the same
alert can fire on a different contract a second later.

**Chip** — One of the 11 one-click filter buttons above the table (All, High Volume, OI Spike,
Big Movers, High Funding, Accumulation, Squeeze, Breakout, Top Active 10, Top Gainers 1D, Top
Losers 1D). Only one can be active at a time. Also called a *quick filter*.

**Closed candle** — A candle whose period has ended. Its numbers are final and never change
again. Most volume, VDelta and RVOL columns read the last closed candle, which is why they hold
steady inside a bar and step at the boundary.

**Cohort** — A group of symbols plotted together on the [Charts page](screener/charts.md): Top
Gainers 24h, Top Losers 24h, Top Volume 24h, Top Active 5m.

**Contract** — One tradable Binance USDT-margined perpetual, and one row in the screener table.
Used interchangeably with *symbol* and *coin* in this manual, except where a row is a tokenized
stock or commodity rather than a coin.

## D

**Density** — The screener setting that controls row height, trading visible rows against
readability.

## E

**Em dash (—)** — In a cell it means *no data*, never zero. A dead feed produces a dash rather
than a fabricated 0.00, and dashed rows sink to the bottom of every sort.

## F

**Favourites** — Coins you have starred. They are lifted into their own block at the top of the
table. Stored in the browser you starred them in, so they do not follow you to another device.

**Forming candle** — The candle currently being built. Its volume is incomplete and grows through
the bar. Change 5m, Change 15m, RVOL 15m and the fast Bar Vol Δ legs read the forming candle.

**Funding rate** — The periodic payment between long and short holders of a perpetual contract.
Positive means longs pay shorts; negative means shorts pay longs. ErkeScan shows it as a percent
with three decimals, exactly as the exchange settles it for that contract, for one funding
period — it is never annualised or converted.

## H

**High Funding** — A quick filter: absolute funding rate above 0.1%, in either direction.

**High Volume** — A quick filter: RVOL 5m above 2.0, meaning the last closed 5-minute candle
traded more than twice its recent average.

## L

**Liquidity** — How easily you can get in and out of a position without moving price. ErkeScan's
practical proxy for it is **Volume 1h**.

**Liquidity floor** — The $500,000-per-hour Volume 1h threshold a symbol must clear before it can
appear in the Top Active, Top Gainers and Top Losers chips, in the Charts cohorts, or in the
Charts funding table.

## M

**Mark price** — An exchange's reference price, used for funding and liquidations. ErkeScan's
**Price** column is *not* the mark price: it is the last traded price, with a bid/ask midpoint as
a fallback.

## O

**OI Spike** — A quick filter: open interest up more than 5% over the last hour. Growth only.

**Open interest (OI)** — The value of contracts currently open on a symbol, shown in US dollars.
Rising OI alongside rising price means new money is entering; falling OI means positions are
being closed. ErkeScan samples it every five minutes, which is why the OI Change windows are
approximate.

## P

**Percentile (pNN)** — The small grey number beside a RetailHeat value, showing where that reading
ranks among all symbols that produced one. p90 means only about a tenth of the pool read higher.

**Perpetual (perp)** — A futures contract with no expiry date. It is held open indefinitely, and
funding payments keep it tethered to the underlying price. Every row in ErkeScan is a perpetual.

**Premium** — In ErkeScan this means one thing: an active subscription on your account. It gates
the screener, alerts, the Charts page, symbol pages, and the live details on the signal pages.

**Profit factor** — Gross profit divided by gross loss across a set of trades. Shown on the
strategy cards in the Signals hub.

**Profitable** — On the Signals hub, the share of trades that closed in profit, partial exits
included. It is deliberately not called a win rate, because a strict win rate is a different and
lower number.

## Q

**Quick filter** — See *Chip*.

## R

**RetailHeat (5m)** — An ErkeScan-only measure: aggTrade events per $1 million of 5-minute dollar
volume. High means many small orders per dollar traded; low means fewer, larger ones. A value
with an asterisk is a smoothed fallback used when the last closed 5-minute candle traded between
$5,000 and $50,000; below $5,000 the cell shows a dash.

**Rolling window** — A window measured backwards from *now*, continuously, rather than from the
last bar boundary. Change 1h, Change 24h, Volume 24h and the Ticks columns are genuinely rolling.
Change 5m and Change 15m are not.

**RVOL (relative volume)** — How current volume compares with the recent average, as a multiple.
2.0 means twice normal. The legs are not built identically. **RVOL 5m** compares the last closed
5-minute candle with the average of the closed ones before it, and holds steady until the next
5-minute close. **RVOL 15m** reads the still-forming 15-minute candle, so it starts low each bar
and climbs. **RVOL 1h** divides the trailing sum of the last 12 closed 5-minute candles by a
baseline taken from the 1-hour candles, so it re-steps every five minutes and mixes two candle
series — treat it as an approximation. RVOL 8h and 1d compare the last closed bar of that size
with the ones before it.

## S

**Sector tag** — The neutral grey label some coins carry beside the ticker (Layer-1, Meme, AI,
TradFi and similar). No row is ever badged "CRYPTO".

**Signal** — A published trade idea from one of the premium strategies, shown on its page and
delivered in Telegram with entry, stop and two targets. Separate from your own custom alerts. See
[premium overview](premium/overview.md).

**Snapshot** — One complete recomputation of every field for every symbol. The screener serves the
newest accepted snapshot; if a new one comes back badly incomplete, the previous good one keeps
serving.

**Sparkline** — See *Trend*.

**Squeeze** — Generally, crowded positioning being forced to unwind. In ErkeScan it is a quick
filter: absolute funding above 0.15% together with a move of more than 1% over the last hour
against the crowded side.

**Stale** — A connection state, shown as a banner above the table, meaning no fresh snapshot has
been accepted recently or prices have stopped advancing. Prices on screen may be frozen. Do not
trade off a stale screen.

## T

**Ticks** — The count of aggTrade events in the last 5, 15 or 60 wall-clock minutes. Not individual
trades, and not a candle metric — the window rolls continuously and is accurate to about five
seconds.

**Tokenized commodity** — A perpetual contract tracking a commodity such as gold, crude oil or
natural gas, badged **COMMODITY**.

**Tokenized equity** — A perpetual contract tracking a stock or index such as TSLA, NVDA or SPY,
badged **STOCK**.

**Top Active 10** — A quick filter showing the ten most retail-active liquid symbols, ranked by
RetailHeat.

**Top Gainers 1D / Top Losers 1D** — Quick filters showing the biggest liquid movers over the
rolling 24 hours in one direction, requiring at least a 1.5% move.

**Trend (4h)** — The small green or red line in the second column, drawn from prices sampled while
the tab is open. Green means the last sample sits at or above the first. It needs about four hours
of an open tab to cover the full window, and restarts from a shorter seed after a page reload.

## U

**Universe** — Every contract ErkeScan tracks: roughly 670 Binance USDT-margined perpetuals,
around 140 of them tokenized equities and commodities. Rebuilt from the exchange continuously.

**USDⓈ-M / USDT-margined** — Binance futures collateralised and quoted in USDT. Only these are
covered; USDC-margined and dated quarterly contracts are excluded.

## V

**VDelta** — Net taker flow in dollars over the window: buyer-initiated volume minus
seller-initiated volume. Positive means aggressive buying dominated. It is a dollar figure, not a
count, and it is blank rather than zero when the underlying breakdown is unavailable.

**Volatility** — The spread of a symbol's per-candle returns, in percent. The label names the
candle size, not the look-back: the measurement always uses 20 candles, so "Volatility 1h" spans
roughly 20 hours.

**Volume** — Dollars traded in the window. Volume 5m is the last closed 5-minute candle; 15m and
1h are trailing sums of closed 5-minute candles; 24h is a true rolling 24 hours from the
exchange.

## W

**Watchlist** — See *Favourites*.

**Next:** [Frequently asked questions](faq/README.md)
