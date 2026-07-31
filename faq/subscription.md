# Subscription and billing

Prices, payment, activation, renewal, and what happens when a term ends.

### What do the plans cost and how do they differ

| Plan | Price | Per month |
|---|---|---|
| Monthly | $200 for 1 month | $200 |
| Quarterly | $468 for 3 months — badged **Most popular**, **Save 22%** | ≈ $156 |
| Annual | $868 for 12 months — badged **Best value**, **Save 64%** | ≈ $72 |

They differ in **term length and price only**. The feature set is identical on all three; the
pricing page says it plainly: "All plans include full access to every feature."

Full breakdown: [choose a plan](../getting-started/choose-a-plan.md). Prices are public at
[app.erkescan.com/pricing](https://app.erkescan.com/pricing).

### Is there a free trial or a lifetime plan

Neither. No trial, no free tier, no lifetime option. The three plans above are the only things
you can buy.

### How can I pay

Three routes, all one-time payments:

1. **Crypto** — always offered on the checkout page. You are sent to our payment provider's
   hosted invoice.
2. **Card** — a hosted card checkout. It appears on the checkout page only while card payment
   is switched on; if you do not see it, crypto is the route.
3. **In Telegram** — **@erkescan_premium_bot**: `/start` → choose a language → **Subscribe** →
   pick 1 Month, 3 Months or 1 Year → type your email → the bot returns a pay link. This route is
   crypto only.

Paying through the Telegram bot has a side benefit: it links your Telegram chat to your account
at the same time, which is what custom-alert delivery needs.

### How soon does access start after payment

As soon as the payment is confirmed. After a card payment you land on a success page that waits
for the confirmation and then shows your access as active. A crypto payment moves through
**processing** to **activated**, and an on-chain confirmation can take a few minutes.

If a page sits on "processing" much longer than that, send the payment time and the plan to
[support](../reference/support.md).

### What happens if I renew before my term ends

The new time is added on top. When your current expiry is still in the future, the extension is
counted from that date rather than from today, so you lose nothing by renewing early.

Renewal is also the only way to extend: there is no auto-renew and no recurring charge, which is
why an active subscriber sees **Renew / extend** instead of a subscribe button.

### Where do I see my status and my purchase history

**Subscription** in the avatar menu, which opens `app.erkescan.com/payments/billing`.

It shows an active or inactive badge, your plan, the date your access runs to (or the date it
ended), the email on the account, your linked Discord username, and up to ten past purchases. If
a payment never completed, a banner offers a link to resume it.

### Will I be warned before my subscription ends

Yes — reminders go out **7 days, 3 days and 1 day** before expiry, with a renewal link. They are
sent in Telegram, so you only receive them if your Telegram chat is linked to your account.

### What happens when my subscription expires

Within the hour after expiry:

- the screener, alerts page and Charts page fall back to the upgrade panel;
- your custom alerts are deactivated — not deleted;
- premium signal delivery stops;
- you are removed from the private Telegram groups and Discord access is withdrawn;
- your web sessions are signed out;
- an expiry message with a renew button arrives in Telegram.

### What comes back when I renew after a lapse

Renewing from an expired state reverses those effects automatically: your alerts switch back on,
community access is restored, and your Discord role is re-assigned.

One caveat — this only runs on the transition from inactive to active. Alerts you paused
yourself stay paused, and an early renewal while still active changes nothing, because nothing
had been withdrawn.

### Can I get a refund

Refunds are handled by people, not by the bot. Write to support@erkescan.com or message
[@ErkeScanSupportbot](https://t.me/ErkeScanSupportbot) with your account email, the plan and the
approximate payment time. The support bot cannot issue refunds itself and will hand you to an
operator.

Note that the card checkout asks you to accept the terms, including — for EU and UK buyers — a
waiver of the 14-day right of withdrawal, because access starts immediately.

### What is the Discord plan on my billing page

Access granted through membership of the closed community rather than through a purchase on the
website. It carries no end date: entitlement is re-checked against your community role roughly
every hour instead. Because it is not a website purchase, its billing panel points you to manage
it in the community rather than offering a renew button.

### Do I need a subscription to receive premium signals

Yes. It is checked when you request the Telegram link, again when you press **Start**, and again
by the dispatcher before every send. See [premium overview](../premium/overview.md).

**Next:** [Features and tools](features.md)
