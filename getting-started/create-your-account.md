# Create your account

This page takes you from nothing to a signed-in ErkeScan account, and tells you exactly what you can and cannot see before you subscribe.

## Sign up

1. Go to **https://app.erkescan.com/sign-up**.
2. Complete the sign-up form. It is hosted by our authentication provider, and it appears in Russian when your browser's top language starts with `ru`, otherwise in English.
3. When sign-up finishes you land on the **Screener** page.

That is the whole of account creation. There is no questionnaire and no payment at this stage. What you actually see on the Screener depends on whether you have an active subscription.

## Sign in later

Go to **https://app.erkescan.com/sign-in**, or press **Sign in** at the top right of the app.

If you followed a link to a page that requires an account, you are sent to the sign-in screen first and returned to that page afterwards. Signing in without such a link takes you to the Screener.

## What you see before you subscribe

A signed-in account without an active subscription is a real account — it simply has no market access yet.

| Page | Without an active subscription |
|---|---|
| **Screener** (`/screener`, and the site root) | A short summary panel with a **Get Started** button to the pricing page — no table |
| **Alerts** (`/alerts`) | The same panel with **Get Started** — no alert list, no form |
| **Charts** (`/charts`) | The same panel with **Get Started** — no charts |
| **Integrations** (`/integrations`) | Works. You can link Discord from here |
| **Subscription** (`/payments/billing`) | Works. Shows an *Inactive* badge and a **Subscribe** button |
| **Pricing** (`/pricing`) | Works — and is visible even to people who are not signed in |

A few pages are open to everyone, signed in or not: the pricing page, the strategy hub at `/signals`, and the individual strategy pages such as `/alpha-pulse` and `/vertex-signals`. On those pages the track record is public, but the details of any live signal — the symbol and the price levels — are removed on the server before the page reaches your browser. You will see blurred placeholder rows where those values would be; they are only placeholders. The real values are not in the page at all unless your subscription is active.

{% hint style="info" %}
There is no free trial and no lifetime plan. Access is a subscription for a fixed term — see [Choose a plan](choose-a-plan.md).
{% endhint %}

## Finding your way around

The header carries **Screener**, **Signals** and **Charts**. Some accounts also see one or two extra links; those are limited releases and are not part of what every subscription includes.

Three pages are reachable **only** from the avatar menu at the top right:

- **Subscription** → your plan, expiry date and purchase history
- **Alerts** → your custom alerts
- **Integrations** → Telegram and Discord

The header also has a **Contact us** button. It opens our support bot, **@ErkeScanSupportbot**, in Telegram. See [Support](../reference/support.md).

## English or Russian

Every page carries an **EN | RU** pill at the top right of the header. Click it, or focus it and use the left/right arrow keys, to switch language. Column headers, column tooltips, filter chips and the rest of the app switch with it.

A few labels stay in Latin script on purpose, because they are names rather than words: **VDELTA**, **RVOL**, **RetailHeat**, and the abbreviations OI and BTC inside otherwise-Russian headers.

Three things are worth knowing:

- Switching language does **not** change the URL. There is no Russian address for the screener, so you cannot bookmark or send someone a "Russian link" into the app. Your choice is stored in your browser and remembered for a year.
- On a first visit the language is picked for you: Russian when your browser's top language starts with `ru`, otherwise English.
- The sign-in, sign-up and account windows keep whichever language they were rendered with. If you switch language and one of them still looks wrong, reload the page.

## Your e-mail and closing the account

Your account e-mail comes from your sign-in identity and is kept in sync automatically. You can see the address the platform holds for you on the **Subscription** page.

If you delete your account, the billing record is kept for refund and chargeback purposes, but the account stops counting as subscribed immediately — no page will treat you as a paying customer afterwards. For account closure, refunds and privacy requests, the published contact address is **support@erkescan.com**.

---

**Next:** [Choose a plan](choose-a-plan.md) — the three plans, what they really cost, and how to pay.
