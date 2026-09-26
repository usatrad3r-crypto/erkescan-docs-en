# Connect Bybit to Vertex

Open [Copy trading](https://app.erkescan.com/copy-trading) and select Vertex. Complete the account, API and risk steps below. Connecting the key and starting trading are separate operations; finish by checking the displayed bot status.

## 1. Prepare the account

Use a dedicated Bybit subaccount. Switch to that subaccount in Bybit **before creating its API key**: a key belongs to the account where it was created.

The current connection supports Bybit Global and Bybit Kazakhstan (`bybit.kz`); the platform is detected automatically. Bybit EU is not supported by this connection. Use the API settings on the platform where your account actually exists.

Vertex requires a Unified Trading Account (UTA 2.0) in **Cross margin** and **One-Way** position mode. Isolated margin, Portfolio margin and Hedge mode do not meet the current requirements. Prepare these settings on an empty dedicated account, not by changing a separate account's active trade.

The account must have usable own USDT in its Unified Trading Account, with USDT enabled as collateral. Borrowing, accrued interest, bonus or locked balances can prevent the service from verifying supported funds. Other assets are not counted as USDT. A small positive balance can still be insufficient for the exchange's minimum order size.

The bot prepares and checks leverage automatically. You do not choose a leverage multiplier in this setup.

## 2. Create a separate trading key

In Bybit, open **API Management → Create New Key**. Create a **Read-Write** key with **Contracts → Orders and Positions**. The Derivatives trade permission that Bybit adds with those contract permissions is expected.

Leave other permissions off: no withdrawals or transfers, and no Spot, Options, Earn, Exchange or unrelated permissions. A read-only key cannot run Vertex. Do not reuse the Journal key.

In ErkeScan, copy **all IP addresses shown for this connection**. Add that exact list to the key's IP restrictions in Bybit and save it. The list may change as the service assigns trading capacity, so copy it from the current connection page. Do not substitute your home IP or a list from an old screenshot.

Bybit may change the wording or layout of its API settings. The permissions and IP list matter more than where a checkbox appears. Bybit documents the distinction between read-only and read-write keys in its [API key reference](https://bybit-exchange.github.io/docs/v5/user/apikey-info).

## 3. Choose risk and connect

Choose **Risk per trade** in ErkeScan. This is a percentage of the verified available USDT balance, not the amount of margin to allocate. Read the explanation in [Risk and execution](risk-and-execution.md) before accepting the terms.

Paste the API key and API secret into the connection form. Confirm the required statements and submit. Never put the key or secret into a support message, screenshot or journal note.

Wait for the result. If the page says that the outcome is not yet known or verification is still running, use its status-check or recovery button. The key may already be saved. Repeatedly pasting the same secret is not a way to speed up verification.

If the IP list changes, save the new list in Bybit, return to ErkeScan and use the displayed retry action. For an already saved key, an IP correction normally does not require entering the key again. If the form explicitly says that the key was never saved or its fields were cleared, enter both values when requested.

## 4. Start and verify

Use **Start Vertex** or the combined **Check again and start Vertex** action shown by your setup flow. Check the selected account and the resulting status.

**Waiting for a signal** means the bot is ready for a future eligible entry. No immediate order is expected. You can close the page; the service runs on the server.

If connection succeeds but the bot cannot start, read the reason next to the status. Common causes include an incomplete IP list, unavailable USDT, account-mode restrictions, unavailable capacity or an access/subscription check. Follow [Controls and troubleshooting](manage-and-troubleshoot.md).

## Returning to an existing setup

Open the existing account or resume its unfinished connection. You do not need a second connection just because you changed browser or signed out.

The retry action checks the **saved** key. If you created a different key or switched to another Bybit account during an unfinished setup, use **Delete unfinished connection**, then enter the new pair. For a completed connection, use the normal connection-management flow after open trades and pending orders have settled.
