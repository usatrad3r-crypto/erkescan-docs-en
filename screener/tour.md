# A tour of the screener

This page names every control on the screener screen and says what it does. Read it once with the app open in another tab, and nothing on the screen will be a mystery afterwards.

The screener lives at **app.erkescan.com/screener**. It is subscriber-only. If you are not signed in you are redirected to the sign-in page; if you are signed in without an active subscription you get an upgrade page instead of the table.

Every row is one Binance USDT-margined [perpetual futures](../glossary.md) contract. That is roughly 670 contracts, and about 140 of them are tokenized stocks and commodities rather than coins — they sit in the same table with the same columns. More on coverage in [Data and coverage](../reference/data-and-coverage.md).

---

## The top of the screen

### The search box

A single text field with the placeholder **Search...**. It filters the **SYMBOL** column only: a case-insensitive substring match, applied on every keystroke, with no minimum length and no "Enter" needed.

Symbols are stored as pairs like `BTC/USDT`, so the match runs against the whole pair string. Typing `usdt` or `/` therefore matches essentially every row, and typing `btc` also matches BTCDOM.

Search combines with everything else: a chip, your sort and your favourites all still apply while a search is active.

### The quick-filter chip row

Eleven chips, always in this order:

**All · High Volume · OI Spike · Big Movers · High Funding · Accumulation · Squeeze · Breakout · Top Active 10 · Top Gainers 1D · Top Losers 1D**

They are **single-select** — clicking one replaces the previous one. There is no way to combine two chips.

Choosing any chip other than **All** clears your current column sort and applies that chip's own ordering (for example **Big Movers** orders by the size of the 1-hour move).

{% hint style="info" %}
While any chip other than **All** is active, that chip's ordering wins. Clicking a sort caret changes the sort state, but the chip re-applies its own order on top, so the row order you see does not change. To sort by a column of your choice, go back to the **All** chip first.
{% endhint %}

The exact rule behind each chip, and why a chip can legitimately be empty, is in [Quick filters](quick-filters.md).

### The match counter

Next to the chips. With **All** selected it shows how many rows currently have data. With any other chip it shows `matched / total-with-data`.

{% hint style="info" %}
The counter beside the chips and the row count in the footer intentionally disagree. The footer counts every row in the list, which under **All** includes the greyed-out no-data rows at the bottom; the chip counter does not.
{% endhint %}

---

## The toolbar on the right

### Density

A three-way segmented control: **Compact**, **Default**, **Comfortable**. Compact packs more rows on screen with smaller type; Comfortable gives each row more air. It changes the desktop table only.

### The Columns button

Opens a panel on the right with two tabs, **Columns** and **Alerts**.

The **Columns** tab holds three one-click presets — **All**, **Defaults** and **Core Only** — then the 12 column groups (Core, Change %, Change $, Volume, RVOL, VDelta, Bar Vol Δ $, Bar Vol Δ %, OI Change, Volatility, Ticks, BTC Corr), each with its own **Show All** / **Hide All** and one chip per column. At the bottom sits **Reset Column Order & Visibility**.

All 57 columns are offered here; none are withheld. Which 19 are on by default, and how to reorder them, is covered in [Personalize the screener](personalize.md).

### The Alert button

A bell icon beside the Columns button, with a live badge showing how many alerts you have (it stops counting at `99+`). It opens the **Alerts** tab of the same panel.

On a first visit the bell is ringed with a gold glow and shows a small dismissible tooltip, **Set up your alerts here**. Dismissing it is permanent for that browser.

---

## The table

### Column headers

Each header has two separate controls, and they do different things:

| You click | What happens |
|---|---|
| The header **label** | Nothing sorts — the label is the drag handle. Hold and drag sideways to move the column. |
| The small **caret** to the right of the label | Sorts by that column. |

The sort cycle is ascending on the first caret click, descending on the second, then it alternates. Clicking cannot clear a sort; only choosing a chip clears it. There is no multi-column sort — each sort replaces the previous one.

On first load nothing is sorted: rows arrive in feed order. The header of the column you sorted by turns gold.

