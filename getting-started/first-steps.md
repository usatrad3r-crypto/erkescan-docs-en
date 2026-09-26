# 4. Your first 15 minutes

This short exercise takes you from a market question to a chart and your first Telegram alert. You need an active subscription. It does not require an exchange connection or place an order.

On a computer, the screener shows a table with sortable columns. On a phone, it shows compact market cards; tap a card to open its chart. Both layouts let you find a symbol and use alerts.

## 1. Choose a task

For this exercise, ask: **“Which market should I look at more closely?”** Open the [Screener](https://app.erkescan.com/screener) and wait for market values to load. If a stale-data warning appears, follow [Troubleshooting](../screener/troubleshooting.md) before relying on the displayed prices.

If you came for ready-made strategy signals, automated execution or trade review, start with [Choose a tool](../signals/choose-a-tool.md), [Copy trading](../copy-trading/overview.md) or [Trading Journal](../journal/overview.md). Those have their own setup steps.

## 2. Find an actively traded market

Select **All**, then search for a familiar contract such as `BTC`. Read the complete symbol: a partial search can also find other contracts containing those letters.

Check **Volume (1h)**. On a computer, use the small arrow beside that column to sort by descending turnover; on a phone, read the value on the card. Look for a market with substantial recent activity, rather than choosing only the largest percentage move. Turnover helps compare activity; it does not guarantee liquidity at your order size.

## 3. Read one row or card

Compare three values for your chosen contract:

* **Price:** its latest displayed price.
* **Change (1h):** its percentage move over a rolling hour.
* **Volume (1h):** an hour of turnover from completed five-minute candles.

Price change and turnover describe different things. A large move alone does not show how much was traded. A dash means the value is unavailable, not zero. Use the [Column reference](../screener/column-reference.md) when you need a definition.

## 4. Open the chart

On a computer, click the ticker text. On a phone, tap the market card. Compare the displayed move with the chart: is price continuing in one direction, reversing or moving within a range?

The chart helps you investigate the row. It does not turn a filter result into a trade recommendation. Return to the screener when you have checked the symbol and timeframe.

## 5. Create one alert

First [connect Telegram](connect-integrations.md). Then open the screener's bell button and choose **Create New Alert**.

1. Name it **Hourly move check**.
2. In **Change**, select **1h**, choose **>** and enter `3`.
3. Check that the form reads your number as `3`, then save.
4. Confirm that the alert appears in your list and is active.

This example asks for a message when a contract's rolling hourly change exceeds +3%. **It checks the supported market list, not just the contract you opened.** Several matching contracts can produce several messages. It is an exercise, not a recommended entry condition. Pause it after the exercise if you do not want ongoing notifications.

## 6. Check delivery

Open [Integrations](https://app.erkescan.com/integrations), confirm that Telegram is connected and use **Test Telegram bot**. Check the linked Telegram chat for the test message.

A successful test confirms that the bot can reach this chat at that moment. Your saved alert sends a separate message only when its conditions match and its repeat interval allows it; saving alone does not send a signal. You can close the browser while custom alerts run.

If the test fails, check the connection and whether you blocked the bot, then follow the [Telegram guide](../integrations/telegram-bot.md). If the test arrives but an alert does not, use [Alert troubleshooting](../faq/technical.md).

**Done:** you have inspected a market, opened its chart, saved an alert and checked the delivery channel. Next, adapt an [alert recipe](../alerts/alert-recipes.md) to your own research question.
