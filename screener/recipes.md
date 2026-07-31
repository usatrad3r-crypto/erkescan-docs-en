# Recipes

Twelve concrete screens you can run today, each built from the chips, columns and sorts described in [Build your own filters](build-your-own-filters.md). Every one tells you what it hunts, exactly how to set it up, what confirms it, what kills it, and what it costs you when it is wrong.

## How to read a recipe

Numbers in these recipes come in two kinds, and the difference matters:

- **Product rule** — a threshold ErkeScan enforces in code. When a chip says "above 3%", that is the machine's number and it is exact.
- **Rule of thumb** — a number *we* suggest as a starting point. ErkeScan does not enforce it. It is a place to begin, not a discovery.

Every column named here is defined in the [column reference](column-reference.md), and the trading terms in the [glossary](../glossary.md).

Reminders that apply to all twelve: sorting is the **small caret** beside a column header, first click ascending and second descending. Selecting a chip clears your sort. Rows showing "—" sink to the bottom whichever way you sort. Only the three top-N chips carry the shared liquidity floor; on every other recipe, checking **VOLUME (1h)** is your job.

---

## 1. Fresh volume surge

**Hunting:** a coin whose last completed 5-minute candle traded far more than its own recent normal — the earliest useful sign that something is happening.

**Set it up:** click the **High Volume** chip. *(Product rule: RVOL 5m above 2.0×, computed from the last closed 5-minute candle against the average of the 18 before it. The list arrives sorted by RVOL 5m descending.)*

**Confirm with:**
- **VOLUME (5m)** — the actual dollars in that candle. *(Rule of thumb: ignore anything under $50,000; that is the floor ErkeScan itself uses elsewhere for "this candle is real".)*
- **VDELTA (5m)** — green and large means the surge was net taker buying; red means selling; near zero means a two-sided fight.
- **TICKS (5m)** — the count of aggregated trade events over the trailing five minutes — and **RETAILHEAT (5m)**, which is those trades per $1 million of the last closed 5-minute candle's turnover. A high RetailHeat percentile reads as fragmented, retail-sized flow; a low one reads as fewer, larger trades.
- **CHANGE (5m)** — has the price responded to the volume, or absorbed it?

**Invalidated by:** the next closed candle printing an ordinary RVOL, VDelta flipping against the first candle, or a dash appearing in VDELTA (no directional read available).

**Timeframe:** minutes. This is the shortest-horizon recipe on the page and it decays fast.

**Risk note:** a single hot candle is the most common false positive in the whole product. One candle is an event; three consecutive ones are a move.

---

## 2. Hourly momentum scan

**Hunting:** coins that have made a real move in the last rolling hour, in either direction.

**Set it up:** click **Big Movers**. *(Product rule: absolute Change 1h above 3%, bi-directional — a −6% hour qualifies exactly as much as a +6% hour. Sorted by |Change 1h| descending.)* To separate the two directions, sort **CHANGE (1h)** yourself: one caret click puts the biggest fallers on top, two puts the biggest risers on top.

**Confirm with:**
- **VOLUME (1h)** — the liquidity floor this chip does not apply. *(Rule of thumb: $500,000, the floor ErkeScan uses for its own top-N chips.)*
- **OI CHANGE (1h)** — the interpretation hinge. Price up with open interest up means new positions opening into the move. Price up with open interest falling means positions closing — frequently short covering, and frequently late.
- **RVOL (1h)** above 1.5× suggests the hour was busy, not just directional. It is an approximate ratio — its numerator is a trailing 60 minutes built from twelve closed 5-minute candles and it re-steps every 5 minutes, so read it as "busier than usual", not as an exact multiple.

**Invalidated by:** CHANGE (1h) decaying back under 3% while volume dries up, or open interest reversing hard against the price.

**Timeframe:** the coming hours.

