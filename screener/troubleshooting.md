# Troubleshooting

The problems people actually hit with the screener, why each one happens, and what to do. Most of them are the product behaving as designed — knowing which is which saves you from "fixing" something that is not broken.

## The table is empty or stuck on "Loading market data..."

**Why.** The first version of the page is rendered on the server, and that render gives up after a couple of seconds so the page does not hang. If it times out, you get an empty table and the **Loading market data...** state while the browser opens its own live connection. The rest of the data arrives over a live stream a moment later.

**What to do.**

1. Wait a few seconds. This normally resolves itself without any action.
2. Reload the page.
3. If the table is still empty after a reload and the footer does not reach **Connected**, check your own network first — corporate networks, VPNs and aggressive ad blockers can block the live stream.
4. If everything else on the internet works and the screener still will not fill, [contact support](../reference/support.md).

If the table shows **No results.** rather than the loading text, the page loaded fine but nothing came back — treat it the same way.

## A chip returns nothing: "No tokens match this filter."

**Why.** Usually because the chip is doing its job. Several chips require multiple conditions to hold **at the same instant**:

- **Accumulation** needs three: open-interest growth above 3% in the hour, RVOL 1h above 1.5×, and the price flat (|Change 1h| under 1%).
- **Breakout** needs four, including a compression test against the median VOLATILITY (5m) of the whole streamed market.
- **Squeeze** needs extreme funding **and** the price moving against the crowded side by more than 1%.

There are two additional reasons a row you expected does not qualify:

- **Missing data never counts as a match.** If a coin's Change 1h is unavailable, it cannot satisfy Accumulation's "flat price" test by accident. Nulls fail, they do not pass quietly.
- **Funding refreshes about once an hour.** The two funding chips (High Funding, Squeeze) change slowly by nature.

**What to do.** Nothing, if the market is quiet — an empty chip is honest information. If you want a looser version of the same idea, go back to **All**, sort the relevant column with the caret and read down the list yourself. That method is described in [Build your own filters](build-your-own-filters.md).

## Top Active 10 / Top Gainers 1D / Top Losers 1D show fewer than 10 rows

**Why.** By design. Those three chips apply a real, two-part liquidity gate — at least **$500,000 of VOLUME (1h)** *and* a last closed 5-minute candle that traded at least **$50,000**, which is what gives a coin a primary-path RetailHeat value. They would rather return four honest rows than pad the list to ten with coins you cannot trade. Gainers and Losers additionally require a rolling-24-hour move of at least 1.5% in the right direction, which simply does not exist for ten coins on a quiet day.

**What to do.** Nothing. A short list is the correct answer to a quiet market.

## Cells show "—"

**Why.** An em dash means **no data**, never zero. It appears when a value could not be computed or when a feed went quiet and the affected fields were deliberately blanked rather than left frozen at an old number.

Common specific causes:

| Column showing "—" | Most likely reason |
|---|---|
| **RETAILHEAT (5m)** | The last closed 5-minute candle traded under $5,000; or it was between $5,000 and $50,000 but the longer volume window was unusable; or the trade-count feed is unavailable |
| **TICKS (5m/15m/1h)** | The aggregate-trade feed has delivered nothing for two minutes; the whole trio blanks together |
| **VDELTA (any)** | One of the candles in the window is missing the buy/sell breakdown, so the split cannot be computed |
| **OI CHANGE (any)** | Not enough open-interest history yet for that window, or no valid starting sample |
| **BTC CORR (any)** | Fewer than three usable candle pairs — typical on thin or newly listed contracts |
| Anything else | That interval's candle feed went stale and the field was blanked |

**What to do.** Do not substitute a zero. If your decision rests on that column, you do not have the input — pick a different coin or wait for the value to return. Rows showing "—" sink to the bottom of the table whichever direction you sort, so they never masquerade as low or high values.

## RetailHeat shows a value with an asterisk

**Why.** The last closed 5-minute candle for that coin traded between $5,000 and $50,000 — thin. Rather than print a wild number from a nearly empty candle, ErkeScan smooths the calculation over the longer ~100-minute volume window and marks the result with an asterisk in a dimmed colour. Hovering the value on a desktop shows a note explaining it; there is no equivalent on touch, so on a phone the asterisk is unexplained.

**What to do.** Treat it as an indication, not a measurement. ErkeScan's own Top Active 10, Top Gainers 1D and Top Losers 1D chips exclude asterisked rows entirely, and so should your screens.

## A warning strip appeared above the table

**Why.** The page has decided the data can no longer be trusted, and says so where you cannot miss it. Two thresholds trigger it:

