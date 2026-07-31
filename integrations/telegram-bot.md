# Telegram bots

Everything ErkeScan sends you arrives in Telegram. This page is the full reference for it: which bot does what, how your chat genuinely becomes linked, exactly what lands in your chat, and what to check when nothing does.

If you are setting this up for the first time, follow [Connect integrations](../getting-started/connect-integrations.md) first — the step-by-step lives there. This page is the detail behind it.

## Three bots, three jobs

ErkeScan runs three customer-facing bots. Mixing them up is the most common reason a customer thinks something is broken.

| Bot | What it is for |
|---|---|
| **@erkescanalert_bot** | Delivery only. Your [custom alerts](../alerts/how-alerts-work.md) **and** your [premium signals](../premium/overview.md) arrive here |
| **@erkescan_premium_bot** | Payments, subscription status, and Discord verification |
| **@ErkeScanSupportbot** | Human support |

**@erkescanalert_bot is one-way.** It sends; it does not hold a conversation. Typing into it achieves nothing, and nobody reads what you send there. Questions go to **@ErkeScanSupportbot**.

**@erkescan_premium_bot asks your language once.** Send `/start` with no link and it replies with two buttons — **English 🇺🇸** and **Русский 🇷🇺**. That choice applies to the bot's own menus only.

{% hint style="danger" %}
Those three handles, spelled exactly as above, are the only ErkeScan bots. Look-alike handles with an extra word, a digit or a different suffix are not ours. No ErkeScan bot will ever ask for your password, your seed phrase, your exchange API keys or a full card number.
{% endhint %}

## One chat, two kinds of message

Custom alerts and premium signals land in the **same** chat with **@erkescanalert_bot**, but they are two independent systems with two independent switches. This surprises people constantly.

| | Custom alerts | Premium signals |
|---|---|---|
| What produces them | The alert rules you built yourself | A strategy you subscribed to |
| Where you switch them off | Pause or delete the alert on the [Alerts page](../alerts/managing-alerts.md) | The toggle on that strategy's signal card |
| Effect on the other | None — signals keep arriving | None — your alerts keep arriving |

Both need the same thing first: a linked chat.

## How your Telegram actually becomes linked

Exactly three things attach your Telegram chat to your ErkeScan account:

1. Completing a payment inside **@erkescan_premium_bot**.
2. Redeeming the one-time Telegram link from a signal page, then pressing **Start**.
3. Confirming a Discord verification inside **@erkescan_premium_bot** (see [Discord](discord.md)).

[Connect integrations](../getting-started/connect-integrations.md) walks through each one.

{% hint style="warning" %}
Opening **@erkescanalert_bot** yourself and sending `/start` links nothing — the bot answers with a general message and your account is untouched. The same applies to the plain bot link on the Integrations page. The bot only accepts the one-time link a signal page mints for you.
{% endhint %}

### What the link writes

When a link succeeds, three things happen at once:

- Your chat is stored against your account, so **custom alerts can be delivered from that moment on**. Alerts you saved earlier start firing on their own — you do not need to re-save them.
- Your message language is captured from your **Telegram app's own language** at that instant. See [Language](#what-language-your-messages-arrive-in) below.
- If you linked through a signal page, that strategy's delivery is switched **on** and the bot confirms it in a message of its own.

### The rules the one-time link follows

- Valid for **10 minutes**, usable **once**. Expired or reused, the bot says so — go back to the signal page and press the button again.
- Your subscription is checked **twice**: when the link is created, and again when you press **Start**.
- **One Telegram chat belongs to one ErkeScan account.** If the chat is already attached elsewhere, the bot refuses and points you at [support](../reference/support.md).
- You can mint at most **5 links per 10 minutes**, and flip a strategy's toggle at most **10 times per 10 minutes**. Past that you get a "too many requests" answer; wait it out.

### Proving the link exists

Avatar menu → **Integrations** → in the Telegram card press **Test Telegram Bot**. A working link produces, in Telegram:

> ✅ ErkeScan connection test successful!
> Your alerts are working correctly.

Anything else — including *"Connection check failed. Please ensure you've connected your Telegram account and haven't blocked the bot."* — means the chat is not linked. Three presses per minute are allowed.

{% hint style="info" %}
There is no "disconnect Telegram" control in the app. To stop messages, pause or delete your alerts and switch off the premium toggles. Only Discord has a real disconnect button.
{% endhint %}