**Risk note:** Change 1h is a true rolling 60 minutes, so a coin can leave this chip simply because the clock moved, without anything happening. Do not read an exit from a chip drop-out.

---

## 3. Quiet build-up

**Hunting:** positions being opened while the price stays flat — somebody accumulating before a move, at least in theory.

**Set it up:** click **Accumulation**. *(Product rule, all three must hold at once: OI Change 1h above +3%, RVOL 1h above 1.5×, and |Change 1h| below 1%. Sorted by OI Change 1h descending.)*

**Confirm with:**
- **VDELTA (1h)** — positive means the new positions came from aggressive buying.
- **VOLUME (1h)** for the liquidity floor.
- **TREND** — the 4-hour sparkline should look flat or gently sloped. If it looks like a cliff followed by a shelf, "flat" only means the move already finished.

**Invalidated by:** the price breaking out and CHANGE (1h) rising past 1% — at which point this is no longer the setup you screened for — or OI CHANGE (1h) turning negative.

**Timeframe:** hours. Build-ups resolve slowly or not at all.

**Risk note:** flat price plus rising open interest is a *description*, not a direction. It is equally consistent with a large seller distributing into steady demand. VDelta is your only clue about which, and it is a weak one.

---

## 4. Open-interest spike

**Hunting:** a sudden inflow of new positions, whether or not the price has reacted yet.

**Set it up:** click **OI Spike**. *(Product rule: the OI Change 1h percent leg above +5%, growth only — a −20% unwind does **not** match. Sorted by that percentage descending.)*

**Confirm with:**
- **CHANGE (1h)** — small means the positions were opened quietly; large means they were opened into a move that is already running.
- **FUNDING RATE** — if funding is stretching in the same direction as the price, the new positions are the crowded side.
- **VOLUME (1h)** for liquidity.

**Invalidated by:** the percent leg falling back below +5% on the next samples, or the price making a full round trip while open interest stays high (trapped positions, not fuel).

**Timeframe:** hours.

**Risk note:** open interest is sampled every five minutes and the change windows stretch — "OI Change 5m" can span anywhere from roughly 2.5 to 10.5 minutes. Treat OI percentages as approximate and prefer the 1h leg for decisions.

---

## 5. Compression before expansion

**Hunting:** a coin that is unusually quiet *and* unusually one-sided — the shape that sometimes precedes an expansion.

