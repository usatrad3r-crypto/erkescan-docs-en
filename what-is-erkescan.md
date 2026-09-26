# What ErkeScan does

ErkeScan helps you find markets worth investigating, receive notifications and use separate tools for execution and trade review. Each section answers a different question.

| Section | What you do there | Does it place trades? |
| --- | --- | --- |
| Screener | Compare price, volume, open interest, funding and other futures metrics | No |
| Custom alerts | Choose conditions and receive Telegram messages when they match | No |
| Signals | Read the track records and available live levels of Alpha Pulse, Vertex and Helix | No; receiving a signal does not execute it |
| Radar | Find a market move together with a news or event catalyst | No; a Radar card is not a trade with entry, stop and targets |
| Copy trading | Connect your Bybit account and explicitly activate Vertex execution | Yes, after connection and activation |
| Trading Journal | Review imported exchange trades using the Journal's connection instructions | No; the Journal uses a read-only connection |
| Charts | Compare cohorts using the screener feed | No |
| GEX | Read options-derived positioning and levels | No |

## Start with a market question

For example: “Which contracts have unusually high turnover?” Open the screener, try a quick filter, sort the relevant column, then open a contract's chart. The result is a shorter research list, not an instruction to enter a trade.

The screener covers Binance USDT perpetual futures. The available list changes as contracts are listed or removed; use the current table rather than a fixed count in a guide. A stock- or commodity-related perpetual is a derivative, not ownership of the underlying asset.

[Screener tour](screener/tour.md) · [Column reference](screener/column-reference.md) · [Data and coverage](reference/data-and-coverage.md)

## Signals and execution are separate

You can receive a strategy's signals in Telegram and choose whether to act on them manually. Switching on Telegram delivery does not start a trading bot.

The [Copy trading](https://app.erkescan.com/copy-trading) section provides automatic Vertex execution on a separately connected Bybit account. It requires your own connection and risk settings. **Helix Signals is available in the signal catalogue; Helix copy trading is still marked as preparing.** The availability of one does not imply availability of the other.

Do not reuse Journal instructions for copy trading: a read-only Journal key cannot place orders, while a trading connection requires the permissions listed on its own setup page. Enter credentials only in the appropriate secure application form, never in support chat.

## Before relying on a number

Check the metric's unit and measurement window. Different columns can use rolling windows, closed candles or the current unfinished candle. A dash means no usable value; it is not zero. If the screen warns that data is stale, confirm the current market on your exchange before making a decision.

Charts and published results describe observations under their stated methodology. They are not promises of a fill, a future return or the result of your own account.

## Language and access

The app supports English and Russian. Use **EN | RU**. Most pages keep their URL; Journal pages include the language in the path. Some product links and actions depend on your account's access. Check the product page for its current state instead of treating a visible link as proof that every action is enabled.

**Next:** [Create your account](getting-started/create-your-account.md).
