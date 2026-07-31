# How alerts work

An ErkeScan alert is a set of numeric conditions that the platform checks against every Binance USDT-margined perpetual contract, around the clock, and reports to you in Telegram. This page explains what the engine actually does, so the alerts you build behave the way you expect.

## What an alert is

An alert is a name plus one or more conditions. Each condition is one metric, one operator and one number — for example **OI Change (15m)** `>` `5`, meaning open interest grew by more than 5% over roughly the last quarter of an hour.

Every threshold is typed as a bare number in the metric's own unit: percent for Change, OI Change, Volatility and Funding Rate; US dollars for Volume, VDelta, Open Interest and Price; a plain count for Ticks. [Create an alert](create-an-alert.md) lists the unit and the real time window of all 29 of them.

All conditions on one alert are combined with AND. Every condition must be true for the **same contract in the same check** before anything is sent.

You can put only one condition on each metric. There is no way to build a band such as "between 1% and 3%" on a single metric.

## An alert watches the whole market, not one coin

There is no symbol picker in the alert form. Every alert is evaluated against every contract in the market snapshot, and it fires separately for each contract that matches.

That universe is Binance USDT-margined [perpetual futures](../glossary.md) only — roughly 670 contracts, refreshed continuously. Around 140 of them are tokenized stock and commodity contracts, so an alert with a wide threshold can and will match those too. See [Data and coverage](../reference/data-and-coverage.md) for exactly what is and is not in scope.

The only way to narrow an alert is with the conditions themselves. A liquidity floor such as **Volume (1H)** `>` `500000` — 500,000 US dollars traded across the last 12 closed 5-minute candles — or a **Price** floor removes most of the market before the interesting condition is even considered.

{% hint style="info" %}
One evaluation pass can match many contracts at once. Each match becomes its own Telegram message, so a loose alert can produce a burst of messages in a few seconds.
{% endhint %}

## What the engine does

Your active alerts are re-queued for evaluation about every 30 seconds. They are checked against a shared market snapshot that is refreshed every 5 seconds.

For each contract, the engine reads the exact fields your alert uses and compares them to your numbers. If all conditions hold, the alert fires on that contract.

If any single metric your alert uses is unavailable for a contract, that contract is skipped entirely for that pass. A five-condition alert can look dead simply because one of its metrics is missing on thin contracts.

Alerts belonging to an account with no linked Telegram chat are not queued at all. Saving them works; they simply do nothing until Telegram is linked — see [Connect Telegram and Discord](../getting-started/connect-integrations.md).

## The re-trigger cooldown

After an alert fires on a contract, that same alert will not fire again on that same contract until the cooldown expires — **60 minutes** by default. There is no setting for it in the form.

The cooldown is per alert *and* per contract. The same alert can fire on a different contract one second later, and a different alert can fire on the same contract immediately.

This is why a **Change (1H)** `<` `-3` alert does not repeat every 30 seconds while a coin keeps bleeding. You get one message per coin per cooldown window, at most.

## The 200-alert limit

Every account can hold a maximum of **200 alerts**. The limit is identical on the Monthly, Quarterly and Annual plans — plans differ only in term length and price. See [Choose a plan](../getting-started/choose-a-plan.md).

Attempting to save the 201st alert fails with **Alert limit reached (max 200). Delete unused alerts to create new ones.** Editing an existing alert still works when you are at the cap.

In practice the limit is far above what a person can read. The number of messages, not the number of alerts, is what breaks a workflow.

## Where the message arrives

Custom alerts are delivered in Telegram by **@erkescanalert\_bot**, and nowhere else. There is no email, no Discord delivery, no browser push and no in-app inbox for custom alerts.

That is the same chat where premium signals arrive, but the two are wired to different records. Turning a premium signal feed off does not stop your custom alerts, and vice versa.

If you block the bot, or the chat becomes unreachable, the platform clears your linked chat and every one of your alerts stops being queued until you link Telegram again.

## What the message contains

You get one message per matched contract. The body follows a fixed shape:

```
<bell> <your alert name>
Token: <TICKER>
<Metric label>: <value>        one line per condition
Date & Time: <date and time> (<timezone>)
Alerts in Last 24H: <number>
Last Alert for <TICKER>: <time>
View Full Chart: Coinglass
```

The condition lines use fixed metric labels — **Change (5m)**, **Change (1H)**, **Change (24h)**, **Funding Rate**, **OI Change (15m)**, **Open Interest**, **Price**, **Volatility (5m)**, **Ticks (1H)**, **VDelta (5m)**, **Volume (1H)** and so on. Values print as whole numbers when they are whole, otherwise rounded to four decimals.

**Alerts in Last 24H** counts messages you received for that same ticker across *all* of your alerts in the trailing 24 hours, including this one. It is not a per-alert counter.

**Date & Time** carries a timezone label in brackets. It is a fixed platform timezone, not your local one, and the **Last Alert for** line repeats the same moment in a shorter format — treat the two lines as one timestamp.

Two inline buttons sit under every message. One opens that coin's page on `app.erkescan.com`; the other opens your alerts list. Both button labels are in Russian regardless of the language you use in the app.

{% hint style="info" %}
Alert messages are sent with content protection enabled, so Telegram will not let you forward or save them. Very wide alerts can also hit Telegram's caption limit; the tail of the message, including the chart link, is then cut and replaced with `… (truncated)`.
{% endhint %}

## The chart image

When it is available, the message arrives as an image with the text as its caption. The chart is a dark-theme Coinglass advanced chart for that contract, watermarked, with four studies drawn on it: aggregated open interest, aggregated liquidations, aggregated spot CVD and aggregated futures CVD.

The chart interval is fixed at **15 minutes**. It is not tied to the timeframe of your condition, and there is no setting to change it — a 5-minute condition and an 8-hour condition both arrive with the same 15-minute chart.

The image is best-effort. If it cannot be fetched in time, the same alert is still delivered as plain text with no error shown to you.

## When an alert is quietly skipped

Some situations stop a message without any visible feedback. Knowing them saves a lot of guessing:

- A contract is skipped when any one of your alert's metrics is unavailable for it.
- An **Open Interest** condition skips a contract whose open interest reads exactly zero.
- Conditions built on candle data are skipped for a contract whose 5-minute feed has gone quiet for more than 5 minutes.
- If the whole market snapshot is stale, no alert is evaluated at all until fresh data arrives.
- A fired alert that is more than 10 minutes old when the sender picks it up is dropped rather than delivered late. This is deliberate: a stale price move is worse than no message.

{% hint style="warning" %}
An alert tells you a number crossed a line. It does not tell you the move will continue, and ErkeScan never sizes or times a trade for you. Treat every alert as a prompt to go and look at the chart, and decide your risk before you act.
{% endhint %}

**Next:** [Create an alert](create-an-alert.md) — the form, the 29 conditions and how to pick a threshold that fires occasionally rather than constantly.
