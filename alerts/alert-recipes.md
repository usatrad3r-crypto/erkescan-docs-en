# Alert examples

These examples demonstrate the form's logic and units. Their thresholds are illustrative observations, not calibrated trading signals. They do not predict price direction or prescribe a position.

Each alert checks all supported instruments, including eligible contracts linked to traditional assets. There is no symbol selector. All conditions must hold on the same instrument. See [Create an alert](create-an-alert.md) for locale-aware numeric entry and the full condition reference.

| Observation | Conditions — all together | How to read |
| --- | --- | --- |
| Hourly rise | `Change (1H) > 3; Volume (1H) > 500000` | Positive rolling hourly price change |
| Hourly fall | `Change (1H) < -3; Volume (1H) > 500000` | Negative rolling hourly price change |
| Five-minute fall | `Change (5m) < -3; Volume (1H) > 500000` | Rolling five minutes, not the age of the current candle |
| OI increase | `OI Change (1H) > 5; Volume (1H) > 500000` | Increase in open quantity over an approximate hour |
| OI decrease | `OI Change (15m) < -5; Volume (1H) > 500000` | Decrease in open quantity; the cause is not identified |
| Rising OI, one-sided price bound | `OI Change (1H) > 3; Change (1H) < 2; Volume (1H) > 500000` | Also admits large negative price changes; not a ±2% range |
| Positive funding | `Funding Rate > 0.1; Volume (1H) > 500000` | Longs pay shorts at a rate above 0.1% per contract period |
| Negative funding | `Funding Rate < -0.1; Volume (1H) > 500000` | Shorts pay longs; this is not a count of short positions |
| Funding plus opposite price move | `Funding Rate > 0.15; Change (1H) < -1; Volume (1H) > 500000` | A joint observation; it does not confirm liquidations |
| Negative funding plus rise | `Funding Rate < -0.15; Change (1H) > 1; Volume (1H) > 500000` | The opposite signed observation |
| Positive taker-flow difference | `VDelta (5m) > X; Volume (1H) > 500000` | Choose X in quote currency; this is not RVOL or a ratio |
| Price band observation | `Price > P` | Choose P in quote currency; any matching instrument is eligible |

`X` and `P` are placeholders: replace them with a numeric threshold before saving. For a volume-only observation, use **Volume (5m) > X**; it measures turnover in one completed five-minute candle, not unusual turnover relative to that instrument's own history. RVOL is not available in the alert form.

## What these rules can and cannot reproduce

The Big Movers chip includes both directions; examples 1 and 2 split them into two alerts because a single metric cannot have OR conditions. The High Funding chip uses absolute funding; examples 7 and 8 split its signs. Adding Volume 1H >500000 changes the rule and excludes turnover equal to the threshold; the screener's top filters use an inclusive floor.

The Accumulation chip has a two-sided price bound and RVOL condition. Example 6 is not equivalent: the form cannot express that price range or RVOL. The Breakout chip uses a volatility median, RVOL and a VDelta/volume ratio; an absolute VDelta threshold cannot recreate it. Top Active and top-mover rankings cannot be represented by static market-wide alert conditions either.

The turnover condition is a selection aid. It does not guarantee a narrow spread, fill size or ability to exit. OI decline does not by itself identify liquidation, a completed move or an upcoming reversal. A funding sign gives payment direction, not a direct measure of who is crowded.

## Tune an observation without changing its meaning

1. Write the question you want answered, such as “which contracts currently meet this hourly change threshold?”
2. Read the matching screener columns with the same units and windows. Do not select a threshold solely to force a target number of messages.
3. Add one condition at a time and check that every condition is available and logically compatible.
4. Review messages over a representative period. Record which observation each message adds, then adjust or pause a rule that does not serve that question.

Remember the cooldown applies to each alert-contract pair. A rule can notify again after cooldown even if the value never moved back across the threshold. A wide rule can match many instruments, and service or Telegram limits can defer or prevent some deliveries. A high price threshold never guarantees a single-symbol alert.

Next: [Managing alerts](managing-alerts.md).
