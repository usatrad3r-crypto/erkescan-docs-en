# 3. Connect Telegram and Discord

Connect Telegram to receive custom alerts and the strategy messages you enable. Discord is optional: it is relevant when your access comes through an existing community membership.

## Know which bot you need

| Bot | Purpose |
| --- | --- |
| [@erkescanalert_bot](https://t.me/erkescanalert_bot) | Custom alerts and enabled signal/Radar notifications |
| [@erkescan_premium_bot](https://t.me/erkescan_premium_bot) | Subscription purchase, status and eligible community verification |
| [@ErkeScanSupportbot](https://t.me/ErkeScanSupportbot) | Automated help and escalation to an operator |

Use links from the application or this guide. Do not send credentials or money to a look-alike account.

## Connect Telegram from the app

1. Sign in with the account that has your active subscription.
2. Open **avatar menu → Integrations**, or [open Integrations](https://app.erkescan.com/integrations).
3. In the Telegram card, select **Connect Telegram**. The app creates a personal link and opens the delivery bot.
4. In Telegram, press **Start** using that link. Opening the bot independently and typing `/start` is not the same as using your personal link.
5. Return to the app. Look for **Connected**; use **Refresh connection status** if needed. If the browser blocked the new tab, use the visible **Open Telegram** link in the card.
6. Use **Test Telegram Bot** if you want a test message. Receiving it confirms that the bot can send to your linked chat at that moment.

The link is single-use and normally expires after about 10 minutes. If it expires before you connect, create a fresh one. If the app already says Connected, do not reuse the old link.

This connection path also enables Alpha Pulse delivery. You can switch Alpha Pulse off on its strategy page while keeping custom alerts connected. Other strategies have their own Telegram controls.

**No additional purchase is needed to link an already subscribed account.** A Telegram payment or an eligible Discord confirmation in the subscription bot can also establish the chat link, but neither is necessary just to use the app's Connect button.

## If it does not work

* **Could not check the connection:** retry the status check. An unsuccessful check does not prove the chat is unlinked.
* **Test message failed:** ensure the delivery bot is not blocked, wait briefly and retry. A network or Telegram error can also fail the test.
* **Already linked to another account:** stop and contact [support](../reference/support.md). Do not buy a second term or make more accounts to work around the conflict.
* **Upgrade required:** check the email and subscription shown on [Subscription](https://app.erkescan.com/payments/billing).
* **Coming soon / temporarily unavailable:** check that product's status or contact support. A second payment does not enable an unavailable channel.

## Stop messages or change Telegram accounts

To stop one custom alert, pause it in **Alerts**. To stop one strategy, switch off its Telegram delivery on that strategy's page.

To remove the Telegram connection, open **Integrations → Unlink Telegram** and confirm. This disconnects custom-alert delivery and disables Telegram preferences for signal strategies. It does not cancel your subscription. After connecting a different chat, check and re-enable the strategies you want.

Telegram delivery controls do not pause or stop the separate Copy trading bot. Manage that in [Copy trading](../copy-trading/manage-and-troubleshoot.md).

## Connect Discord, if you already use community access

1. Open **Integrations → Discord → Connect**.
2. Authorize using the Discord account that holds your membership.
3. Return to Integrations and check the result.

**Linked** means the identity is connected but active eligible membership has not been confirmed. **Connected** means membership is also recognized. **Disconnected** means no identity is linked. Linking alone does not join a server or grant a role.

For the subscription-bot route, choose **Connect your Discord**, enter your ErkeScan account email, complete Discord authorization, then return to Telegram and press **Confirm**. Complete the confirmation before it expires.

Do not disconnect Discord as a troubleshooting experiment if your access depends on it. See [Discord](../integrations/discord.md) for membership and access details.

**Next:** [Your first 15 minutes](first-steps.md).