{% hint style="info" %}
The in-app tour step says "Click column headers to sort, drag to reorder". That wording is out of date — clicking the label starts a drag. Use the caret to sort.
{% endhint %}

Hovering any header shows a tooltip describing that column. All 57 columns have one, and they are translated into Russian.

### The three row sections

The table body is always three blocks, in this order, and sorting only reorders rows *inside* a block:

1. **Favourites** — every coin you have starred, pinned to the top under an accent-coloured divider, with a highlighted row style.
2. **Active rows** — everything else that currently has data.
3. **No-data rows** — shown below a hairline separator at 40% opacity. A row lands here when its price is not above zero, or when it has no positive volume in any of the five volume columns *and* no open interest. This block is only rendered under the **All** chip; any other chip drops those rows entirely.

There is no pagination and no row-count cap. The desktop table only draws the rows near your viewport as you scroll, which is why scrolling stays smooth on a full universe, and the header row and the Symbol column stay pinned in place.

### Favourites

On desktop, the star is a checkbox inside the **SYMBOL** cell. On a phone it is a large star button in the top-right corner of each card.

Favourites are stored in your browser only — there is no server-side watchlist and no sync between devices. A favourited coin still has to pass the active chip and the search box to be visible.

When at least one favourite is on screen the footer appends `· N starred`.

### Clicking a row

On desktop there is no whole-row click. Clicking the **ticker text** opens a TradingView chart in a modal over the table — the Binance perpetual for that symbol, 15-minute interval, dark theme — with a **Full Page →** link that opens the dedicated symbol page in a new tab. Escape, the ×, or a click on the backdrop closes it. See [The coin view](coin-view.md).

---

## The footer

Two things live down there:

- **The row count** for the list as it is currently filtered, plus `· N starred` when favourites are showing.
- **The connection indicator** — a coloured dot and a word telling you whether the data is live, degraded or frozen.

That indicator is worth understanding properly, because a frozen price under a calm-looking label is how people lose money. The full behaviour, including the warning strip that appears above the table when data stops advancing, is in [Reading the table](reading-the-table.md#the-connection-indicator).

---

## On a phone

Below 768 px wide the HTML table is not rendered at all. You get a card list instead.

Each card shows the ticker, the price, and four labelled metrics: **15M %**, **1H %**, **VOL 1H** and the funding rate. If the chip you have selected orders by some other metric, that metric is added to the card as one extra value. Nothing else from your column layout appears on a card.

The card values are drawn by the same code as the desktop table, so the formatting and the colours are identical.

Tapping a card opens the full symbol page. Tapping the star button only stars the coin — it does not navigate.

The **Columns** and **Alert** buttons open the same two-tab panel as on desktop, this time as a drawer sliding up from the bottom. The Alerts tab is fully usable there. Column choices are saved too, but they change the desktop table, not the fixed card layout.

Search, all 11 chips, the counter, favourites and the footer status all work on mobile. Dragging columns into a new order needs the desktop table, and the density control also affects the desktop table only.

---

## The 4-step onboarding tour

On a browser that has never seen it, a guided tour starts by itself 2.5 seconds after the page loads. It dims the screen and spotlights four things in order:

1. **Your Screener** — the table headers.
2. **Quick Filters** — the chip row.
3. **Telegram Alerts** — the bell button.
4. **Customize Columns** — the Columns button.

Controls: **Skip** on the first step, **Back** / **Next** afterwards, **Got it!** on the last one, an × to close, and progress dots. Escape dismisses, the right arrow or Enter advances, the left arrow goes back, and clicking the dimmed backdrop dismisses too.

To see it again, load the screener with `?tour=1` on the end of the URL — for example `app.erkescan.com/screener?tour=1`. There is no in-app button for this.

---

## Where your settings live

Your favourites, visible columns, column order and row density are saved in the browser you are using, not in your account. A different browser, a different device or a cleared site storage starts from the defaults.

Two things reset on every page load no matter what you saved: **SYMBOL** and **TREND** come back if you hid them, and **TREND** and **PRICE** are re-pinned immediately after **SYMBOL** if you dragged them elsewhere.

---

**Next:** [Reading the table](reading-the-table.md) — what the colours, the dashes and the connection states are telling you.
