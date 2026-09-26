# GEX: how to read the screen

GEX shows estimated options gamma exposure for BTC and ETH: how it is distributed across price levels and which market regime the model describes. It provides additional context, not an instruction to buy or sell.

Open [GEX](https://app.erkescan.com/gex) from the app's top navigation. If you see an access prompt instead of data, check your signed-in account and the current plan terms.

## Your first two minutes

1. **Choose BTC or ETH.** Check that the page title shows the asset you intended to view.
2. **Check the age of the data.** It appears beside the price. The `60s` label is the usual refresh interval, not a guarantee that the displayed snapshot is always fresh.
3. **Read the regime.** In the model, positive gamma is associated with hedging that may dampen price moves; negative gamma with hedging that may amplify them. Neither predicts the next candle.
4. **Look at nearby levels.** Key Levels shows each level's price and its distance from the current price. The closest level is not necessarily the strongest.
5. **Open any unfamiliar label's explanation.** Select its card or information button. For a longer explanation, open Guide at the top right of GEX.

**Your result:** you know which asset you are viewing, how fresh the snapshot is, and what nearby markers mean. Viewing this page does not place trades.

## What the labels mean

| Label | Plain-language explanation |
|---|---|
| F — Gamma Flip | The estimated transition level between gamma regimes. It can move as the options market changes. |
| P1, P2 | Highlighted positive-gamma levels. They do not guarantee that price will stop there. |
| N1, N2 | Highlighted negative-gamma levels. They do not establish the direction of the next move. |
| A1, A2 — Magnet | Concentrations of interest identified by the model. “Magnet” does not mean price must reach the level. |
| S — Stability Zone | The price of maximum positive gamma in the calculated profile. |
| V — Max Volatility | The price of most negative gamma in the calculated profile. This is a metric label, not a promise of measured future volatility. |
| MP — Max Pain | An estimated options payout reference. It does not guarantee the expiry price. |

Colour and sign distinguish types of levels. They do not replace checking data freshness or reading the metric's explanation.

## Charts and gauges

**GEX by Strike** shows the distribution across options strike prices. **NET** shows the net estimate. The Gamma Regime, GEX Call/Put and GEX Above/Below gauges describe different aspects of the same snapshot. Their values are not the probability of a profitable trade.

The level-card filter switches between positive, negative, absolute and regime views. It changes the analytical display, not your account's trading settings.

## If data is stale or incomplete

When a stale-data warning appears, do not treat the remaining levels as current. Check your connection and reload the page. If a venue is marked unavailable, the snapshot may contain an incomplete set of sources.

If the problem persists, send [support](https://t.me/ErkeScanSupportbot) the selected asset, the time and time zone, and the warning text. Support does not need your API credentials or exchange access for this report.

## Learn more

The built-in [GEX guide](https://app.erkescan.com/gex/guide) contains examples, diagrams and level explanations. Numbers in learning examples are not current market levels.

Use the [screener](https://app.erkescan.com/screener) to find market activity and [Signals](https://app.erkescan.com/signals) to view strategy signals. GEX adds context to these tools and does not enable automated trading.
