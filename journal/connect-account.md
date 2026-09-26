# Connect an account to the Journal

Open [Journal](https://app.erkescan.com/en/journal) and choose the option to connect or add an account. For an account already listed, open its Settings to repair the connection or replace its key. Creating a second journal for the same exchange account can duplicate the history in your combined view.

## Bybit: use a read-only key

1. Sign in to the Bybit account or subaccount whose history you want to import. Open **API Management → Create New Key**.
2. Choose **Read-Only**. Follow the Journal's current permission instructions: select the offered reading scopes and leave withdrawals disabled. Keep this key separate from the trading key used by Vertex.
3. In ErkeScan, select the correct environment. A Demo key belongs to Demo; it is not a Live key.
4. Paste the API key and API secret into the Journal connection form. Select the offered history period and press **Connect and import**.
5. Wait for the key check and import. Then open the Journal and confirm its account and update status.

The Journal only reads your account. Trading permission is unnecessary even if the connection can accept some broader keys with a warning. Use a separate read-only key to give the Journal only the access it needs.

The Bybit connection may offer an optional IP restriction. If you use it, copy the Journal's current displayed IP into that key's Bybit settings. If a key is already IP-restricted, the Journal's request must be allowed. **The Journal's IP instructions are separate from the full IP list required for copy trading.**

Never put your API secret into a note or send it to support. If the exchange rejected the key, read the reason before replacing it: an incorrect environment or account type will not be fixed by repeatedly pasting the same values.

## Hyperliquid: use your public wallet address

Choose Hyperliquid and paste the full public address of the wallet you trade with. It starts with `0x` followed by 40 characters. Use your main trading wallet's address, not an API wallet address.

No API secret, private key, recovery phrase or trading signature is required. A public address allows the Journal to read public trading data; it does not authorize trading or withdrawals.

Select the offered history range, then connect and import. Check that you selected the right wallet before interpreting an empty trade list. Hyperliquid Demo is not offered by this Journal connection.

## Prop challenges

Choose the prop-challenge option if you want to track a supported CFT challenge. Select the program, phase and size, and follow the Bybit Demo flow. Where offered, attach the challenge to an existing eligible personal Demo account to keep its history in one place.

Review the warning before replacing a key on an active challenge: provider rules may restrict key changes. Verify current challenge conditions with the provider; Journal tracking does not grant permission to change them.

## What to expect during the first import

Key verification usually takes seconds and an initial import may take a few minutes; the visible status is the reliable guide. The page updates as data arrives. The chosen history range and exchange API coverage limit what can be imported.

| Result | Next step |
| --- | --- |
| Connected; import running | Wait for completion or open the Journal while data arrives. |
| Connected; first import did not start | Retry the import or start it from account Settings. You do not need to reconnect the key solely for this. |
| Import paused | Read the message. When paused by the service, it can continue without leaving the page open. |
| Action needed | Complete the specific exchange action requested, then return. |
| Import status unavailable | The job may still be running. Check its status again before assuming it failed. |
| Import complete; no trades | Check the account, environment, selected period and whether it contains supported closed trades. An empty period is possible. |

After the first import, the Journal continues loading new supported history. Check update freshness, especially before comparing totals with the exchange. See [Review trades and fix missing data](review-and-troubleshoot.md).
