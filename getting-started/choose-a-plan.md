# Choose a plan

ErkeScan has three plans. They unlock exactly the same product — the only difference is how long the term runs and what it costs. This page covers prices, payment methods, activation and where your subscription status lives.

The only working pricing page is **https://app.erkescan.com/pricing**. It is public, so you can read it before you sign in.

## The three plans

| Plan | Term | Price | Badge on the card | Works out at |
|---|---|---|---|---|
| **Monthly** | 1 month | **$200** | — | $200 / month |
| **Quarterly** | 3 months | **$468** | *Most popular* · *Save 22%* | ≈ $156 / month |
| **Annual** | 12 months | **$868** | *Best value* · *Save 64%* | ≈ $72 / month |

The savings are measured against paying monthly: 3 × $200 = $600 versus $468, and 12 × $200 = $2,400 versus $868. The Quarterly and Annual cards print that per-month figure themselves, as an approximation; the Monthly card carries no badge and no discount.

{% hint style="info" %}
All three plans include full access to every feature. There is no per-plan feature list, no alert quota that differs by plan, and no "pro" tier. Longer term, lower monthly cost — that is the whole difference.
{% endhint %}

## What the subscription unlocks

- The full [screener](../screener/tour.md) table — roughly 670 Binance USDT-margined [perpetual futures](../glossary.md) contracts, live. Around 140 of them are tokenized stocks and commodities rather than coins.
- [Custom alerts](../alerts/how-alerts-work.md) delivered to Telegram, up to 200 alerts per account.
- The [charts page](../screener/charts.md) with its cohort and funding panels.
- The single-symbol pages at `/symbols/<TICKER>`.
- Premium signal delivery in Telegram — see [Premium signals](../premium/overview.md).

## How to pay

Start on **https://app.erkescan.com/pricing** and press the button on the plan you want. What happens next depends on your state: if you are not signed in you are sent to sign-up first; if you are signed in without a subscription you go to that plan's checkout page; if your subscription is already active the button reads **Renew / extend**, and any term you buy is added to the time you already have.

On the checkout page:

- **Crypto** is always offered. The server builds the invoice from the plan's own price — the amount is never taken from your browser — and then hands you over to our payment provider's hosted page.
- **Card** appears on the same page when card checkout is switched on. If you do not see a card button, use crypto, or buy inside the Telegram bot.

Checkout also shows a consent line linking the [Terms](https://erkescan.com/terms) and the [Privacy Policy](https://erkescan.com/privacy-policy). Card checkout additionally asks you to tick acceptance of the terms, including a waiver of the EU/UK 14-day withdrawal right.

### Paying inside Telegram

You can also buy from **@erkescan_premium_bot**: send `/start`, pick your language, choose **Subscribe**, pick **1 Month**, **3 Months** or **1 Year**, type an e-mail, and the bot returns a pay-link button. The bot takes crypto only, at the same prices.

This route has a useful side effect: completing a payment inside the bot also links your Telegram chat, which is what makes custom alerts deliverable. See [Connect integrations](connect-integrations.md).

## Activation

Activation is automatic. Nothing needs to be sent to support, and no code needs to be entered anywhere.

- **Crypto.** After you pay, the success page shows one of three live states: *processing* while the payment is still unconfirmed, *received* once it has arrived, and *activated* when your subscription has been granted. Crypto activation waits on network confirmation, so give it time rather than paying twice. If the page cannot find your payment at all, take it to [support](../reference/support.md) — do not pay again.
- **Card.** You are returned to a success page that waits for the grant to land and then confirms it. Cancelling on the card page simply returns you to the pricing page — nothing is charged.

{% hint style="info" %}
Pressing pay twice for the same plan and e-mail within 30 minutes does not create a second invoice — the still-valid one is handed back to you. If you left a payment half-finished, the **Subscription** page shows a banner with a link to resume it, for up to two hours after the invoice was created.
{% endhint %}

## One-time payments, and how renewal stacks

Every plan is a **one-time payment for a fixed term**. There is no auto-renew and no recurring charge — your card or wallet is never billed again on its own.

Renewing early is safe: if your current end date is still in the future, the new term is added **to that date**, not to today. Renew a monthly plan five days before it lapses and you keep those five days.

## Where your subscription lives

Open the avatar menu at the top right and choose **Subscription** (`/payments/billing`). The page shows:

- an **Active** / **Inactive** badge;
- your plan and the date it stays active until — or the date it expired;
- your account e-mail and, if you linked one, your Discord username;
- a banner with a **resume payment** link when a recent invoice is still open;
- your purchase history, up to ten entries, read-only;
- the action button: **Subscribe** when inactive, **Renew / extend** when active.

## Reminders, expiry and coming back

If your Telegram chat is linked, the bot messages you **7 days**, **3 days** and **1 day** before your subscription ends, each message carrying a renewal link. Customers with no linked Telegram chat get no reminders at all — which is one more reason to complete [Connect integrations](connect-integrations.md).

When a term expires, all of the following happen automatically:

- all of your custom alerts are paused;
- your access to the private Telegram groups is removed;
- Discord access granted through ErkeScan is revoked;
- your active web sessions are ended, so you are signed out;
- you receive an expiry message in Telegram with a **Renew** button.

Renewing after a lapse reverses it: your alerts are un-paused and your community access is restored. Note that this only runs on a genuine inactive → active transition. Alerts **you** paused yourself stay paused — un-pause them from the [Alerts page](../alerts/managing-alerts.md).

## The community plan

Access can also come from an active membership in our closed community: if your linked Discord account holds the **Trader** role there, that counts as an active subscription with no end date. It is re-checked automatically about once an hour, so losing the role removes access within roughly that window.

That membership is not bought on this pricing page, and a community-based plan shows no renew button on the **Subscription** page — it tells you to manage the membership in the community instead.

If your access should be coming from the community and the **Subscription** page still shows *Inactive*, first check [Connect integrations](connect-integrations.md), then contact [support](../reference/support.md).

{% hint style="warning" %}
Buy only through **https://app.erkescan.com/pricing** or **@erkescan_premium_bot**. The old marketing address `erkescan.com/pricing` no longer exists, and anyone offering an ErkeScan subscription anywhere else is not us.
{% endhint %}

---

**Next:** [Connect integrations](connect-integrations.md) — get your Telegram chat linked so alerts and signals can actually reach you.
