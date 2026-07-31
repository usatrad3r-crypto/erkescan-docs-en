# Make the screener yours

The screener ships with 19 columns visible out of 57 available. This page shows you how to choose which ones you see, in what order, how densely, which coins sit pinned at the top — and exactly what your browser remembers between visits.

## The Columns panel

Open it with the **Columns** / **Колонки** button in the toolbar above the table. On a desktop it slides out as a 280-pixel panel on the right; on a phone the same panel opens as a drawer from the bottom. It has two tabs: **Columns** and **Alerts**.

At the top are three one-click presets:

| Preset | What it does |
|---|---|
| **All** | Turns on every column. |
| **Defaults** | Restores the built-in 19-column layout. |
| **Core Only** | Cuts back to ten: Symbol, Trend, Price, Funding Rate, Open Interest, Change 5m, Change 1h, Volume 5m, OI Change 5m, OI Change 1h. |

Below the presets are the twelve category groups. Each has its own **Show All** / **Hide All** toggle and a row of chips, one per column:

**Core** · **Change %** · **Change $** · **Volume** · **RVOL** · **VDelta** · **Bar Vol Δ $** · **Bar Vol Δ %** · **OI Change** · **Volatility** · **Ticks** · **BTC Corr**

Click a chip to show or hide that column. Most chips read only the timeframe — `5m`, `15m`, `1h`, `8h`, `1d`, `24h` — because the group heading already tells you the family. The **Core** group is the exception — its chips carry full names — and so does **[RetailHeat](../glossary.md) (5m)**, which lives in the **Ticks** group.

At the bottom sits **Reset Column Order & Visibility** / **Сбросить порядок и видимость**, which throws away both your saved order and your saved visibility and puts the defaults back.

{% hint style="info" %}
The default 19 columns, in order, are: Symbol, Trend (4h), Price, RVOL 5m, Change 5m, Change 24h, Change$ 5m, Volume 5m, Bar Vol Δ% 5m, Ticks 5m, RetailHeat (5m), VDelta 5m, Volatility 15m, OI Change 5m, OI Change 1h, Funding Rate, BTC Corr 1h, Volume 1h, VDelta 1h.
{% endhint %}

### Two columns that come back

You can switch **Symbol** and **Trend** off — the chips are there and the table really does drop them — but the layout rebuild on every page load forces both back on. Treat hiding them as a temporary thing for the current session.

## Reordering columns: drag the label

Drag a column header sideways to move that column. Dragging works with a mouse, with touch, and from the keyboard, and it is restricted to the horizontal axis. The new order is saved the moment you drop it.

Two positions are fixed: **Trend** and **Price** are re-pinned immediately after **Symbol** on every load, whatever order you saved. Everything to the right of Price is yours to arrange.

## Sorting: the caret, not the label

This is the single most common misunderstanding on the screener.

- The **header label** is the drag handle. Your cursor turns into a grab hand over it. Clicking it does not sort.
- The small **caret button** beside the label is the sort control. Click it once for ascending, again for descending, and it alternates from there.

Sorting cannot be cleared by clicking — there is always an explicit direction once you start. There is no multi-column sort either: each click replaces the previous sort entirely, and holding Shift changes nothing. The header of the sorted column turns gold so you can see at a glance what the table is ordered by.

Picking a [quick filter](quick-filters.md) other than **All** clears your sort and applies that chip's own ordering — and that ordering keeps winning while the chip is active, so clicking a caret afterwards does not visibly reorder the rows. Go back to the **All** chip when you want to sort a column yourself.

On a fresh page load nothing is sorted at all; rows appear in feed order. **Trend** cannot be sorted.

Rows showing "—" always sink to the bottom, on ascending *and* descending sorts. A missing value never poses as 0.00.

{% hint style="warning" %}
The four-step welcome tour says "Click column headers to sort, drag to reorder." The first half is wrong — clicking the label starts a drag. Use the caret.
{% endhint %}

## Row density

A three-way segmented control in the toolbar sets how tall the rows are:

