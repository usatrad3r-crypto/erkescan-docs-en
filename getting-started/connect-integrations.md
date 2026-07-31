# Connect integrations

ErkeScan delivers your alerts and premium signals through Telegram, and can link your Discord account for community access. This page shows the routes that actually link your Telegram chat, and what Discord linking does and does not do.

## Three bots, three jobs

Customers confuse these constantly, so learn them once:

| Bot | What it is for |
|---|---|
| **@erkescanalert_bot** | Delivery. Your [custom alerts](../alerts/how-alerts-work.md) *and* premium signals arrive here |
| **@erkescan_premium_bot** | Payments, subscription status and Discord verification |
| **@ErkeScanSupportbot** | Human support |

{% hint style="danger" %}
Those three handles, spelled exactly as above, are the only ErkeScan bots. Look-alike handles with an extra word or a different suffix are not ours — never send them money or personal details.
{% endhint %}

## Part 1 — link your Telegram chat

Your Telegram chat has to be attached to your ErkeScan account before anything can be sent to you. Custom alerts you create before that are saved and simply stay undelivered until the link exists — they start firing on their own once it does.

Exactly three things link the chat, and nothing else does:

- completing a payment inside **@erkescan_premium_bot** — Route A below;
- redeeming the one-time Telegram link from a signal page — Route B below;
- confirming a Discord link inside **@erkescan_premium_bot** — the last section of Part 2.

Pick whichever fits your situation.

### Route A — buy or renew inside @erkescan_premium_bot

The most direct route, and the one to use if you have not paid yet.

1. Open **@erkescan_premium_bot** in Telegram and send `/start`.
2. Choose your language — **English 🇺🇸** or **Русский 🇷🇺**.
3. Choose **Subscribe** and pick **1 Month**, **3 Months** or **1 Year**.
4. Type an e-mail when the bot asks for one.
5. Press the pay-link button the bot returns and complete the payment.

When the payment completes, the chat you used is linked to your account. Nothing else to press.

The same bot has a **Connect your Discord** entry in its menu, and completing *that* flow also links your chat — see Part 2 below.

### Route B — the Telegram button on a signal page

Use this if your subscription is already active and you bought it on the website.

1. Open a signal page — for example **https://app.erkescan.com/alpha-pulse**.
2. Press the Telegram button on the signal card. The page mints a one-time link and opens **@erkescanalert_bot**.
3. Press **Start** in Telegram.
4. Leave the browser tab open. It checks for about a minute, showing **Open Telegram** with the sub-line *Press Start in Telegram*, then flips to **Alerts on** with a green **On** badge.

Telegram confirms with a message of its own — for Alpha Pulse it reads *"Alpha Pulse is active — Signals will arrive here — in the same Telegram chat as your custom alerts."*

This route does two things at once: it links your chat, and it switches that strategy's signals **on**. You can turn the signals back off later without unlinking the chat.

Rules that apply to this route:

- The link is valid for **10 minutes** and can be used **once**. If it expires, the bot tells you so — go back to the page and press the button again.
- Your subscription is checked twice: when the link is created and again when you press Start. An expired subscription is refused at the second check.
- **One Telegram chat can belong to only one ErkeScan account.** If that chat is already attached to a different account the bot refuses and tells you to contact support.
- The button can be created at most 5 times per 10 minutes.
- If the button reads *Coming soon*, that delivery route is not switched on for your account yet. Ask [support](../reference/support.md) rather than buying a second term to force it. If the button asks you to upgrade instead, your subscription is not active.

### Check that it worked

Open the avatar menu → **Integrations**. In the Telegram card press **Test Telegram Bot**. A successful link produces this message in Telegram:

> ✅ ErkeScan connection test successful!
> Your alerts are working correctly.

If instead you get *"Connection check failed. Please ensure you've connected your Telegram account and haven't blocked the bot."*, your chat is not linked — go back and complete Route A or Route B. The test button can be pressed 3 times per minute.

{% hint style="warning" %}
Opening **@erkescanalert_bot** by hand and sending `/start` does **not** link anything, and neither does the plain link to that bot on the Integrations page. The bot needs the one-time link minted by a signal page (Route B), or your chat has to arrive through **@erkescan_premium_bot** (Route A). If you pressed **Start** and the test above still fails, that is why. Treat **Test Telegram Bot** as the only proof that the link exists.
{% endhint %}

