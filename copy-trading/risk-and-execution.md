# Risk and execution

{% hint style="warning" %}
**Connection-terms mismatch — September 26, 2026**

ErkeScan's consent page still states **10×** leverage, while the current public Vertex configuration uses **30×**. Until this mismatch is resolved, **do not confirm a new connection or proceed to start or restart the bot using this guide**. These instructions are published for reference and do not replace consent to terms that match the service's actual operation. Contact [support](https://t.me/ErkeScanSupportbot) to clarify the connection terms; never send API keys or secrets.

If your bot is already running, this notice does not pause it. To stop new entries, use **Pause** in ErkeScan; pausing does not close an existing position. Check your position and protective orders on Bybit.
{% endhint %}

The percentage you choose for Vertex is a **planned risk budget for one trade**. It is calculated from the available USDT balance checked on Bybit before that entry.

**Risk budget = verified available USDT × selected risk percentage.**

For illustration, 1,000 available USDT and a 1% setting give a 10 USDT risk budget. This is an explanation of the calculation, not a recommended balance or risk setting.

## Risk, position value and margin are different

The bot uses the risk budget and the distance from the entry to the signal's initial stop to calculate quantity, while accounting for applicable fees and exchange constraints. With the same risk budget, a closer stop generally implies a larger position and a more distant stop a smaller one.

The position's full value is its **notional value**. **Margin** is the collateral required by the exchange. **Leverage** affects the relationship between position value and required margin. None of these is the risk percentage selected in ErkeScan, and the bot does not simply multiply your selected percentage by leverage.

The leverage setting is prepared and checked by the bot. A usable account balance alone does not guarantee entry: minimum order size, quantity increments, available margin and other checks must also pass. A signal can be skipped when its required position cannot be opened within those constraints.

The dashboard's amount is based on its latest balance observation. Before a new entry the service checks the balance again, so deposits, withdrawals and funds used elsewhere can change the next trade's risk amount. There is no need to enter a fictional starting balance.

## From the signal to the close

**Entry.** Vertex acts on an eligible new source signal. Your actual fill can differ from the signal's displayed reference price because your order reaches the exchange later and liquidity changes.

**Initial stop.** The original signal's stop level is retained for the copied trade. A submitted order is not the same as confirmed protection. Check the dashboard's protection state and the actual Bybit orders.

**TP1 and break-even.** The original signal's TP1 is the reference for the break-even rule; it is not recalculated from each customer's fill. When the rule is triggered, the service calculates a stop from your actual entry and the relevant entry/exit trading fees, and moves it only when the exchange and safety checks allow. Do not assume that seeing TP1 touched on a chart means every customer's stop has already moved, or that TP1 necessarily closed half of your copied position.

**TP2.** The original signal's TP2 is the copied trade's take-profit target. Execution still depends on the live order and the exchange. Check Bybit for the remaining quantity and completed fills.

**Completion.** The service checks the exchange result and reconciles closed positions and remaining orders. A manual close on Bybit is also reconciled. Closing a copied trade manually must not create another entry from that same source signal; a genuinely new eligible signal can still open a later trade while the bot is active.

## Why your result can differ

Signal statistics describe the signal page's methodology and observation period. They are not your personal exchange statement. Your result also depends on when you connected, which signals your account could take, your risk setting, fill prices, fees, funding, partial fills and any manual actions.

“Break-even” describes the stop calculation, not a guarantee that the final net result will be exactly zero. Funding, slippage and the exchange's actual execution can still produce a difference. Likewise, an initial stop does not guarantee that loss is limited to the selected percentage during a market gap or technical failure.

For the authoritative account result, inspect Bybit's fills and account history. Use the [Journal](../journal/overview.md) to review imported closed trades and cash movements, while checking its import freshness and coverage.