## What a custom alert message contains

One message per matched contract. The shape is fixed; the values below are only an example:

> 🔔 **Your alert name**
> Token: $BTC
> Change (1H): 4.12
> Volume (1H): 812345678
> Date & Time: …
> Alerts in Last 24H: 3
> Last Alert for BTC: …
> View Full Chart: Coinglass

Reading it correctly:

- **One line per condition**, using the metric's fixed display name and its raw value — whole numbers stay whole, otherwise up to four decimals. Units are the metric's own: percent, US dollars, or a count.
- **Date & Time** carries a timezone label in brackets. That is a fixed platform timezone, not yours.
- **Last Alert for {ticker}** is the *same* moment as Date & Time in a shorter format. It is not the previous alert's time — do not read it that way.
- **Alerts in Last 24H** counts messages you received for that ticker across **all** of your alerts in the trailing 24 hours, this one included.
- Underneath sit two buttons. The first opens that coin in ErkeScan. The second is labelled as an alert-settings button but only opens your alerts list — no edit form opens. Both button labels are in Russian regardless of your language.

A dark 15-minute chart image is attached when it can be fetched in time. It is best-effort: when the fetch fails the identical alert arrives as plain text with all values intact.

Very long alerts get truncated at Telegram's caption limit, and the tail — including the chart link — can be cut. Fewer conditions per alert avoids it.

The full breakdown of the engine behind these messages is in [How alerts work](../alerts/how-alerts-work.md).

## What a premium signal message contains

A signal message carries the direction and the symbol, then **Entry**, **SL**, **TP1** and **TP2**, the signal time in UTC, and a button back to that strategy's page.

Two fixed reminders are printed on every one of them: that exchange prices differ and the signal time is the reference point, and that the stop is always 2% from entry.

The first time a strategy is switched on you also get a **one-time activation notice**, separate from the signals themselves. If that notice fails to send it is retried a few times and then abandoned — you keep receiving trade signals either way, so a missing activation notice is not a delivery problem.

{% hint style="warning" %}
Both kinds of message are sent with forwarding and saving disabled by Telegram. You cannot pass them on, and neither can anyone you share your screen with. Treat a signal as yours alone.
{% endhint %}

## What language your messages arrive in

**Premium signals** follow your **Telegram app's language as it was when you linked the chat**: anything starting with `ru` gives Russian, everything else English.

**Custom alerts** arrive in English with the two buttons underneath labelled in Russian. There is no setting for this.

The **EN | RU** switch in the web app changes the website only. It has no effect on anything sent to Telegram.

## When messages do not arrive

Work down this list in order — the first two explain most cases.

1. **Press Test Telegram Bot.** If the test fails, nothing else matters: the chat is not linked. Go back to [Connect integrations](../getting-started/connect-integrations.md).
2. **Did you block, delete or restrict the bot?** Blocking **@erkescanalert_bot** makes the platform drop your stored chat. Custom alerts then stop **silently** — there is no warning, because there is nowhere left to send one. Unblock the bot and link again.
3. **Is the alert running?** A paused alert sends nothing. When a subscription lapses, *every* alert of yours is paused automatically, and renewing un-pauses all of them again — including ones you had paused on purpose.
4. **Is the strategy's toggle still on?** Switching it off stops that strategy from the next dispatch onwards and leaves your custom alerts untouched.
5. **Was the message simply too old to send?** A custom alert older than 10 minutes when the sender picks it up is dropped rather than delivered late, and a premium signal older than 6 hours is abandoned rather than retried. Both are deliberate: a stale entry is worse than no message.
6. **Did a burst get throttled?** A loose alert can match many contracts at once, and one message per contract can hit Telegram's own pace limits. Tighten the alert — see [Alert recipes](../alerts/alert-recipes.md).
7. **Message arrived without a chart?** Nothing is wrong. The image is best-effort; the values in the text are the alert.

If an alert has never fired at all, the cause is usually the alert rather than Telegram — [Manage your alerts](../alerts/managing-alerts.md) has that checklist.

Still stuck? Write to [support](../reference/support.md) with your account email, the alert name, and the time you expected the message.

**Next:** [Discord](discord.md) — what community access gives you, how the link works, and what "Linked" versus "Connected" really means.
