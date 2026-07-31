# Build your own filters

The eleven [quick filters](quick-filters.md) answer eleven questions. This page teaches you the method for answering your own — how to turn a vague market question into a repeatable screen you can run in under a minute, using the tools ErkeScan actually gives you.

Terms used below — [RVOL](../glossary.md), [VDelta](../glossary.md), [open interest](../glossary.md), [funding rate](../glossary.md), [RetailHeat](../glossary.md) — are defined in the [glossary](../glossary.md).

{% hint style="info" %}
**There is no saved-filter builder in ErkeScan.** You cannot define "volume > X and funding < Y" and save it under a name. What you have instead is: the 11 quick-filter chips, sorting by any column, the search box, favourites, your saved column layout, and [custom alerts](../alerts/how-alerts-work.md) for anything you want watched while you are away. Used deliberately, that is enough for most screens. Used carelessly, you will read the wrong number and never know it.
{% endhint %}

## The six tools you are actually working with

| Tool | What it does | Saved? |
|---|---|---|
| **Quick-filter chip** | Applies one fixed rule to the whole universe. One at a time — they never combine. | No, resets on reload |
| **Caret sort** | Orders the table by any column except **TREND**, which has no sort. Use the small caret beside the header label, **not** the label itself. | No, resets on reload |
| **Search box** (`Search...`) | Case-insensitive substring match on the symbol only. | No |
| **Favourites** | Pins chosen coins into their own block above everything else. | Yes, in this browser |
| **Column layout** | Which columns are visible, in what order, at what density. | Yes, in this browser |
| **Custom alerts** | Watches a threshold for you and messages you in Telegram. | Yes, on your account |

Two consequences follow. First, because chips are single-select, a "filter" in ErkeScan is usually **one chip plus one sort plus your own eyes on two or three confirming columns**. Second, because neither the chip nor the sort survives a page reload, everything you want to keep has to live in the column layout, the favourites list or your alerts — so build those deliberately.

## The method

### 1. State the question in one sentence

Write it down before you touch the screen. A good question names a behaviour and a horizon: *"Which liquid coin is having money pushed into it right now without the price having moved yet?"* A bad question is a mood: *"What looks good?"*

The sentence matters because it forces you to pick a horizon. Five-minute questions and one-day questions use different columns, and mixing them is the single most common way to build a screen that never works.

### 2. Choose one trigger metric — and learn its window

The trigger is the one thing that must be unusual for the row to interest you. Everything else is confirmation.

Pick it from the [column reference](column-reference.md), and read the window before you use it. ErkeScan's column families are deliberately non-uniform, and the header label names the candle size, not always the look-back:

| Trap | The truth |
|---|---|
| **CHANGE (5m)** / **(15m)** | Not a rolling window. It is the move since the last 5-minute / 15-minute bar boundary, so at ten seconds past the boundary it describes ten seconds. |
| **CHANGE (1h)** | Genuinely rolling 60 minutes. |
| **CHANGE (24h)** | Genuinely rolling 24 hours, not a calendar day. |
| **VOLUME (15m)** / **(1h)** | Sums of the last 3 and last 12 *closed* 5-minute candles. They step every 5 minutes. |
| **VOLATILITY (1h)** | The spread of 1-hour candle returns over the retained 20-candle buffer — a look-back of roughly 20 hours. **VOLATILITY (5m)** looks back roughly 100 minutes. |
| **RVOL (15m)** | The only RVOL leg built from the still-forming candle. It reads near zero just after each 15-minute boundary and climbs through the bar. |
| **RVOL (1h)** | Not "the last closed hourly candle". The numerator is the trailing 60 minutes assembled from twelve closed 5-minute candles, and the baseline comes from the hourly candle buffer — two different candle series. It re-steps every 5 minutes and is an approximation on both legs. The column's own tooltip describes it wrongly; trust the [column reference](column-reference.md). RVOL 5m is the one leg built entirely from a single closed-candle series. |
| **BAR VOL Δ% (5m/15m/1h)** | Bar progress, not a market move. Every symbol sits near −100% at the start of every bar. The 8h and 1d legs are different — they compare two completed bars. |
| **OI CHANGE (5m)** | Open interest is sampled every five minutes, so this window stretches; it can cover anywhere from about 2.5 to 10.5 minutes. |
| **FUNDING RATE** | A percent per funding period as Binance publishes it for that contract. ErkeScan does not annualise it and does not normalise different funding intervals to a common period. |

