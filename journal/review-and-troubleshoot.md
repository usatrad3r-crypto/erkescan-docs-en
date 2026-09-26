# Review trades and fix missing data

A useful review starts with complete enough data. Select the correct account and period, then check the last successful import before drawing conclusions from P&L or a chart.

## A simple trade-review routine

1. Open **Trades** and narrow the list using the available filters. Confirm that you are looking at the intended account or the combined view.
2. Open a closed trade. Review its entry and exit details, realized P&L and execution timeline where available.
3. Add a note explaining what you saw, why you acted and what you would do differently. Add consistent tags, such as a setup name or a recurring mistake, so later comparisons are useful.
4. Save your changes. If another tab changed the same record, use the conflict dialog to review the versions. Returning to editing does not save the text automatically.
5. Continue through trades awaiting review, then compare the pattern with the Dashboard and Calendar.

Your notes and tags are journal annotations. Editing them does not change orders or the exchange's trade history.

## Read warnings before comparing results

**Partial history** means a position began before the available import window. Some entry details describe only the part the Journal could see. Where available, the exchange's realized P&L is used; do not assume the Journal observed the entire position lifecycle.

**P&L unavailable** means the exchange did not provide a usable result for that trade. A dash is not zero. The same principle applies to R when entry equity is missing.

**Reconstructed equity** is an estimate of the earlier curve, not a historical sequence of daily balance measurements. Check [Journal basics](overview.md) before using it to judge drawdown.

Compare the same account, dates and timezone when reconciling with Bybit or Hyperliquid. Inspect deposits, withdrawals, funding and fees in Cashflows; a cash movement and a closed trade can be presented in different sections. Do not add numbers together twice just because they appear in more than one view.

## If trades are missing

| What you see | What to check |
| --- | --- |
| First import running | Let it finish. Closed trades appear as supported data arrives. |
| Import finished; no trades | Verify the account/wallet, Live or Demo, date range, filters and whether trades are closed and within supported product coverage. |
| Data may be behind | Open the account's connection settings, check the last successful import and run the available sync action. |
| Exchange rejected the key | Read the reason in Settings. Correct the IP restriction, permissions or environment, or replace an expired key. |
| Connection not finished | Complete verification in that account's Settings instead of creating a duplicate account. |
| Key revoked / wallet disconnected | Reconnect through the existing account's Settings if you want to preserve its history in one place. |
| Account disabled by support | Contact support. Replacing the key does not remove that service-side restriction. |
| Import status unknown | Refresh the status. A read error does not prove that the import stopped. |

If the same account already has imported history, repair its connection from Settings. Adding the same account again can cause duplicate history in the combined view.

## Replace access without losing the journal

In the individual account's **Settings**, use the key or wallet-address section. For Bybit, create a new read-only key and enter both values; for Hyperliquid, enter the public trading wallet address. Use **Save and verify**, then check the result and subsequent import status. Replacement preserves the existing trade history.

If you fixed the existing key's permissions or IP restriction on Bybit, use the displayed **I fixed it — check again** action before creating another key. An active prop challenge may have additional restrictions on changing credentials; read its warning first.

## Remove an account

Use **Settings → Delete account** for the selected journal account. The confirmation explains that its stored key or wallet address is removed and imports stop; the account and journal disappear from your list.

The exchange account or wallet is not deleted, and no position is closed or funds withdrawn. A Bybit API key remains valid on Bybit until you delete it there. Removing a Journal account also does not stop a separately connected Vertex bot.

If removal was a mistake, contact support about restoring the journal; reconnecting credentials may be needed. Do not assume a newly created duplicate restores the same journal.

## Contact support with useful details

Include the product name, exchange, Live or Demo, selected dates and timezone, last successful import time, and the visible message. If one trade is missing, provide its symbol and approximate close time with personal details hidden. Never send API secrets, private keys, recovery phrases, passwords or 2FA codes.