| Setting | Cell padding | Font | Header height |
|---|---|---|---|
| **Compact** / Компакт | 2 px | 10 px | 28 px |
| **Default** / Обычный | built-in | built-in | built-in |
| **Comfortable** / Свободный | 10 px | 14 px | 40 px |

Compact fits far more rows on one screen and is the right choice once you know your columns. Density styles the desktop table only — it does not change the mobile cards.

## Favourites

Favourites are your watchlist.

- **On desktop:** tick the checkbox inside the **Symbol** cell of any row.
- **On a phone:** tap the star in the top-right corner of the card. Tapping the star does not open the coin.

Favourited rows are lifted out of the list and pinned in their own block at the very top, above everything else, separated by an accent-coloured divider and given a highlighted row style. When at least one favourite is on screen, the footer appends **· N starred** / **· N избр.**

Two things to know:

1. A favourited coin still has to pass the active quick filter and the search box. Star a coin, then switch to **Squeeze**, and it disappears until it matches — that is the filter working, not the star failing.
2. Favourites live in your browser only. There is no server-side watchlist and no sync between devices.

## What your browser remembers

Everything you set on this page is stored locally in the browser you set it in. Nothing about your layout travels with your account.

**Saved between visits:**

- your favourites
- which columns are visible
- your column order
- your row density
- that you have seen the welcome tour
- that you have dismissed the alerts-button hint

**Not saved — resets on every load:**

- your column sort (the table starts unsorted, in feed order)
- the hidden state of **Symbol** and **Trend** (both come back)
- the position of **Trend** and **Price** (both re-pinned after Symbol)

Open the screener in a different browser, on a different device, or after clearing site data, and you start from the defaults again.

## On a phone

The **Columns** and **Alerts** panels both open on phones, in a bottom drawer, from the same toolbar buttons.

The card list itself, however, shows a fixed set of five metrics per coin — **Price**, **Change 15m**, **Change 1h**, **Volume 1h** and **Funding Rate** — plus the metric the active quick filter sorts by, if it is not already one of those five. That set does not follow your column choices. So the columns you switch on shape the desktop table; on the phone you get the fixed card.

The search box, all eleven quick filters, the counter, favourites and the footer status all work on mobile. Below 768 pixels wide the table is not rendered at all — you get cards instead.

## Replaying the welcome tour

The first time you open the screener in a browser, a four-step spotlight tour starts 2.5 seconds after the page loads: **Your Screener** (the table headers), **Quick Filters** (the chip strip), **Telegram Alerts** (the bell button), **Customize Columns** (the Columns button). Steps whose target is not on screen are dropped, so phones get a shorter tour.

Move through it with **Next** and **Back**, leave with **Skip**, **Got it!**, the **×**, or a click on the dimmed backdrop. Keyboard: Right-arrow or Enter advances, Left-arrow goes back, Escape dismisses.

It runs once per browser. To see it again, load the screener with `?tour=1` on the end of the URL:

```
https://app.erkescan.com/screener?tour=1
```

There is no in-app button for this.

## Language

The **EN | RU** pill at the top right of the header switches the whole app between English and Russian. It is on every page. Click it, or focus it and use Enter, Space, or the Left/Right arrow keys.

Switching language on the screener does not change the URL — your choice is stored in the browser and in a cookie that lasts a year. On your first ever visit the app picks Russian if your browser asks for Russian, and English otherwise.

In Russian mode all 57 column headers and all 57 header tooltips are translated. Three metric families keep their Latin names because they are treated as brand terms — **VDELTA**, **RVOL** and **RETAILHEAT** — and the acronyms *OI* and *BTC* stay Latin inside otherwise-Cyrillic headers such as «ИЗМ. OI (1ч)» and «КОРР. BTC (1ч)». Four chips in the Columns panel — *Vol Δ$ 8h*, *Vol Δ$ 1d*, *Vol Δ% 8h*, *Vol Δ% 1d* — stay in English, and their wording there does not match the table header, which reads **BAR VOL Δ$ (8h)** and so on.

{% hint style="info" %}
There is no Russian-language URL for the screener, so you cannot bookmark or share a "Russian link" to it. Sign-in and account dialogs are localised when the page is first rendered, so if you switch language and those dialogs are still in the old language, reload the page.
{% endhint %}