### 3. Always add a liquidity floor

A screen without a liquidity floor will hand you a coin that moved 40% on $9,000 of turnover. You cannot get in, you certainly cannot get out, and the metric that excited you was noise.

ErkeScan's own three top-N chips — Top Active 10, Top Gainers 1D and Top Losers 1D — apply what [Quick filters](quick-filters.md) calls the **shared liquidity floor**: at least **$500,000 of volume in the last hour**, read from **VOLUME (1h)**, *and* a primary-path RetailHeat value, which requires the last closed 5-minute candle to have traded at least **$50,000**. That pair is a reasonable floor to borrow, and it is the one the product itself trusts.

The other eight chips do not apply it. Only **Breakout** carries any volume condition of its own, and it is the $50,000 single-candle one, not an hourly figure. So if your screen starts from High Volume, OI Spike, Big Movers, High Funding, Accumulation, Squeeze or Breakout, **the hourly floor is your job**: turn on VOLUME (1h) and check it on every row before you look at anything else.

{% hint style="warning" %}
Dollar volume, not percentage. A 3× RVOL reading on a coin doing $40,000 an hour is still $40,000 an hour. RVOL tells you a coin is busier than usual; only VOLUME tells you whether "busy" is a size you can trade.
{% endhint %}

### 4. Add a confirmation from a different family

One metric moving is an observation. Two metrics from different families moving together is a story. Confirmation is worth most when it comes from a family your trigger cannot mechanically drag along with it.

| Family | Columns | What it tells you |
|---|---|---|
| **Price** | CHANGE %, CHANGE $, TREND, VOLATILITY | Whether the move has happened yet, and how big |
| **Volume** | VOLUME, RVOL, TICKS, RETAILHEAT | Whether anyone is actually trading it, and who |
| **Open interest** | OPENINTEREST, OI CHANGE | Whether positions are being opened or closed |
| **Positioning** | FUNDING RATE, VDELTA | Which side is crowded and which side is paying |
| **Context** | BTC CORR | Whether this is the coin's own story or the whole market's |

Two pairings do most of the work:

- **Price + open interest.** Price up with open interest up means new positions are being opened into the move. Price up with open interest falling means somebody is closing — often shorts covering, and often near the end.
- **Volume + VDelta.** VOLUME tells you how much traded; **VDELTA** tells you how much of it was net taker buying (positive, green) or net taker selling (negative, red), in dollars. Large volume with VDelta near zero is a fight, not a direction.

### 5. Add a disqualifier

Decide what must **not** be true. This is what turns a list into a screen. Useful disqualifiers:

- **A dash in a column you are relying on.** "—" means no data, not zero. If VDELTA (5m) is a dash, you have no directional read on that bar — do not substitute your imagination.
- **An asterisk on RETAILHEAT (5m).** The asterisk means the last closed 5-minute candle was thin ($5,000–$50,000) and the value was smoothed over the longer ~100-minute volume window. It is a hint, not a measurement, and ErkeScan's own three top-N chips exclude those rows.
- **The move already happened.** If CHANGE (24h) is already +38%, a fresh 5-minute volume spike is more likely to be the exit than the entry.
- **A stale connection.** If the warning strip is showing above the table, no row on screen is a fact. See [troubleshooting](troubleshooting.md).

### 6. Sanity-check it on a quiet day and on a violent day

A screen is only useful if you know what it does at both ends of the market's range. Run yours twice, deliberately:

