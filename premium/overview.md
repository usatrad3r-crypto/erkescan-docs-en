# What else your subscription includes

Your subscription is not only the screener and alerts. It also opens the premium signal
strategies and the private community. This page explains what you receive and how to switch
it on.

## The Signals hub

**Signals** in the top navigation opens the strategy catalogue at `/signals`. Each strategy
has its own card and its own page.

The catalogue carries **Alpha Pulse** and **Vertex**. A strategy gets a card only once it has
been published, so the list on the page is the list you can actually open.

Every card shows three numbers taken from that strategy's own record: **Profitable** (the
share of closed trades that ended in profit, in percent, with partial exits counted),
**Profit factor** (gross profit divided by gross loss) and **Trades** (how many closed trades
the record covers). The product deliberately says "Profitable" and not "win rate", because a
strict win rate would be a different, lower number.

{% hint style="warning" %}
A track record is a record of what already happened, over the period that record covers. It is
not a forecast, not a promise, and not advice. If a strategy's record cannot be refreshed, the
page keeps showing the last verified figures without flagging it, so treat the numbers as a
description of history rather than as live state. Position sizing and risk are your decisions.
{% endhint %}

## What a subscriber sees on a strategy page

Take **Alpha Pulse** as the example. Without an active subscription the live signal card is
locked: four blurred `●●●●●●` rows labelled **Entry**, **Stop**, **Target 1** and **Target 2**,
and no ticker. The blanking happens on the server: the ticker is never sent to your browser, so
there is nothing to dig out of the page source.

With an active subscription the same card shows the symbol, the direction, **Entry**,
**Stop**, **Target 1**, **Target 2**, the status, and how long ago the signal was raised. When
nothing is live you get a plain "no signal right now" card instead of the locked one.

The **Recent signals** table lists local time, symbol, direction, result and status. A symbol
less than **six hours** old is stripped out of the shared feed for everyone, as
anti-front-running protection, and is filled back in for paying viewers; if that lookup fails
you see `●●●●●●` rather than a wrong ticker.

The other strategy pages follow the same principle — the track record is public, the live
detail is not — but each lays its live section out in its own way.

## Getting the signals in Telegram

Delivery is through **@erkescanalert_bot** — the same bot and the same chat that your
[custom alerts](../alerts/how-alerts-work.md) arrive in.

1. Open the strategy page you want (for example **Signals → Alpha Pulse**).
2. Press the Telegram button on the signal card.
3. Telegram opens on **@erkescanalert_bot**. Press **Start**.
4. Come back to the browser tab. The button flips to **Alerts on** with a green **On** badge.

The link the button opens is single-use and valid for about **10 minutes**. If you take longer,
or open it twice, the bot replies that the link is expired or invalid — go back to the page and
press the button again for a fresh one.

{% hint style="info" %}
One Telegram chat can be bound to one ErkeScan account only. If the bot answers that this
Telegram account is already linked to another ErkeScan account, contact
[support](../reference/support.md).
{% endhint %}

An active subscription is required both when the link is created and again when you press
**Start**. If the button reads **Coming soon**, that channel is not open for your account yet;
support can tell you where it stands.

## What arrives, and what it looks like

Each signal message carries the direction and symbol, **Entry**, **SL**, **TP1**, **TP2**, the
signal time in UTC, and a button back to the strategy page. It also carries a fixed reminder
that prices differ between exchanges and that the signal time is the reference point.

Messages are sent with forwarding and saving disabled, so you cannot pass them on.

The language of these messages comes from your **Telegram app language** at the moment you
press **Start** — anything Russian becomes Russian, everything else English. The EN|RU switch
in the web app does not change it.

If a message has to be retried and the signal is by then more than **six hours old**, it is
dropped rather than delivered late.

## Turning it off and on

Once Telegram is linked, a toggle appears on the signal card. Switching it off stops that
strategy's delivery from the next dispatch onward. Switching it back on reuses the same link —
you do not need a new one.

Each strategy has its own toggle, and none of them affect your custom screener alerts. Those
run on a separate record and keep arriving.

## Community access

An active subscription also covers the private community.

- **Discord.** Connect your Discord account on **Integrations** (reachable from the avatar
  menu). Linking is read-only: it identifies your account and checks your community role. It
  does **not** join you to the server and does not grant you a role by itself. The card shows
  **Linked** when the account is connected but no active membership was found, and
  **Connected** once membership is confirmed.
- **Telegram community.** The invite is handed out by **@erkescan_premium_bot** — after a
  Discord confirmation there, or from the bot's profile screen. That invite is single-use and
  expires after 24 hours.

An hourly check keeps this in step with your billing: when a subscription lapses, community
access is withdrawn on the next pass; when you renew from a lapsed state, it is restored
automatically.

## Anything about access goes to support

Which strategies your account can reach, whether a channel is open yet, community membership,
a link that will not bind — all of that is an account question, and
[support](../reference/support.md) can see your account. Nothing about how the strategies pick
their trades is published anywhere, and support cannot share it either.

**Next:** [Data and coverage](../reference/data-and-coverage.md)
