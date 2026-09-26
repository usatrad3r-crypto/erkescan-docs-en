# Technical questions

## Why is the price different from my exchange?

The screener shows the last traded price of the Binance USDT perpetual. Your exchange may show a mark price, a spot market or another venue's order book. Compare the same contract and price type. Use the exchange where you trade to check executable prices.

## What does a dash mean? Can numbers be stale?

A dash means no usable value, not zero. Missing history or a missing baseline can cause it. During an update failure the application may retain the last usable snapshot, so visible numbers alone do not prove freshness. Check the connection status, update time where shown and any warning.

## The table stopped updating. What should I do?

Some completed-candle metrics remain unchanged between candle closes. Check the status and a live value before diagnosing a failure. If there is a stale-data warning, wait for recovery and reload once if needed. Check your connection; a repeated warning alone does not identify the cause. See [Screener troubleshooting](../screener/troubleshooting.md).

## Why is Bar Vol Δ negative? Why is Volume unchanged?

Short-window Bar Vol Δ compares an unfinished candle with a completed one, so elapsed time affects the comparison. It is not automatically evidence of a market-wide drop in activity. The 8h and 1d versions use completed candles.

Volume 5m uses a completed candle; Volume 15m and 1h combine completed five-minute candles. Other metrics have their own windows. Use the [Column reference](../screener/column-reference.md) instead of applying one timing rule to every Volume, VDelta or RVOL field.

## Why is the Trend line shorter after reloading?

Trend uses available history and samples collected in the current browser session. Reloading can shorten it. It is a scanning aid; open the contract's chart for historical analysis.

## Why did my columns or favourites disappear?

Column visibility and order, density and favourites are saved in this browser. They do not follow you to another device. Private browsing or clearing site data can remove them. Symbol and Trend always remain visible. See [Personalize the screener](../screener/personalize.md).

## Does switching language change the URL?

The screener remains at `/screener` when you use **EN | RU**. Journal pages use language paths such as `/en/journal` and `/ru/journal`. If a sign-in dialog retains the previous language, reload it.

## Does the screener work on a phone?

The table becomes market cards. Each shows Price, Change 15m, Change 1h, Volume 1h and Funding, plus the active filter's metric when needed. Tap a card to open its chart; the star toggles a favourite. The alert controls remain available. Desktop columns and mobile cards have different layouts.

## Why did my alert not arrive?

Check these in order:

1. The intended account has active access.
2. Telegram is connected and **Test Telegram bot** reaches the chat.
3. The saved alert is active and its values are correct.
4. Every condition matched the same contract, with usable data.
5. The repeat interval and delivery timing allowed a message.

A blocked bot or permanently unavailable chat can clear the connection. Temporary delivery errors do not by themselves mean it was removed: check the current status. A successful test confirms the channel at that moment, not that your alert conditions matched. Follow [Managing alerts](../alerts/managing-alerts.md).

## Why does a message differ from the row I saw?

The screen and alert engine can observe different snapshots. Brief conditions between checks may be missed, and messages can arrive later. Compare the same symbol, metric, window and observation time. Change 8h is supported; its name alone is not a reason for missing delivery.

## Must I keep the browser open?

Custom alerts run on the server. A separately activated copy-trading bot also continues when you close its tab. Closing a page is not a pause command. Browser-rendered views, including the live table and Trend, update while you use them.

## Can I use an API? Which browsers work?

These guides do not provide a public customer API for the screener. Describe any integration requirement to support. Use a current desktop or mobile browser; include its name and version when reporting a display or sign-in problem. Browser preferences remain local even when account access and alerts follow your sign-in.

## How do I report a bug or request a feature?

Send the page URL, interface language, steps, ticker or alert name, and time with timezone. Include the visible status and relevant screenshot area, with credentials and unrelated personal data hidden. See [Support](../reference/support.md).
