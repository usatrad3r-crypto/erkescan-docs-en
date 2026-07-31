# Manage your alerts

Everything you do to an alert after it exists: finding it, editing it, pausing it, deleting it, and diagnosing the two failures people actually hit — an alert that never fires, and an alert that fires but never reaches you.

## Where your alerts live

Open your account menu (your avatar, top right) and choose **Alerts**. The alerts page is not in the main navigation bar; the menu item and the direct URL are the only ways in.

Each alert is a card showing its position in your list, its name, the date you created it, and a pill reading **Active** or **Paused**.

The screener has a compact version of the same list. Press the gold **Alert** bell button in the screener header and the panel opens on the right — on a phone it slides up from the bottom. The bell also carries a live count badge, which stops counting past **99+**.

There is no in-app history of alerts that have fired. Your Telegram chat is the record.

{% hint style="info" %}
The second button under every Telegram alert message opens your alerts list, but it does not open that particular alert for editing. Find the alert by name on the page instead.
{% endhint %}

## Editing an alert

Press the pencil icon on the alert's card. The same form opens, pre-filled with the alert's name and conditions.

Change what you need and save. You will see **Alert updated successfully!** and the alert keeps its place in your list — it is the same alert, not a new one.

Editing does not change the paused state. A paused alert stays paused after an edit; un-pause it separately when you are ready.

{% hint style="warning" %}
Whatever you leave empty when you save becomes empty. If you clear a condition's value while editing, that condition is removed from the alert. Before saving, check every row you intended to keep still has both an operator and a number.
{% endhint %}

{% hint style="warning" %}
**Do not use the copy icon to duplicate an alert.** It behaves differently depending on where you press it: in the screener panel it opens an empty form, and on the alerts page it saves under the original alert's name rather than the "Copy" name shown on the draft card. Worse, while a copy draft is pending, editing a *different* alert and saving can create a new alert instead of updating the one you opened.

If you have already pressed it, reload the alerts page before you edit anything else. To get a second, similar alert, build it from scratch — it takes under a minute.
{% endhint %}

You can still edit alerts when you are at the 200-alert limit — the alert you are editing is not counted against the cap.

## Pausing and resuming

Each card has a play/pause toggle. Pausing stops the alert from being evaluated at all; the card's pill switches to **Paused** and you see **Alert paused**.

Un-pausing asks for an immediate re-check across the system, so a resumed alert is usually live within seconds. If that re-check has just run for someone else, yours is picked up by the next 30-second cycle instead.

Pausing is the right move for an alert you want back later — a setup that only matters in certain conditions, or one you are re-tuning.

## Deleting an alert

Press the trash icon. Your browser shows a plain confirmation box asking **Delete this alert?**

Confirm and the alert and all its conditions are removed in one go. You will see **Alert deleted**.

{% hint style="danger" %}
Deletion is permanent. There is no undo, no archive and no trash bin for alerts. If you might want it back, pause it instead.
{% endhint %}

## The 200-alert limit

Every account can hold 200 alerts, the same on every plan. Trying to save one more fails with:

> Alert limit reached (max 200). Delete unused alerts to create new ones.

To recover, delete alerts you no longer act on. Read down the list — the cards show name and creation date, and anything whose purpose you cannot immediately explain to yourself is a candidate.

Pausing does **not** free a slot. A paused alert still counts against the 200.

## Errors you may see when saving

Most of these appear both as a red notification and as red text under the form. The name-length and invalid-number messages are field-level checks and appear next to the input that caused them.

| Message | What it means |
| --- | --- |
| *Alert name must be at least 2 characters.* | The name is too short. |
| *Add at least one condition (operator + value) before saving.* | Every row is empty, or a row has an operator but no number. |
| *Invalid input. Please enter a valid number using digits (0-9) and a period (.) for decimals. Symbols like %, $, or commas (,) are not allowed.* | You typed `%`, `$`, a comma or a space into a value box. |
| *Alert limit reached (max 200). Delete unused alerts to create new ones.* | You are at the cap. |
| *An active subscription is required to save alerts.* | The account has no active subscription. |
| *Your subscription has expired. Renew it to save alerts.* | The subscription lapsed. Renew, then try again. |
| *Link your Discord account to use the Discord plan.* | Your access comes through the community plan and the Discord link is missing. |
| *Too many changes — please wait a moment and try again.* | You hit the rate limit — creating and editing is capped at 10 changes a minute. Wait a moment. |
| *Please sign in again to save alerts.* | Your session expired. Sign in and retry. |
| *This alert no longer exists.* | The alert was deleted, probably in another tab. |