- **Stale** — no accepted update for about 30 seconds, **or** the newest price update from the upstream feed has not advanced for about 60 seconds. The second case is the dangerous one: updates keep arriving, but the numbers inside them are frozen.
- **Error** — about two minutes with no accepted update at all.

**What to do.**

{% hint style="danger" %}
**Do not act on a price while that strip is showing.** A frozen price during a fast move is the most expensive number in the product. Reload the page; if the strip returns immediately, check your connection, and if it persists across a reload on a working connection, [contact support](../reference/support.md) rather than trading around it.
{% endhint %}

## What the connection indicator in the footer means

| State | Appearance | Meaning |
|---|---|---|
| **Loading market data...** | Gold dot, pulsing | The first snapshot has not arrived yet |
| **Connected** | Green dot | The live stream is delivering data normally |
| **Connected** | **Gold** dot, tooltip reads **Polling** | The live stream is unavailable and the page is fetching updates on a timer instead |
| **Reconnecting...** | Gold dot | A new live connection is being opened; polling continues in the meantime |
| **Stale** | Warning strip above the table | Data has stopped advancing — see the section above |
| **Error** | Warning strip above the table | No accepted update for about two minutes |

The trap is the third row: **the word says "Connected" in both the healthy and the degraded case.** Only the colour and the hover tooltip tell them apart. Polling is a working fallback, not a failure — data still arrives, just less promptly — but if you are trading fast setups it is worth knowing which one you are on.

Reconnection attempts back off progressively, up to about half a minute between tries, so a stubborn reconnection can take a little while to recover on its own. A page reload usually shortcuts it.

## Columns I hid came back after reloading

**Why.** **Symbol** and **Trend** are forced visible every time the page loads. You can switch them off for the current session — including with a group **Hide All** — but they return on the next load. Similarly, **Trend** and **Price** are re-pinned immediately after **Symbol** on every load, so you cannot save a different position for those two.

**What to do.** Nothing; this is intentional. Every other column's visibility and order is saved.

## My layout is gone on another device, another browser, or after clearing site data

**Why.** Your column visibility, column order, table density and favourites are stored **in the browser you set them in**. They do not sync to your account, so they do not follow you to your phone, to another browser, or into a private window — and clearing site data removes them.

**What to do.** Set the layout up again on the device you actually work on, and keep to that device. If you want a specific set of columns permanently, note it down; rebuilding it from the Columns panel takes under a minute. To start clean deliberately, use **Reset Column Order & Visibility** at the bottom of the Columns panel.

Favourites have the same limitation: they are a per-browser list, not a synced watchlist.

## Clicking a column header does not sort — it drags

**Why.** The header **label** is the drag handle for reordering columns. Sorting is the **small caret button** immediately to its right.

**What to do.** Click the caret. First click sorts ascending, second sorts descending, and it alternates from there — so put the biggest values on top with two clicks. A sort cannot be cleared by clicking; select **All** and reload if you want to get back to the unsorted feed order. There is no multi-column sorting; each sort replaces the last. **TREND** is the one column with no sort at all.

## My sort disappeared when I clicked a chip

**Why.** Selecting any chip other than **All** clears your current column sort and applies that chip's own ordering — High Volume by RVOL 5m, Big Movers by the size of the hourly move, and so on.

**What to do.** Apply the chip first, then sort by whatever column you want. Doing it in that order keeps your sort.

## The search box matches everything

**Why.** The box does a plain substring match against the symbol, and symbols are stored as pairs like `BTC/USDT`. So typing `usdt` or `/` matches essentially every row, and `btc` also matches `BTCDOM`.

**What to do.** Search the base ticker only — `sol`, `arb`, `link`. And remember the search filters *within* whatever the active chip already selected; it does not search the whole universe while a chip is on.

## A coin I expected is not in the table at all

**Why.** Several possibilities, in order of likelihood:

1. **A chip is active.** Chips remove everything that does not match, including your favourites.
2. **It is not in the universe.** The screener covers **Binance USDT-margined perpetual futures only**. USDC-quoted pairs are removed before the table renders, and other exchanges are not covered.
3. **The row was withheld.** If a symbol has no valid price or its short-interval candle data is missing, the row is dropped entirely rather than shown with holes.
4. **It is in the faded block at the bottom** (see below) and you scrolled past it.

**What to do.** Click **All**, clear the search box, then scroll to the bottom before concluding it is missing.

## Rows at the bottom of the table are faded

**Why.** That is the no-data block. A row lands there when its price is not a positive number, **or** when it shows no volume in any of the five volume windows and no open interest either. Those rows are separated by a hairline and rendered at 40% opacity so they do not clutter the real list. The block only exists while the **All** chip is selected — any other chip removes those rows completely.

