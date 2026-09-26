# Trading Journal

The Journal imports your exchange history and helps you review completed trades, account equity and cash movements. It reads data; it does not place orders, close positions or start copy trading.

Open [Journal](https://app.erkescan.com/en/journal) in ErkeScan. Connect an account, wait for the initial import and check the update status before interpreting the numbers.

## What can be connected

For personal accounts, the current connection flow offers **Bybit** and **Hyperliquid**. Bybit supports the Live and Demo environments offered in the setup. Hyperliquid connects through the public address of the wallet you trade with and uses Live in the Journal.

Bybit history support is for the Unified Trading Account and linear USDT perpetuals. Do not assume the Journal includes every Bybit product, Spot trade or historical transaction simply because your account is connected. Binance is not currently offered in the new-account flow.

The prop-account flow provides CFT challenge tracking on Bybit Demo. It helps you follow the supported rules; it does not replace your provider's official account statement or decisions. Choose the correct program, phase and account size when connecting a challenge.

## Choose an account before reading the numbers

The account picker switches between one account and the combined view. **All accounts** combines the connected journals; it is not a separate exchange account. To change a connection or its settings, select the individual account first.

| Section | Use it for |
| --- | --- |
| Dashboard | Overall results, account equity, the review workflow and import freshness. |
| Trades | Find closed trades, filter the list and open an individual trade for review. |
| Equity | Inspect the account-value curve and drawdown for a chosen period. |
| Cashflows | Review deposits, withdrawals, fees, funding and other imported movements. |
| Calendar | Compare results and activity by day or month. |
| Settings | Rename an account, set its timezone, check the connection, replace credentials or remove the account from the Journal. |

## Three distinctions that prevent misleading conclusions

**Closed-trade P&L is not account equity.** A completed trade's result and the whole account's value answer different questions. Deposits and withdrawals can move account value without being trading profit or loss. Use Cashflows alongside Equity when investigating a change.

**The Journal's R has a specific definition: 1R = 1% of account equity at entry.** It is not automatically the trade's original stop-risk amount, your Vertex risk setting or the R methodology on a signal page. If entry equity or a usable P&L is missing, the Journal may leave R unavailable or exclude affected trades from an R total. This is missing evidence, not a zero result.

**An equity curve may contain reconstructed history.** Balance snapshots start when tracking begins. When the earlier curve is labelled reconstructed, it was calculated backwards from later data and does not include unrealized P&L or movements that were never imported. A single snapshot is also not a full history.

When the combined view warns that settlement assets are mixed, its USDT and USDC figures have been added without currency conversion. Use the individual accounts to inspect that limitation.

Continue with [Connect an account](connect-account.md) or [Review trades and fix missing data](review-and-troubleshoot.md).
