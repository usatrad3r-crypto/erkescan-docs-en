# First steps

Fifteen minutes, seven steps, on a real live table. By the end you will have filtered the market, sorted it your way, built a small watchlist, opened a coin's chart and created your first alert.

Do this on a desktop or laptop. On a phone the screener drops the table entirely and shows a card list with five values per coin — price, change 15m, change 1h, volume 1h and funding rate — so there are no column headers and step 4 has nothing to click. Everything else works on a phone, and the differences are called out as you go.

## 1. Open the screener

Go to **https://app.erkescan.com/screener**, or press **Screener** in the header. The site root goes to the same place.

**What you should see:** the header, a search box, a strip of filter chips, a **Columns** button and an **Alert** bell button on the right, and a wide table of coins. The table starts in feed order — no column is sorted yet.

About 2.5 seconds after the page settles, a short four-step tour opens by itself and highlights the table headers, the filter chips, the alerts bell and the Columns button. Step through it with **Next**, or dismiss it with **Skip**, **Got it!**, the X, the Escape key or a click on the dimmed background. It only appears once per browser. To see it again, load the page with `?tour=1` on the end of the URL. On a phone any step whose target is not on screen is dropped, so the tour is shorter there.

{% hint style="info" %}
The tour's first step says to click a column header to sort. That is not how sorting works — see step 4. Trust this manual on that point.
{% endhint %}

## 2. Let it connect

Look at the connection indicator in the footer, under the table.

| What the indicator says | What it means |
|---|---|
| **Loading market data...** (gold, pulsing) | The first snapshot is still arriving. Normal for a moment |
| **Connected** with a green dot | The live stream is running. This is the healthy state |
| **Connected** with a **gold** dot | The live stream failed and the app is polling instead. Hover it and the tooltip reads *Polling*. Data still updates, just less smoothly |
| **Reconnecting...** (gold, ping animation) | A new live connection is being opened |

If the data actually goes stale, a warning strip appears **above the table** — not just a coloured dot. It shows up when no fresh snapshot has been accepted for over 30 seconds, or when prices across the whole market have stopped advancing for over 60 seconds, and it escalates after two minutes without data.

{% hint style="danger" %}
Never act on a price while that strip is showing. A frozen table looks exactly like a quiet market. Reload the page and wait for the green dot before you judge anything.
{% endhint %}

Numbers refresh as new exchange data arrives, at most once every couple of seconds — not on a fixed metronome. A calm market genuinely does sit still for a while.

## 3. Try one quick filter chip

Click **Big Movers** in the chip strip.

**The rule:** the coin's [Change (1h)](../glossary.md) — its rolling 60-minute price change in percent — is more than 3% away from zero, in either direction. A coin down 6% in the hour qualifies just as much as one up 6%.

**What you should see:** the table shrinks to the matches and re-sorts itself by the size of that 1-hour move, biggest first. The counter next to the chips changes from a single number (how many coins have data at all) to *matched / total*.

Things to know before you go chip-hunting:

- The chips are **single-select**. Clicking another one replaces this one; there is no combining.
- Selecting any chip other than **All** **clears your column sort** and applies the chip's own sort instead. Filter first, sort second — not the other way round.
- An empty chip is a real answer, not a bug. On a quiet afternoon *Big Movers* can legitimately match nothing, and you get *"No tokens match this filter."*

Click **All** to return to the full market. All eleven chips and their exact rules are in [Quick filters](../screener/quick-filters.md).

## 4. Sort a column with the caret

**Desktop only** — a phone shows cards, not columns, so there is nothing to sort. Skip to step 5 there.

Make sure the **All** chip is selected, so your sort will survive.

Now look closely at a column header — try **VOLUME (5m)**. There are two controls there:

- the **header label** itself, which is a **drag handle**. Press and drag it sideways to move the column. Clicking it does not sort;
- a small **caret button** just to the right of the label. That is the sort control.

Click the caret once: **ascending**. Click again: **descending**. Every further click alternates. Sorting is single-column — a new sort replaces the previous one — and once you have sorted, clicking cannot return the table to "unsorted"; sort another column, or reload the page.

**What you should see:** with **VOLUME (5m)** descending, the top of the table is the coins that traded the most US dollars during the **last closed 5-minute candle**. Coins with no value for that column show a dash (**—**) and sink to the bottom in both directions — they never pretend to be zero.