- **On a quiet day** (weekend afternoons are good). How many rows come back? If a screen returns nothing on a quiet day, that is often correct behaviour — ErkeScan's top-N chips are explicitly built to return fewer than 10 rows rather than pad the list. But if it returns nothing on a *normal* day too, your thresholds are simply unreachable.
- **On a violent day** (a large BTC move, a macro release, a liquidation cascade). Does it come back with 200 rows? A screen that matches everything is telling you nothing. On those days, tighten with the liquidity floor first and the trigger threshold second, and check **BTC CORR (1h)** — when most of the table is moving together, the "signal" you found is beta.

Write both results down next to the screen's one-sentence question. That pair of observations is what makes it reusable next month.

### 7. Decide in advance what makes the screen invalid

Screens rot. Decide now what would retire this one:

- The threshold stops discriminating (everything matches, or nothing ever does).
- The behaviour it was built for stops paying, and you have the notes to prove it.
- The underlying column changes meaning. ErkeScan's field definitions have been corrected over time; a threshold you wrote against a column a year ago may be on a different scale today. If a screen suddenly matches everything or nothing after months of stability, re-read the column's window in the [column reference](column-reference.md) before you re-tune it.

## Running a screen without a filter builder

**Narrow with a chip.** Pick the chip whose rule is closest to your trigger. Selecting a chip clears whatever sort you had.

**Then sort with the caret.** Click the small caret to the right of a header label — the label itself is the drag handle for reordering, and clicking it will not sort. First click is **ascending**, second is **descending**, and it alternates from there; you cannot clear a sort by clicking. So: to put the biggest positive numbers on top, click twice. To put the most negative on top, click once. Rows showing "—" sink to the bottom whichever direction you choose, and never pretend to be 0.

**Use the search box as a manual filter.** It matches a substring of the symbol only. Because symbols are stored as pairs like `BTC/USDT`, typing `usdt` or `/` matches essentially every row, and `btc` also matches BTCDOM. It is excellent for jumping to a coin and useless as a category filter.

**Promote survivors to favourites.** The checkbox inside the Symbol cell (the star on mobile) pins a coin into its own block at the top of the table. That block is your working shortlist — it survives reloads in this browser, but it does not sync to your phone, and a favourited coin still has to pass the active chip and the search box to be shown.

**Build the column layout the screen needs.** Turn off everything your question does not use. A screen with eight relevant columns is read in three seconds; the same screen with all 57 columns is read never. See [personalise your screener](personalize.md).

**Hand the waiting to an alert.** You cannot sit on the table all day. Convert the trigger into a [custom alert](../alerts/create-an-alert.md) and let it find you.

{% hint style="warning" %}
Alerts cover a smaller field set than the table. You can alert on Change, Price, Volume, VDelta, Volatility, Ticks, Open Interest, OI Change and Funding Rate. You **cannot** alert on RVOL, RetailHeat, Change$, Bar Vol Δ or BTC Correlation. When your trigger is one of those, alert on the raw ingredient underneath it — for an RVOL 5m idea, alert on **Volume (5m)** in dollars; for a RetailHeat idea, alert on **Ticks (5m)**. Also skip **Change (8h)** as an alert condition: the alert engine reads a different, near-zero field than the column shows, so it will not match what you see.
{% endhint %}

---

## Worked example A — "Is anyone building a position quietly?"

**1. The question.** *Which liquid coin has had open interest grow meaningfully in the last hour while the price barely moved?* Horizon: hours.

**2. The trigger.** **OI CHANGE (1h)** — the percent leg, the small number in parentheses. Growth, not just movement.

**3. The liquidity floor.** **VOLUME (1h)** ≥ $500,000. *(Product rule for the top-N chips; here you are applying it by eye.)*

**4. The confirmation.** From a different family: **RVOL (1h)** above 1.5× says the hour looks busier than this coin's own recent average, so the OI growth is not one lonely order. Read it as a rough "busier than usual", not an exact multiple — see the RVOL (1h) row in the trap table above. Then **VDELTA (1h)**: if it is meaningfully positive, the new positions are being opened by aggressive buyers.

