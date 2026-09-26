# Telegram bots

ErkeScan uses different bots for delivery, purchases and help. Start from the appropriate official link:

| Bot | Use it for |
| --- | --- |
| [@erkescanalert_bot](https://t.me/erkescanalert_bot) | Receiving custom alerts and enabled strategy/Radar notifications |
| [@erkescan_premium_bot](https://t.me/erkescan_premium_bot) | Buying or renewing a subscription, viewing its status and eligible Discord verification |
| [@ErkeScanSupportbot](https://t.me/ErkeScanSupportbot) | Questions, troubleshooting and operator escalation |

The delivery bot is not a support inbox. Use the support bot for a reply.

## Connect once, choose what to receive

Follow [Connect integrations](../getting-started/connect-integrations.md). The primary path is **Integrations → Connect Telegram → Start in Telegram → return to the app**. There is also a connection control in the screener's alert panel. Use the personal link created by the app, not an ordinary `/start` sent to a bot you opened yourself.

The standard connection enables Alpha Pulse delivery as well as linking custom alerts. Each strategy has its own switch; turn off a strategy you do not want. Enabling a notification channel does not activate copy trading.

| What you want to change | Where to do it |
| --- | --- |
| Stop one custom alert | Pause or delete it on Alerts |
| Stop one strategy/Radar channel | Its own Telegram delivery control |
| Change the Telegram account or disconnect all delivery | Integrations → Unlink Telegram, then confirm |
| Pause a trading bot | Copy trading; Telegram controls do not do this |

## What arrives

**Custom alerts** identify the alert and contract and list the matching conditions. Units depend on the selected metric. A chart image may be attached; a text-only message can still be a valid alert. Read the timestamp and confirm the current market before acting.

**Strategy signals** use the format of their strategy, which can include direction, entry, stop and targets. Do not assume every strategy uses the same stop distance or that a signal's price movement equals account profit. **Radar** is a market observation with a catalyst, not a ready-made entry/stop/target trade.

Signals arrive when their conditions occur, not on a fixed timetable. The absence of a new signal is different from a broken Telegram connection. A missed or stale notification is not promised to arrive later.

Some messages use Telegram's protected-content setting. This limits built-in forwarding and saving; it is not a guarantee that information cannot be copied. Do not share personal sign-in or Telegram-connection links.

## Language

The premium subscription bot has its own language selection. Strategy messages use the language captured by their Telegram connection; the website switch is not a universal Telegram-language setting. Custom-alert formatting can differ from strategy messages. The connection test uses the current app language when available.

If the message language is wrong, tell support which bot and message type you mean. Changing the website language alone may not change future strategy messages.

## Messages stopped: check in this order

1. Check your subscription and the email on it.
2. Check the connection status in Integrations. A failed check means the state could not be confirmed, not necessarily that it is disconnected.
3. Confirm that @erkescanalert_bot is unblocked. Use the test button if you want a delivery test.
4. Check the alert is active or that strategy's Telegram switch is on.
5. For custom alerts, check that all conditions can match the same contract and that the cooldown has ended. No qualifying match means no message.
6. If a bot says the personal link expired, return to the app: if it is already connected, do not redeem that link again; otherwise create a fresh one.

After a lapsed subscription is renewed, alerts paused by the system can resume; alerts you paused yourself remain paused. If the app and Telegram disagree, send [support](../reference/support.md) the message, page, alert/strategy name and time with timezone. Never send an API secret or a sign-in link.