---

## Three starter layouts

These are starting points, not prescriptions. Build one, live with it for a week, and cut anything you never look at.

### 1. Scalper — minutes

You care about what is happening in the last one or two candles and whether there is enough turnover to get filled.

Press **Core Only**, then switch on:

- **Change %** → `15m`
- **Volume** → `15m`
- **RVOL** → `5m`
- **VDelta** → `5m`
- **Volatility** → `5m`
- **Ticks** → `5m` and **RetailHeat (5m)**

You end up with: Symbol, Trend, Price, Change 5m, Change 15m, Change 1h, Volume 5m, Volume 15m, RVOL 5m, VDelta 5m, Volatility 5m, Ticks 5m, RetailHeat (5m), OI Change 5m, OI Change 1h, Funding Rate, Open Interest.

Set density to **Compact**, sort by **RVOL 5m** descending with the caret, and work the top of the list. This layout pairs naturally with the **High Volume** and **Breakout** chips.

### 2. Intraday momentum — hours

You want the 1-hour picture with confirmation from flow and positioning.

Press **Defaults**, then switch on **Change %** → `1h`, **RVOL** → `1h`, and **Ticks** → `15m`. To keep the row readable, switch off **Bar Vol Δ%** → `5m` and **Change $** → `5m`.

You end up with: Symbol, Trend, Price, RVOL 5m, RVOL 1h, Change 5m, Change 1h, Change 24h, Volume 5m, Volume 1h, Ticks 5m, Ticks 15m, RetailHeat (5m), VDelta 5m, VDelta 1h, Volatility 15m, OI Change 5m, OI Change 1h, Funding Rate, BTC Corr 1h.

Sort by **Change (1h)** descending, or run the **Big Movers** and **Accumulation** chips against it. **BTC Corr 1h** is there to tell you whether a move is the coin's own or just the whole market breathing.

{% hint style="info" %}
Prefer **RVOL 5m** and **RVOL 1h** for judgement calls. **RVOL 15m** is built from the still-forming 15-minute candle, so it reads near zero just after each 15-minute boundary and climbs through the bar. [RVOL](../glossary.md) and every other column is defined in full in the [Column reference](column-reference.md).
{% endhint %}

### 3. Swing — days

You want the slower windows and the honest bar-over-bar readings.

Press **Core Only**, then switch on:

- **Change %** → `1h`, `8h`, `24h`
- **Volume** → `8h`, `24h`
- **RVOL** → `8h`, `1d`
- **VDelta** → `8h`, `1d`
- **Bar Vol Δ %** → `8h`, `1d`
- **OI Change** → `1d`
- **Volatility** → `1h`
- **BTC Corr** → `1d`

You end up with: Symbol, Trend, Price, Change 5m, Change 1h, Change 8h, Change 24h, Volume 5m, Volume 8h, Volume 24h, RVOL 8h, RVOL 1d, VDelta 8h, VDelta 1d, Bar Vol Δ% 8h, Bar Vol Δ% 1d, OI Change 5m, OI Change 1h, OI Change 1d, Volatility 1h, Funding Rate, Open Interest, BTC Corr 1d. (Switch off **Change %** → `5m` and **OI Change** → `5m` if you never look at them.)

Set density to **Comfortable**, sort by **Change (24h)** or **OI Change (1d)**, and use favourites to keep the handful of names you are actually tracking pinned at the top.

{% hint style="warning" %}
Only the **8h** and **1d** legs of **Bar Vol Δ$** and **Bar Vol Δ%** compare one finished bar with the previous finished bar. The 5m, 15m and 1h legs measure how far the *current unfinished* bar has filled, so they sit near −100% for the whole market at the start of every bar. Do not build a swing thesis on those.
{% endhint %}

A layout is a lens, not an edge. None of these arrangements makes a trade more likely to work — they only make the numbers you have decided to care about easier to see. Your entry, your stop and your position size are still yours to decide.

**Next:** [Build your own filters](build-your-own-filters.md) — a method for turning a question into a shortlist using columns, sort and search.
