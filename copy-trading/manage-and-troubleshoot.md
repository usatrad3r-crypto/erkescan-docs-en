# Controls and troubleshooting

Start with the selected Bybit account, the bot status and the time of the last check. A page that cannot load current status does not tell you whether the exchange position has closed. Verify an open position directly on Bybit when needed.

## Pause, sign out, close or delete

| Action | What it does |
| --- | --- |
| Close the browser or sign out | Ends your viewing session. The server bot can continue trading. |
| Pause | Stops new entries. Existing positions remain under management. |
| Close a position on Bybit | Closes according to your exchange action; the service then reconciles that trade. It does not automatically pause future signals. |
| Delete connection in ErkeScan | Removes the saved connection and API credentials after no trade or pending order still needs management. It does not delete your Bybit account or its trading history. |

To stop taking new trades, press **Pause** and confirm the status changed. If a position remains open, inspect it and its stop on Bybit. A paused account with no position may show that checks are not running while paused; they run again when you start.

To end the connection, first pause new entries. Let existing trades finish or manage their close deliberately on Bybit. Wait for ErkeScan to confirm that positions and orders have settled, then use **Delete connection** under account access and connection. If deletion is blocked, do not treat it as completed.

Deleting or revoking the API key directly in Bybit removes the bot's access; it does not itself close an exchange position. Avoid using key deletion as a substitute for Pause or a close order. If access has already been revoked while a position is open, check the position and protective orders on Bybit and contact support.

## Read the status

| What you see | Meaning and next step |
| --- | --- |
| Waiting for a signal | Normal waiting. The bot does not promise a trade every day or copy an older signal simply because you just connected. |
| Starting / processing a signal | A check or entry is in progress. Allow it to finish; use the status refresh rather than repeatedly submitting credentials. |
| Position open / stop confirmed | A position is reported and its protection state is shown. Check Bybit for exact prices and quantities. |
| Protection pending | Stop protection has not yet been confirmed. Check Bybit promptly; contact support if the condition persists. |
| No available USDT | Verify that usable USDT is in the connected Unified Trading Account, then refresh the balance. A tiny positive amount may still fail minimum-order checks. |
| Balance stale / unavailable | The page does not have a current balance. Refresh it; do not treat the old estimate as proof of current buying power. |
| Daily entry, daily loss or open-position limit | New entries are blocked by a limit. Existing trades remain under management. Read the stated reason instead of repeatedly restarting. |
| Leverage preparation not confirmed | Vertex has not confirmed the required setting. It retries under its safety checks. Other positions or orders can prevent preparation; use a dedicated account and contact support if the problem persists. |
| Subscription required | Review your subscription/access. Existing-account status and reducing controls remain separate from permission to start new trading. |
| Source or service unavailable | New entries may be held. Refresh status and contact support if it persists; check any open trade on Bybit. |
| Control lost / status unknown | ErkeScan cannot confirm current account control or status. The bot may still be running. Check positions and stops on Bybit before assuming anything has stopped. |

A skipped signal is not automatically a service failure. Account restrictions, available funds, exchange size rules, safety checks or expired signal validity can prevent a particular entry.

## How do I change the saved risk?

The risk percentage is saved when you connect the account. The current dashboard shows it but does not provide an editor for changing that percentage on an existing connection. Refreshing the balance updates the estimated USDT risk amount, not the saved percentage.

If you need a different percentage, pause new entries and contact support about changing the setup. Do not delete a key or reconnect blindly while an open position still needs management. The **daily entry limit** is a different setting: pause, edit the limit under **Risk and bot settings**, then start again to save it.

## What if my subscription expires?

An expired subscription prevents new entries; it is not an instruction to close a position. Existing trade care remains available, as do existing-account status and reducing controls. Review the subscription message and renew access if you want new entries to resume. After renewal, check the actual bot status rather than assuming it has started.

## Fixing an IP or key problem

For an IP error, copy the current complete list from this account's connection page, save it in the key's Bybit IP restrictions and use **Check IPs and start** or the retry button shown. Do not remove IP restrictions to bypass the check. A changed server assignment can require an updated list.

For missing or excessive permissions, follow [Connect Bybit](connect-bybit.md). For an unknown result, read the saved state first. For an unfinished setup using an obsolete key, delete the unfinished connection before entering a replacement. Do not create duplicate setups to recover a slow response.

## What to send support

Send the product name, approximate time and timezone, the visible error text, and the step that failed. Describe whether a position is open and whether Bybit shows its stop. A redacted screenshot can help. Never send API keys, API secrets, passwords, recovery phrases or 2FA codes.