Pause, resume and delete are also rate-limited — roughly 30 pause/resume actions and 20 deletions a minute. Unlike saving, those two actions only ever show a generic **Failed to update alert** or **Failed to delete alert** when something goes wrong; retry after a moment, and if it persists, contact [support](../reference/support.md).

## Why an alert never fires

Work down this list before assuming something is broken.

**Telegram is not linked.** This is by far the most common cause. Alerts belonging to an account with no linked Telegram chat are never even queued for evaluation. See the next section.

**The alert is paused.** Check the pill on the card.

**Your subscription lapsed.** When a subscription expires, every one of your alerts is paused automatically. Renewing un-pauses *all* of them again — including any you had deliberately paused yourself, so read down the list after a renewal and re-pause what you did not want back.

**The threshold is out of reach.** Sort the matching column in the screener descending and see whether anything ever gets near your number. This resolves most "never fires" reports.

**The conditions cannot be true at once.** Every condition must hold on the same contract in the same check. `Change (1H) > 5` together with `Volatility (5m) < 0.5` is asking for a violent move on a calm contract.

**You used Change (8H).** The value an alert reads for Change (8H) is frozen a few seconds into each 8-hour bar, so it sits near zero for practically every contract and the alert will effectively never fire. Rebuild it on Change (1H) or Change (24h).

**One of your metrics is missing on the contracts you care about.** If any single metric in your alert has no value for a contract, that contract is skipped completely for that pass. The more conditions you stack, and the more exotic the metrics, the more contracts drop out silently.

**An Open Interest condition and a zero reading.** A contract whose open interest reads exactly zero is skipped by Open Interest conditions.

**You are using a slow window.** Change (8H), Volume (8H) and VDelta (8H) update once per 8-hour bar, and VDelta (1D) once a day. They cannot react to something that happened ten minutes ago.

## Why a message never arrived

**Telegram was never linked.** Saving an alert without a linked Telegram succeeds, and there is no failure message — the alert simply sits idle. This catches out most new subscribers.

The **Connect Telegram** button on the alerts and integrations pages does not complete the link on its own. The paths that do link your chat are: completing a payment inside **@erkescan\_premium\_bot**, redeeming a premium-signal link from a signal page, or confirming a Discord link inside that same bot. The full working procedure is in [Connect Telegram and Discord](../getting-started/connect-integrations.md).

**Check the link before you debug anything else.** Press **Test Telegram Bot** on the Telegram card — it sits on the alerts page and on the integrations page, both of which live in your account menu. If the link is good you receive *ErkeScan connection test successful! Your alerts are working correctly.* in Telegram within seconds. The button allows three presses per minute.

If the test fails, you get *Connection check failed. Please ensure you've connected your Telegram account and haven't blocked the bot.* — which is exactly the checklist.

**You blocked or removed the bot.** Blocking **@erkescanalert\_bot**, deleting the chat, or otherwise making it unreachable clears your stored chat on the platform. Every alert then stops silently until you link again — there is no warning message, because there is nowhere left to send one.

**The message was too old to send.** If a delivery backlog builds up, anything more than 10 minutes old is dropped rather than sent late. This is deliberate — a stale price move is worse than no message.

**A burst got delayed.** A wide alert matching many contracts at once sends one message per contract, and Telegram throttles heavy bursts. Tightening the alert fixes this properly; see [Alert recipes](alert-recipes.md).

**The message arrived without a chart.** The chart image is best-effort. When it cannot be fetched in time the same alert is delivered as plain text, with the values intact — nothing is wrong with the alert itself.

**Everything looks fine but the numbers seem off.** Check the window of the metric you used against [the condition reference](create-an-alert.md#the-seven-condition-groups). Volume (5m) is one closed candle, Volatility (1H) looks back roughly 20 hours, and the OI Change windows are approximate. Most "wrong value" reports are window mismatches.

Still stuck? Bring your alert name, the exact conditions and the time you expected it to fire to [support](../reference/support.md).

**Next:** [Telegram bots](../integrations/telegram-bot.md) — which ErkeScan bot does what, and which one is the one you actually need to talk to.