**What to do.** Ignore them. If a coin you care about is stuck there, it currently has no tradable data on this feed.

## The two counters disagree

**Why.** They deliberately count different things. The counter beside the chips reports rows that have data — and, when a chip is active, how many matched out of that total. The footer counter reports how many rows are in the list you are looking at, which under **All** includes the faded no-data rows.

**What to do.** Nothing. Use the chip counter for "how selective is this filter" and the footer for "how long is this list".

## On mobile I only get five values per coin

**Why.** Below 768 pixels the table is replaced by cards, and a card shows the price plus Change 15m, Change 1h, Volume 1h and Funding Rate — plus the metric the active chip sorts by, if it is not already one of those. That is the whole mobile column set, regardless of your desktop layout.

**What to do.** Use the chips, the search box and favourites on mobile, and do detailed column work on a desktop. The **Columns** and **Alerts** panels do open on mobile — they slide up from the bottom of the screen — but the card set is fixed, so changing column visibility there will not add a metric to a card. Drag-to-reorder and the row-density control are desktop-only.

## Numbers change when the market looks still

**Why.** Some columns are supposed to move on the clock rather than on the market:

- **BAR VOL Δ% (5m/15m/1h)** measures how far the current unfinished bar has filled against the previous one, so it sits near −100% for the whole board at every bar open and climbs back toward zero. That is bar progress, not a market event.
- **RVOL (15m)** is built from the still-forming candle, so it reads low right after each 15-minute boundary and rises through the bar. **RVOL (5m)** does not behave this way.
- **RVOL (1h)** re-steps every five minutes rather than once an hour: its numerator is a trailing 60 minutes assembled from twelve closed 5-minute candles. It moving is not the hour changing.
- **CHANGE (5m)** and **(15m)** measure the move since the last bar boundary, so they reset at every boundary.

**What to do.** Prefer the closed-candle columns for decisions. The [column reference](column-reference.md) marks the window of every one.

## An alert never fires even though the column crosses my level

**Why.** Two known causes.

- **The condition does not exist for alerts.** RVOL, RetailHeat, Change$, Bar Vol Δ and BTC Correlation are table-only — they cannot be alerted on. Alert on the underlying figure instead: Volume in dollars rather than RVOL, Ticks rather than RetailHeat.
- **Change (8h) is the exception you must avoid.** The alert engine evaluates a different field than the **CHANGE (8h)** column displays, and that field sits near zero for almost every symbol. An 8-hour change alert will effectively never fire and will not match what you see in the table. Use another timeframe.

**What to do.** See [managing alerts](../alerts/managing-alerts.md) for the full delivery checklist, and [create an alert](../alerts/create-an-alert.md) for the conditions that are actually available.

## "Alert limit reached"

**Why.** Every account can hold **200 alerts**, and the cap is the same on every plan.

**What to do.** Delete alerts you no longer watch, then create the new one. [Managing alerts](../alerts/managing-alerts.md) covers it.

## Coin logos are missing or show two letters

**Why.** Icons are loaded from third-party image sources. When one is unavailable, the cell falls back to a two-letter avatar.

**What to do.** Nothing — it is cosmetic and has no bearing on the data in the row.

## I dismissed the welcome tour and want it back

**Why.** The four-step tour runs once per browser and then remembers that you have seen it.

**What to do.** Load the screener with `?tour=1` on the end of the URL. That is the only way to replay it; there is no in-app restart button.

## I cannot open the screener at all

**Why and what to do**, in order:

1. **You are sent to the sign-in page.** You are not signed in. Sign in and you will be returned to the page you asked for.
2. **You see a subscription screen instead of the table.** You are signed in without an active subscription. The screener, the Charts page and the symbol pages all require one — see [choosing a plan](../getting-started/choose-a-plan.md). Pricing lives at **app.erkescan.com/pricing**.
3. **You believe you have paid but still see the subscription screen.** Check the **Subscription** entry in the account menu behind your avatar, which opens your billing page. If it disagrees with what you paid for, [contact support](../reference/support.md) with the payment details.

## Still stuck?

Use the **Contact us** button in the site header — it opens the ErkeScan support bot in Telegram. When you write in, include:

- what you were doing and which page you were on,
- the coin and the column, if it is a data question,
- what the connection indicator in the footer said at the time,
- your browser and whether you were on desktop or mobile.

That set of four turns a slow conversation into a fast one. More detail in [Support](../reference/support.md).

**Next:** [How alerts work](../alerts/how-alerts-work.md) — what an alert is, how the engine checks it, and where the message lands.