**Set it up:** click **Breakout**. *(Product rule, all four must hold: VOLATILITY (5m) above 0 and below the median VOLATILITY (5m) of the whole streamed market; RVOL 5m at least 1.20; VOLUME (5m) — the last closed 5-minute candle — at least $50,000; and |VDelta 5m| ÷ Volume 5m above 0.20, meaning more than a fifth of that candle's turnover was net directional. Sorted by that ratio descending.)*

**Confirm with:**
- The **sign of VDELTA (5m)** — that is the chip's only directional information, and it is one candle old.
- **VOLUME (1h)** for liquidity, and **CHANGE (1h)** to check the expansion has not already started.

**Invalidated by:** volatility expanding without the price going anywhere (the compression released into chop), or the VDelta ratio collapsing on the next candle.

**Timeframe:** minutes to an hour.

**Risk note:** the volatility bar is the *universe median*, which moves with the market. The same coin can enter and leave this chip without changing at all, because everything else got calmer or noisier. Never read chip membership as an event.

---

## 6. Crowded book starting to hurt

**Hunting:** one side of the market heavily positioned while the price moves against it — a squeeze in progress.

**Set it up:** click **Squeeze**. *(Product rule: |funding| above 0.15% **and** the price moving against the crowded side by more than 1% over the last hour. Positive funding with Change 1h below −1% means longs are being squeezed; negative funding with Change 1h above +1% means shorts are. Sorted by |funding| descending.)*

**Confirm with:**
- **OI CHANGE (1h)** — a negative percent leg means positions are actually being closed. That is the squeeze physically happening rather than merely being possible.
- **VOLUME (1h)** and **VDELTA (1h)** — a real squeeze is loud and one-sided.

**Invalidated by:** funding normalising toward zero, open interest flattening out, or the price turning back in the crowd's favour.

**Timeframe:** hours.

**Risk note:** squeezes are violent in both directions and the crowded side is crowded for a reason. This recipe finds a mechanism, not a bottom.

---

## 7. Positioning watchlist

**Hunting:** extreme funding *before* anything has happened — a list to keep an eye on rather than a trade.

**Set it up:** click **High Funding**. *(Product rule: |funding| above 0.1%, bi-directional. Sorted by |funding| descending.)* Star the survivors so they sit in your favourites block.

**Confirm with:**
- **VOLUME (1h)** — extreme funding is easiest to find exactly where it is least tradable.
- **OI CHANGE (1h)** and **CHANGE (24h)** — is the crowd growing or already unwinding, and has the price already paid for it?

**Invalidated by:** funding drifting back toward the middle of the pack. Funding refreshes about once an hour, so this list changes slowly.

**Timeframe:** a day or more.

**Risk note:** funding is a percent per funding period exactly as Binance publishes it for that contract. ErkeScan does not annualise it and does not convert between contracts with different funding intervals, so compare like with like and do not multiply the number out in your head.

---

## 8. Attention leaders

**Hunting:** where trading attention is concentrated right now, among coins that are genuinely liquid.

**Set it up:** click **Top Active 10**. *(Product rule: from coins that pass the shared liquidity floor — at least $500,000 of VOLUME (1h) **and** a primary-path RetailHeat value, which needs the last closed 5-minute candle to have traded at least $50,000 — take the ten with the highest TICKS (5m).)*

**Confirm with:**
- **RETAILHEAT (5m)** and its percentile — trades per $1 million of the last closed 5-minute candle's turnover. High means many small trades, low means fewer and larger ones.
- **VOLUME (5m)** and **CHANGE (1h)** to see whether the attention is attached to a move.

**Invalidated by:** nothing — this is a ranking, not a signal. It is invalid only as a trade idea taken on its own.

**Timeframe:** now. Rebuilt on every data tick.

**Risk note:** fewer than ten rows is normal and deliberate on calm days; the product would rather show you a short honest list than pad it. Coins whose RetailHeat carries an asterisk are excluded from this chip by design.

---

## 9. Rotation board

**Hunting:** the day's liquid winners and losers, as a shortlist for mean-reversion or continuation work.

**Set it up:** click **Top Gainers 1D** or **Top Losers 1D**. *(Product rule: the same shared liquidity floor as Top Active 10, plus |Change 24h| of at least 1.5% and the correct sign. Top ten by Change 24h.)*

**Confirm with:**
- **CHANGE (1h)** — is the move still running, or did it finish six hours ago?
- **VOLUME (24h)** and **RVOL (1h)** — is today unusual for this coin, or just a normal day with a direction?
- **BTC CORR (1d)** — did it lead the market or follow it?

**Invalidated by:** CHANGE (1h) reversing sharply against the 24-hour direction on rising volume.

**Timeframe:** the rest of the day.

**Risk note:** despite the "1D" chip label, the underlying number is the **rolling 24 hours** — the same field the table shows as **CHANGE (24h)**. It is not a calendar day and it does not reset at midnight anywhere.

---

## 10. Coins moving on their own story

**Hunting:** a mover that is not simply doing what Bitcoin does — useful when you want exposure to a specific narrative rather than to market beta.

**Set it up:** start from **Big Movers** or **High Volume**, then read **BTC CORR (1h)** on each survivor. *(Rule of thumb: treat values between −0.3 and +0.3 — the ones the table renders in muted grey — as "moving independently", and values above 0.7, rendered green, as "moving with the market".)*

**Confirm with:**
- **BTC CORR (1d)** as well as 1h, so you know whether the independence is a moment or a regime.
- **VOLUME (1h)**, always.

**Invalidated by:** correlation climbing back toward 1.0, which usually means BTC started moving and swallowed everything else.

**Timeframe:** hours.

**Risk note:** correlation needs at least three paired candle returns to be computed at all, so thin or newly listed contracts show "—" rather than a number. A dash here is not independence — it is no data. And correlation says nothing about *direction* of causality.

---

## 11. Quiet-market routine: build a watch, then walk away

**Hunting:** nothing, deliberately. This is what you run when the chips are empty and there is no trade on the screen.

**Set it up:**
1. Click **Top Active 10** and star the coins you actually trade. They are liquid by construction.
2. Turn off every column your questions do not use, so the favourites block reads at a glance. See [personalise your screener](personalize.md).
3. Turn the thresholds you care about into [custom alerts](../alerts/create-an-alert.md) — for example **Volume (5m)** above a dollar figure, or **Change (1h)** beyond a percentage, on each starred coin.
4. Close the tab.

**Confirm with:** nothing. The alert is the confirmation, and it arrives in Telegram — normally with a 15-minute chart image attached, and as plain text if the image cannot be fetched.

**Invalidated by:** an alert that fires so often it becomes wallpaper. If that happens, raise the threshold rather than muting yourself to it.

**Timeframe:** days.

**Risk note:** you can hold a maximum of **200 alerts** on your account, the same on every plan. Spend them on coins you would genuinely trade, and delete the rest — see [managing alerts](../alerts/managing-alerts.md).

---

## 12. High-volatility routine: triage by liquidity first

**Hunting:** a way through a day when everything is moving and every chip returns a wall of rows.

**Set it up:**
1. **Do not** start from Big Movers. On a violent day |Change 1h| above 3% is most of the table and the chip stops discriminating.
2. Start from **Top Gainers 1D** / **Top Losers 1D** instead. They are hard-capped at ten rows and gated on liquidity, so they degrade gracefully when the market does not.
3. Sort **VOLUME (1h)** descending with the caret and work from the top down. On a violent day, liquidity is what decides whether you can act at all.
4. Read **BTC CORR (1h)** before you form any thesis. If it is high across the board, you are looking at one trade in many costumes.
5. Use **RETAILHEAT (5m)** and its percentile to separate crowded retail chases from blockier flow.

**Confirm with:** **OI CHANGE (1h)** on each candidate — cascades show up as open interest falling fast while price runs.

**Invalidated by:** the connection warning strip appearing above the table. Violent days are exactly when feeds struggle, and a frozen price during a cascade is the most expensive number in the product. See [troubleshooting](troubleshooting.md).

**Timeframe:** the session.

**Risk note:** spreads and slippage on a cascade day bear no resemblance to a calm one, and none of it is visible in the screener. The table shows the last traded price, not what you would get filled at.

---

## Choosing between them

| If you want to… | Start with |
|---|---|
| Catch something in the next few minutes | 1 Fresh volume surge, 5 Compression |
| Work an idea over the next few hours | 2 Hourly momentum, 3 Quiet build-up, 4 OI spike, 6 Squeeze |
| Build a list for tomorrow | 7 Positioning watchlist, 8 Attention leaders, 9 Rotation board |
| Filter out market beta | 10 Own story |
| Survive a dead market | 11 Quiet-market routine |
| Survive a violent one | 12 Liquidity-first triage |

{% hint style="warning" %}
None of these recipes is a strategy, a signal or a tested edge. They are ways of asking the data a specific question. Every one of them will produce losing candidates, several will produce mostly losing candidates in the wrong market regime, and none of them accounts for spread, slippage, funding cost or your own execution. What you do with a row is your decision and your risk.
{% endhint %}

**Next:** [From screen to trade](from-screen-to-trade.md) — the chain from a row to a decision, with worked examples and sizing arithmetic.
