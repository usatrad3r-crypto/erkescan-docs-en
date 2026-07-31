# Technical questions

Prices that do not match, dashes, stale banners, phones, and alerts that never fired.

### Why is the price different from my exchange

Two reasons. First, ErkeScan shows the **last traded price** on the Binance USDT-margined
perpetual, not the mark price your exchange uses for funding and liquidations. Second, if you
trade elsewhere, you are looking at a different order book.

Use ErkeScan to find and rank candidates; take your entry price from the venue you actually
trade on.

### What does a dash in a cell mean

**No data** — never zero. If a feed goes quiet, the affected values are cleared rather than left
showing a stale number, and the cell renders an em dash.

Rows full of dashes sink to the bottom on both ascending and descending sorts, so an empty value
can never sit at the top of your ranking pretending to be 0.00.

Common legitimate causes: a newly listed contract, a very illiquid symbol, or the first minutes
after a service restart for the open-interest columns.

### The table stopped updating what now

Look at the connection state above the table. The screener tracks both how long since it accepted
a fresh snapshot and whether prices anywhere are still moving; when either goes quiet it raises a
**stale** banner, and after a longer silence an **error** banner.

{% hint style="danger" %}
Never trade off a screen showing a stale or error banner. The layout still looks calm, but the
prices in it may be frozen.
{% endhint %}

Reload the page first. If the banner comes straight back, it is the data side, not your browser —
give it a few minutes, then tell [support](../reference/support.md) the time and what the banner
said. More cases in [troubleshooting](../screener/troubleshooting.md).

### Why did every Bar Vol column turn deeply negative at once

Because that is what those columns measure. **Bar Vol Δ$ / Δ%** on 5m, 15m and 1h compare the
**current unfinished bar** against the previous completed one, so at the start of every bar
almost the whole universe reads close to −100% and then climbs back toward zero as the bar fills.

It is bar progress, not a market event, which is why those cells are rendered in neutral colour.
The 8h and 1d legs are different — they compare two closed bars and do carry a real change in
turnover.

### Why does Volume 5m not move for minutes at a time

Because it is the **last closed** 5-minute candle. It is final by definition and steps to a new
value only when the next 5-minute candle closes. Volume 15m and Volume 1h, every VDelta column
and RVOL 5m behave the same way — they are built from closed 5-minute candles and step on the
same boundaries.

RVOL 1h steps every five minutes too, despite its name: it divides a trailing sum of the last 12
closed 5-minute candles by a baseline taken from the 1-hour candles.

If you want something that moves continuously, use Price, Change 1h, Change 24h or the Ticks
columns.

### Why is my Trend line so short after a page reload

The 4-hour trend is drawn from prices sampled while your tab is open. On load it is seeded with
roughly the last 100 minutes of history and then extends in real time, reaching the full four
hours after about four hours with the tab open. A refresh restarts from the seed.

With fewer than two points it shows a dim `--` instead of a line.

### My columns went back to the default layout

Column visibility, column order, density and favourites live in the browser you set them in. A
different browser or machine, a private window, or clearing site data all start from the default
19-column layout.

Note also that **Symbol** and **Trend** can be switched off for the session, but come back on
the next page load by design.

### Does switching to Russian change the URL

No. The **EN | RU** switch updates the interface in place and remembers your choice, but the URL
stays the same — there is no `/ru/screener` address to bookmark or send to someone.

If you clicked RU and the sign-in dialog is still English, reload the page once.

### Does the screener work on a phone

Yes. Below 768 pixels the table becomes a card list showing five metrics per coin — Price,
Change 1h, Change 15m, Volume 1h and Funding — plus the metric of whichever chip is active. The
star in the corner of a card toggles a favourite.

The column picker and the alerts panel open in a bottom drawer from the same header buttons as on
desktop.

### Why did my alert never fire

Work down this list:

1. **Telegram is not actually linked.** This is the most common cause. Custom alerts need your
   Telegram chat bound to your account — see
   [connect integrations](../getting-started/connect-integrations.md).
2. **You blocked or deleted the bot chat.** When Telegram rejects a delivery, the stored chat is
   cleared and everything stops silently until you link again.
3. **Your subscription lapsed.** Expiry deactivates all alerts. They come back when you renew.
4. **The threshold was never reached.** Sort the screener by the same metric and look at the real
   range before choosing a number.
5. **One of the conditions has no value on that contract.** If any single metric in the alert is
   blank for a contract, that contract is skipped entirely for that pass — silently. A
   five-condition alert can look dead simply because one metric is unavailable on thin symbols.
   Fewer conditions fire more often.
6. **You used Change (8h).** An alert on that field reads a different value from the column of the
   same name, and in practice almost never fires. Use another window.

More in [managing alerts](../alerts/managing-alerts.md).

### Why does an alert value not exactly match what I saw on screen

Because the two read the feed on different clocks. The values are recomputed at most every two
seconds; the alert engine polls on its own five-second cycle. A number that flickers across your
threshold between two polls can be missed, and a fired alert can quote a value a few seconds
older or newer than the one on your screen.

Set thresholds with a little margin rather than exactly on a level you saw once.

### Do I need to keep the tab open

Not for alerts. They are evaluated on the server and delivered to Telegram whether or not the
site is open.

Keep the tab open only for things drawn in the browser: the live table itself and the 4-hour
Trend line.

### Is there an API I can pull data from

The data feed is tied to a signed-in browser session with an active subscription, so there is no
customer-facing endpoint to point a script at. If you need something the app cannot do, describe
it to [support](../reference/support.md).

### Which browsers and devices work

Any current desktop or mobile browser. Your subscription and your alerts follow your account, so
you can sign in anywhere; your column layout, density and favourites do not travel — they are
per browser.

### I found a bug or want to request a feature

Send it to [@ErkeScanSupportbot](https://t.me/ErkeScanSupportbot) with the page URL, the time
including your timezone, and a screenshot. See [support](../reference/support.md) for the full
checklist.

**Next:** [Support](../reference/support.md)