## What arrives where, and what switches it off

Custom alerts and premium signals land in the **same Telegram chat**, but they are driven by two separate records, with two separate switches:

| | Custom alerts | Premium signals |
|---|---|---|
| Comes from | Alert rules you create | A strategy you subscribed to |
| Turned off by | Pausing or deleting the alert on the [Alerts page](../alerts/managing-alerts.md) | The toggle on that strategy's signal card |
| Effect of turning one off | Signals keep coming | Your alerts keep coming |

Turning a premium strategy off stops its delivery from the next dispatch onwards. Turning it back on re-uses the existing link — you do not need a new one-time link.

There is no "disconnect Telegram" button in the app. To stop everything, pause or delete your alerts and switch off the premium toggles.

{% hint style="warning" %}
If you block **@erkescanalert_bot** in Telegram, the platform drops your chat link. Custom alert delivery stops silently — you get no warning message, because there is no longer anywhere to send one. Unblock the bot and link again through Route A or Route B.
{% endhint %}

## What language your Telegram messages arrive in

**Premium signal** messages follow your **Telegram client's own language** as it was at the moment you linked the chat: anything starting with `ru` gives you Russian, anything else English.

**Custom alert** messages arrive in English, and the two buttons underneath them are labelled in Russian. There is no setting for this.

The **EN | RU** switch in the webapp changes only the website. It does not change the language of anything sent to Telegram.

## Part 2 — connect Discord

### What it gives you

Linking Discord lets ErkeScan see whether your Discord account holds the **Trader** role in our closed community. If it does, that membership counts as an active subscription with no end date, re-checked automatically about once an hour.

### What it does not do

The link asks Discord only for your identity. It **does not** add you to the server, and it **does not** grant you any role. If you are not already a member with the Trader role, the link succeeds but gives you no access.

### How to link it

1. Avatar menu → **Integrations**.
2. In the Discord card press the connect button. You are sent to Discord's own authorisation page.
3. Approve, and you are returned to the Integrations page with the result.

The card then shows one of three states:

| Badge | Meaning |
|---|---|
| **Disconnected** (red) | No Discord account is linked |
| **Linked** (grey) | Your Discord account is linked, but no active community membership was found |
| **Connected** (green) | Linked *and* an active community membership — full community access |

The card also shows the Discord username the platform holds for you, with a copy button.

### When linking fails

Failures appear as a dismissible red banner at the top of the Integrations page, in your language. You will see a specific message for each of these cases:

- too many attempts in a short time;
- your ErkeScan session was not recognised;
- Discord itself was unreachable;
- the request could not be verified, or came back incomplete;
- the authorisation was rejected;
- your account changed state in the middle of the flow.

All of them are safe to retry. When Discord is unreachable, **nothing is written** — your existing state is untouched, so retry in a few minutes. Connect attempts are limited to 10 per 5 minutes.

### Disconnecting

Press the disconnect button in the Discord card. It asks for confirmation — *"Disconnect Discord? This removes your community access."* → **Yes, disconnect** — then clears your Discord link and deactivates the community-based subscription. Disconnects are limited to 5 per 5 minutes.

Re-linking a **different** Discord account that does not hold the Trader role deactivates the access the previous account was granting. Link the account that actually holds your membership.

### Verifying Discord inside the bot instead

@erkescan_premium_bot can do the same check, and this is the route that also links your Telegram chat:

1. In the bot menu choose **Connect your Discord**.
2. Type your e-mail.
3. Press the authorisation button the bot sends and complete Discord's authorisation.
4. Return to Telegram and press **✅ Confirm**. The buttons expire after 10 minutes.

Nothing is written to your account until you press Confirm — that final step in Telegram is what proves both accounts are yours.

If you do not hold the Trader role, the bot says so and writes nothing. If Discord is down it asks you to try again in a few minutes.

After a successful confirmation the bot offers up to three buttons: one to connect signals, one to join the trading community (a personal invite link, usable once, valid 24 hours), and one that signs you into the ErkeScan dashboard.

---

**Next:** [First steps](first-steps.md) — a guided first fifteen minutes in the screener, ending with your first alert.