Hover any header for a moment and a tooltip explains that column's measurement window. Read them — several column names are shorter than the truth. The [Column reference](../screener/column-reference.md) is the full dictionary, and it is the authority wherever a tooltip and this manual disagree.

## 5. Favourite two coins

Type `btc` into the search box (placeholder **Search...**). It matches on the symbol only, as a plain case-insensitive substring, filtering as you type. Symbols are stored as pairs like `BTC/USDT`, so `btc` also brings up BTCDOM, and typing `usdt` matches almost everything.

**On desktop:** each row's Symbol cell has a small checkbox. Tick it.
**On a phone:** each card has a star button in its top-right corner. Tap it — tapping the star does not open the coin.

Do that for two coins, then clear the search box.

**What you should see:** your favourites are lifted out of the list into their own block at the very top, above an accent-coloured divider, with a highlighted row style. The footer gains a *· 2 starred* note.

Two limits worth knowing now rather than later:

- Favourites live in **this browser only**. There is no cross-device watchlist and no server copy — a different laptop starts empty.
- A favourited coin still has to pass the active chip and the search box to be displayed. Favouriting does not pin a coin through a filter.

## 6. Open a coin's chart

Click the **ticker text** in any row.

**What you should see:** a chart window opens over the page — a TradingView chart of that coin's Binance perpetual, 15-minute candles, dark theme. Close it with **Escape**, the **×**, or a click outside it. A **Full Page →** link opens the same symbol on its own page in a new tab.

On a phone there is no modal: tapping a card takes you straight to that symbol's page.

This is a price chart to sanity-check what the row is telling you — is the move a clean impulse, or a wick that has already been faded? Deeper analysis lives in [From screen to trade](../screener/from-screen-to-trade.md).

## 7. Create one alert

Alerts are how the screener reaches you when you are not looking at it.

1. Press the **Alert** button with the bell icon, at the top right next to **Columns**. A panel opens on the right — on a phone the same panel slides up from the bottom. On a first visit the bell is ringed in gold with a small hint, *Set up your alerts here*; dismiss it.
2. In the **Alerts** tab press **Create New Alert**.
3. Give the alert a **name** — at least two characters. Make it descriptive; the name is the headline of every message you will receive from it.
4. Find the **Change** group and the **1h** row. Choose the operator **>** and type `3` as the value. Digits and a decimal point only — no `%`, no `$`, no commas.
5. Save.

**What you should see:** a confirmation that the alert was created and is now active, and the count badge on the bell going up by one.

What you just built, in plain terms: *tell me whenever any coin's rolling 1-hour change goes above +3%.* Note what is **not** in that sentence:

- **No coin.** An alert has no symbol picker. It is evaluated against every Binance USDT-margined perpetual and fires per matching coin, each as its own Telegram message.
- **No timeframe picker.** Each metric has one fixed window — `Change (1h)` is always the rolling hour.
- **No channel picker.** Telegram is the only delivery channel.

If you add a second condition, both must be true for the **same coin at the same moment** — conditions are ANDed, not ORed.

After an alert fires on a coin it goes quiet for that coin for the cooldown period, 60 minutes by default. The same alert can still fire on a different coin immediately. Your account can hold up to **200 alerts** in total.

{% hint style="warning" %}
A loose threshold on a fast metric can match dozens of coins in one pass and send you dozens of messages. Start deliberately tight, watch it for a day, then relax it. [Alert recipes](../alerts/alert-recipes.md) gives thresholds that do not spam.
{% endhint %}

Alerts can only be delivered once your Telegram chat is linked. If you skipped that, the alert is still saved and starts firing by itself the moment the link exists — see [Connect integrations](connect-integrations.md).

## Where to go from here

- Learn the screen properly: [Screener tour](../screener/tour.md) and [Reading the table](../screener/reading-the-table.md).
- Make it yours — columns, order, density, favourites: [Personalise the screener](../screener/personalize.md).
- Turn a row into a decision: [From screen to trade](../screener/from-screen-to-trade.md).
- Something looks wrong? [Troubleshooting](../screener/troubleshooting.md).

{% hint style="info" %}
Everything in this manual is a description of a data tool, not trading advice. The screener tells you what is happening in the market right now; what you do about it, how much you risk and where your stop goes are your decisions alone.
{% endhint %}

---

**Next:** [Screener tour](../screener/tour.md) — every part of the screen, named and explained.
