# General questions

What ErkeScan is, what it deliberately is not, and whether it fits the way you trade.

### What is ErkeScan

A real-time screener for Binance USDT-margined perpetual futures, with custom Telegram alerts,
a small set of market-wide charts, and premium signal channels. You watch roughly 670 contracts
in one table, filter them down, and get told in Telegram when something you care about happens.

Full picture: [What is ErkeScan](../what-is-erkescan.md).

### Which market does ErkeScan cover

**Binance USDⓈ-M perpetual futures quoted in USDT**, and nothing else. Not spot, not
USDC-margined contracts, not dated quarterlies, not other exchanges.

Around 140 of the rows are not coins at all: Binance lists tokenized equities and commodities as
perpetuals too, and they sit in the same table with a **STOCK** or **COMMODITY** badge. See
[data and coverage](../reference/data-and-coverage.md).

### Does ErkeScan place trades for me

No. The screener, the alerts and the signal channels never touch your exchange account. ErkeScan
reads public market data and sends you messages; you place every order yourself, wherever you
trade.

### Do I need trading experience to use it

Some. The screener is a sortable table and the alerts are "if X crosses Y, message me" rules, so
the mechanics are simple. What takes experience is deciding which number matters and what to do
about it.

If you are new, work through [first steps](../getting-started/first-steps.md), then keep the
[glossary](../glossary.md) open while you read the
[column reference](../screener/column-reference.md).

### Is any of this financial advice

No. ErkeScan is a data tool. Nothing in the product, in this manual, or from support is a
recommendation to buy or sell anything, and no one can tell you how much to risk.

Where a strategy page shows a track record, that is a record of past trades. It is not a
forecast and not a guarantee.

### Which languages does the app support

English and Russian. The **EN | RU** switch sits in the top-right of the header on every page.
All 57 column headers, all 57 column tooltips, the filter chips and the onboarding tour are
translated.

Three things to know. Switching language does not change the URL, so there is no
Russian-language link you can bookmark or send to someone. The language of premium signal
messages in Telegram comes from your Telegram app's own language, not from this switch. And a
handful of labels in the column-picker sidebar — the Bar Vol Δ entries for 8h and 1d — stay in
English in RU mode; the table headers above them are correct.

### Can I see anything before I subscribe

Yes, some of it. Plans and prices are public at
[app.erkescan.com/pricing](https://app.erkescan.com/pricing). The Signals hub and the individual
strategy pages are public too — you can read their track records, though live signal details are
hidden until you subscribe.

The screener itself, the alerts page and the Charts page are not previewable. Without an active
subscription you get an upgrade panel instead of the table.

### Is there a mobile app to install

No installation is needed. Open [app.erkescan.com](https://app.erkescan.com) in your phone's
browser. The screener switches to a card layout with five metrics per coin, and the column and
alert panels open in a bottom drawer.

Alerts arrive in Telegram, so your phone gets those whether or not the site is open.

### How do I reach a human

Through [@ErkeScanSupportbot](https://t.me/ErkeScanSupportbot) on Telegram, or by email at
support@erkescan.com. See [support](../reference/support.md) for what to include and how long a
reply takes.

**Next:** [Subscription and billing](subscription.md)
