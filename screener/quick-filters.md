# Quick filters

Quick filters apply fixed numeric rules. A match means the rule is satisfied; it does not identify a profitable trade, a participant's identity or a confirmed liquidation.

## How they combine

Select one filter at a time. Conditions inside a filter are combined with AND; different filter buttons cannot be combined. Search narrows the selected set. Favourites must still satisfy the filter and search.

Selecting a filter clears the current sort and applies its default ordering. You can then click a column's caret to sort the matching rows differently. Choose **All** to remove the filter.

| Filter | All listed conditions must hold | Initial order |
| --- | --- | --- |
| All / Все | No quick-filter condition | Current manual sort / ручная сортировка |
| High Volume / Выс. объём | RVOL 5m > 2 | RVOL ↓ |
| OI Spike / Скачок OI | OI Change 1h > +5% | OI % ↓ |
| Big Movers / Движение | \|Change 1h\| > 3% | \|Change\| ↓ |
| High Funding / Выс. фандинг | \|Funding\| > 0.1% | \|Funding\| ↓ |
| Accumulation / Накопление | OI Change 1h > 3%; RVOL 1h > 1.5; \|Change 1h\| < 1% | OI % ↓ |
| Squeeze / Сквиз | \|Funding\| > 0.15%; Change 1h < −1% if funding is positive, or > +1% if funding is negative | \|Funding\| ↓ |
| Breakout / Пробой | 0 < Volatility 5m < market median; RVOL 5m ≥ 1.2; Volume 5m ≥ 50,000 USDT; \|VDelta 5m\| / Volume 5m > 0.20 | \|VDelta\| / Volume ↓ |
| Top Active 10 / Топ-10 активных | Shared eligibility gate; up to 10 highest Ticks 5m | Ticks ↓ |
| Top Gainers 1D / Топ роста 24ч | Shared gate; Change 24h ≥ +1.5%; up to 10 highest changes | Change 24h ↓ |
| Top Losers 1D / Топ падения 24ч | Shared gate; Change 24h ≤ −1.5%; up to 10 lowest changes | Change 24h ↑ |

An absolute value uses magnitude: −4% and +4% both clear a 3% magnitude threshold. `>` excludes the boundary; `≥` includes it. All funding thresholds are percent per contract funding interval: `0.1` means 0.1%, not 10%.

## Shared eligibility for the three top-ten filters

A contract needs Volume 1h of at least 500,000 USDT and a primary RetailHeat value. Primary RetailHeat requires a usable trade-event count and at least 50,000 USDT in the last closed 5m candle. Smoothed values marked `*` and missing values do not qualify.

Top Active ranks by **Ticks 5m**, not by RetailHeat. RetailHeat is an eligibility check and a separate descriptive metric. Top Gainers and Top Losers use rolling 24h price change. The top ten is selected globally before search, so search can leave fewer rows or none.

Other filters do not inherit the hourly volume threshold. Breakout has its own single-candle volume condition. These thresholds are selection rules, not guarantees of execution quality: turnover does not measure the order-book spread or depth.

## Why a filter can be empty

All required values must be available and all conditions must hold together. An empty filter may be normal. It does not prove that no squeeze, breakout or accumulation exists elsewhere; these are names for specific rules.

Breakout's median is calculated across usable positive Volatility 5m values in the supplied universe. The median can change even when a particular contract does not. Volatility 5m describes a buffer of 5m candle returns, roughly 100 minutes when full.

Funding identifies the payment direction. It does not reveal each position's leverage or entry. OI growth measures growth in open contracts; VDelta describes taker flow. Neither tells you whether a specific investor opened or closed a position.

If you want different numeric thresholds, use **All**, show the needed columns and sort them, then check your criteria manually. There is no saved custom numeric screener filter builder. [Build your own screen](build-your-own-filters.md).

Next: [Personalise](personalize.md).
