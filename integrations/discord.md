# Discord

Linking Discord connects your ErkeScan account to our closed trading community. This page covers what that link is worth, how to make it, why "linked" and "member" are not the same thing, every error you can hit, and how to undo it.

The short version of the connect flow is in [Connect integrations](../getting-started/connect-integrations.md). This page is the detail behind it.

## What linking Discord gives you

Two things, and they are separate.

**Community access.** The community lives on Discord. Being in it is what the **Trader** role represents.

**Access to ErkeScan itself.** If your Discord account holds the Trader role, that membership counts as an active ErkeScan subscription with **no end date** — the screener, alerts and everything else open up without a dated plan. The platform re-checks it automatically about once an hour.

That is why the link matters even if you never open Discord in a day: it is how community membership turns into product access.

## What linking Discord does not do

The link asks Discord for one thing only: **who you are**. It then reads whether that account holds the Trader role.

It does **not** add you to the server, and it does **not** grant you the role. If you are not already a member with the role, the link will succeed and give you nothing. Getting into the community itself is an access question — ask [support](../reference/support.md).

Discord is also not a delivery channel for your own alerts. [Custom alerts](../alerts/how-alerts-work.md) and premium signals go to Telegram only — see [Telegram bots](telegram-bot.md).

## Connecting, step by step

1. Sign in at **app.erkescan.com**.
2. Open the **avatar menu** (top right) → **Integrations**. Discord lives in its own card, next to the Telegram card.
3. Press the connect button in the Discord card. You are taken to Discord's own authorisation page.
4. Discord shows you what is being requested — your identity, nothing else. Approve it.
5. You are returned to the Integrations page, and the card shows the result immediately.

Use the Discord account that actually holds your membership. Approving with the wrong account links the wrong account — see [Disconnecting](#disconnecting) below.

Connect attempts are limited to **10 per 5 minutes**.

## Linked is not the same as member

After connecting, the Discord card shows one of three states. The middle one is the one people misread.

| Badge | What it means | What to do |
|---|---|---|
| **Disconnected** (red) | No Discord account is linked to you | Connect, as above |
| **Linked** (grey) | Your account is linked, but no active community membership was found | Nothing is wrong with the link. You are simply not in the community with the Trader role — or you linked the wrong account |
| **Connected** (green) | Linked **and** membership confirmed | Nothing. This is the finished state |

**Linked** carries the message *"Your Discord account is linked, but we have not found an active community membership yet."* **Connected** carries the community-access message instead.

The card also shows the Discord **username** the platform holds for you, with a copy button. It is a username, not an ID — send it as-is if support asks for it.

{% hint style="info" %}
The membership check runs about once an hour, in both directions. If you have just been given the role, the badge can lag behind by up to an hour — reconnect or wait a cycle. If your role is removed, access based on it also ends on one of those hourly passes rather than the same second.
{% endhint %}

## Errors you can actually see

A failed connect returns you to the Integrations page with a red banner at the top, in your language, which you can dismiss. Each of these has its own message:

| What happened | What to do |
|---|---|
| Too many attempts in a short time | Wait a few minutes and retry |
| Your ErkeScan session was not recognised | Sign in again, then retry |
| Discord itself was unreachable | Retry in a few minutes — see the note below |
| The request could not be verified | Start again from the Integrations page rather than re-using an old tab |
| The response came back incomplete | Retry the flow from the start |
| The authorisation was rejected | Retry and approve on Discord's page |
| Your account changed state mid-flow | Sign in again and retry |

Anything not on that list falls back to a generic failure message. All of them are safe to retry.

{% hint style="success" %}
When Discord is unreachable, **nothing is written at all** — your existing link and access are left exactly as they were. A Discord outage cannot take your access away by accident.
{% endhint %}

## Disconnecting

Discord is the one integration with a real disconnect control.

1. Press the disconnect button in the Discord card.
2. It asks for confirmation inline: *"Disconnect Discord? This removes your community access."*
3. Press **Yes, disconnect**.

That clears the Discord account stored against you and switches off the subscription that membership was granting. You get a toast confirming success or failure. Disconnects are limited to **5 per 5 minutes**.

{% hint style="warning" %}
Linking a **different** Discord account that does not hold the Trader role immediately deactivates the access your previous account was granting. If you are switching accounts, switch to the one that actually holds your membership.
{% endhint %}

## Verifying Discord inside the bot instead

**@erkescan_premium_bot** can run the same check, and this route has a bonus: it also links your Telegram chat, which the web flow does not.

1. In the bot's menu choose **Connect your Discord**.
2. Type your e-mail when the bot asks.
3. Press the authorisation button the bot sends, and complete Discord's authorisation in the browser.
4. Come back to Telegram and press **✅ Confirm**. The buttons expire after **10 minutes**.

Nothing is written to your account until you press **✅ Confirm** — that last step in Telegram is the proof that both accounts are yours. Let the buttons expire and simply start the flow again.

If you do not hold the Trader role, the bot tells you so and writes nothing. If Discord is down, it asks you to try again in a few minutes.

After a successful confirmation the bot offers up to three buttons: one to connect signals, one to join the trading community in Telegram — a personal invite, usable **once**, valid **24 hours** — and one that signs you into the ErkeScan dashboard.

## How Discord follows your billing

The platform keeps community access and billing in step on the same hourly pass.

- **When a subscription lapses**, the Trader role is removed, private Telegram group access is withdrawn, dashboard sessions are ended, and all of your custom alerts are paused. You get a message with a **Renew** button.
- **When you renew from a lapsed state**, the role is re-assigned and your alerts are un-paused automatically — *all* of them, including any you had paused deliberately, so read down your alerts list afterwards.

Renewing early, while your subscription is still active, changes nothing — there is nothing to restore.

Anything that looks wrong here — a role you should have, access that did not come back — is an account question. [Support](../reference/support.md) can see your account; a screenshot of the Discord card and your account email make the first reply useful.

**Next:** [What else your subscription includes](../premium/overview.md) — the premium signal strategies and the private community.