**5. The disqualifier.** **|CHANGE (1h)| under about 1%.** If the price has already run, this is no longer accumulation — it is participation in a move that started without you. Also disqualify any row where OI CHANGE (1h) or VDELTA (1h) shows a dash.

**6. Run it.**

1. Click the **Accumulation** chip. Its built-in rule is exactly the shape above: OI Change 1h above +3%, RVOL 1h above 1.5×, and |Change 1h| below 1%. The list arrives sorted by OI Change 1h descending.
2. Turn on **VOLUME (1h)** and **VDELTA (1h)** in the Columns panel if they are not already visible, and drop rows below your liquidity floor.
3. If the chip returns nothing — common on quiet days, because all three legs must hold at once — go back to **All**, sort **OI CHANGE (1h)** descending with the caret, and read down the list applying your own, looser numbers by eye. This is the manual version of the same screen, and it is how you widen a chip you cannot edit.

**7. Quiet day / violent day.** On a quiet day expect zero to three rows; that is the screen working. On a violent day expect the chip to be dominated by coins whose price *did* move and then came back to flat — check the **TREND** sparkline before you call anything quiet.

**8. Invalidation.** The idea dies when open interest stops growing, when the price breaks hard in either direction (the build-up resolved without you), or when VDelta flips sign for a sustained period.

---

## Worked example B — "Where is one side of the book crowded and starting to hurt?"

**1. The question.** *Which coin has an extreme funding rate while the price is moving against the crowd?* Horizon: hours to a day.

**2. The trigger.** **FUNDING RATE**. Positive means longs are paying shorts — longs are the crowded side. Negative means the reverse. The number is a percent per funding period as Binance publishes it for that contract.

**3. The liquidity floor.** **VOLUME (1h)**, same as before. Extreme funding is easiest to find on illiquid contracts, which is exactly where it is least tradable.

**4. The confirmation.** **CHANGE (1h)** moving *against* the crowded side — price falling while funding is positive, or rising while funding is negative. That is the crowd being tested rather than being right. Then **OI CHANGE (1h)**: a negative percent leg means positions are being closed, which is what a squeeze physically is.

**5. The disqualifier.** Funding extreme but price agreeing with the crowd. That is a trend with an expensive carry, not a squeeze, and fading it is fighting the flow.

**6. Run it.**

1. Click **Squeeze**. Its rule: |funding| above 0.15% **and** the price moving against the crowded side by more than 1% over the last hour. Sorted by |funding| descending.
2. Read **OI CHANGE (1h)** on every survivor. Negative and getting more negative is the confirmation you want.
3. To hunt earlier, click **High Funding** instead. That chip only requires |funding| above 0.1% and says nothing about price — it is a watchlist builder, not an entry. Star the interesting ones and check back.

**7. Quiet day / violent day.** On quiet days Squeeze is often empty, because extreme funding is rare and the counter-move leg is rarer. On violent days it can fill with coins whose funding is extreme *because* of the move you already missed; the OI-falling check is what separates those.

**8. Invalidation.** Funding normalises toward zero, open interest stops falling, or the price resumes in the crowd's direction. Any of the three and the mechanism you were trading is gone.

---

## The five mistakes that break home-made screens

1. **Mixing horizons.** A 5-minute trigger confirmed by a 20-hour volatility reading is not confirmation.
2. **Trusting a percentage without a dollar figure.** Always pair RVOL with VOLUME.
3. **Reading a dash as a zero.** It is not. It is silence.
4. **Sorting a bar-progress column.** BAR VOL Δ% (5m/15m/1h) sorts the universe by where it is in the current bar, which is the same for everybody.
5. **Not writing the screen down.** If it lives only in your hands, you cannot tell whether it stopped working or you stopped running it the same way.

{% hint style="warning" %}
Every screen on this page finds *candidates*, not trades. A row that passes six filters is a row that deserves a chart and a thesis — nothing more. Nothing here is investment advice, no threshold is an edge, and the decision and the risk are yours.
{% endhint %}

**Next:** [Filter recipes](recipes.md) — twelve ready-made screens with exact settings, confirmations and risk notes.
