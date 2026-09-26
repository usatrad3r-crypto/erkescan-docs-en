# Vertex copy trading

Vertex copy trading can open and manage trades automatically on your connected Bybit account. You choose the risk per trade, connect a dedicated account and explicitly start the bot. Funds remain on Bybit.

Open [Copy trading](https://app.erkescan.com/copy-trading) in ErkeScan. Vertex is available; Helix copy trading is still in preparation. A Helix signal page or Telegram subscription does not activate a Helix trading bot.

## What the bot does

For an eligible new Vertex signal, the service checks your connection, available USDT, account settings and trading limits. It calculates the position from your saved risk percentage and the signal's stop distance, then sends the order to Bybit. It manages the trade's stop protection and take-profit order, including the break-even rule described in [Risk and execution](risk-and-execution.md).

Not every published signal becomes a trade on every account. A signal may be too old, an account may lack usable funds, a previous position may still need management, or another safety check may prevent entry. Your actual fills and results can differ from the signal page and from another customer's account.

## Before you start

You need an ErkeScan account with access to copy trading and a supported Bybit account. Use a dedicated Bybit subaccount and a separate API key for this bot. Keep other bots and discretionary trading on other accounts so their orders and positions do not interfere with Vertex's checks.

Copy trading requires trading permission. The **Journal** has a separate connection for reading history. A journal connection does not activate copy trading, and its recommended read-only key is not suitable for Vertex.

Follow [Connect Bybit](connect-bybit.md), then check the bot's status. **Waiting for a signal** is a normal result: a successful connection does not mean that a trade should appear immediately.

## What the dashboard tells you

The dashboard shows the selected account, whether new entries are enabled, the latest available-balance observation and risk estimate, and whether open positions have confirmed protection. Read the observation time: old data is not a current exchange balance.

For exact entry price, quantity, stop level and current orders, open Bybit. If ErkeScan cannot refresh its status, the bot may still be running. A status error does not pause it.

The bot runs on the server. Closing the page or signing out does not stop it. **Pause** stops new entries while existing positions remain under management. Deleting a connection is a separate action, available after trades and pending orders no longer need management. See [Controls and troubleshooting](manage-and-troubleshoot.md).

## Understand the risk

Futures trading can lose the full amount allocated to the account. A selected risk percentage describes the planned trade risk; it is not a guaranteed maximum loss. Slippage, gaps, exchange failures, fees and funding can change the outcome. Past signal performance does not promise future returns or your account's result.
