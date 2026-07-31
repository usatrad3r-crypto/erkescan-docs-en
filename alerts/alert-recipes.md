# Alert recipes

Twelve ready-made alerts, each paired with the way you would hunt the same thing by hand in the screener. Every recipe gives you a starting threshold, the reason that number was chosen, and what to change when it turns out to be noisy.

They are the unattended half of the [screener recipes](../screener/recipes.md): the screener shows you the market now, these tell you when it changes while you are away. Where a recipe borrows a number, it borrows it from the [quick filters](../screener/quick-filters.md).

Build them in the alert form exactly as written — see [Create an alert](create-an-alert.md) if you have not used it yet. Remember that conditions are combined with AND, that each alert watches the whole market, and that a contract can only re-trigger the same alert once per cooldown window (60 minutes by default).

{% hint style="info" %}
Most recipes below include **Volume (1H)** `>` `500000` — 500,000 US dollars traded across the last 12 closed 5-minute candles. That is the same liquidity floor the screener uses to decide which contracts are liquid enough for its top-ten quick filters. Drop it and your alerts will keep matching contracts nobody can trade in size.

All thresholds are typed as bare numbers: percent for Change, OI Change and Funding Rate, US dollars for Volume, VDelta and Price.
{% endhint %}

## 1. Big hourly move, up

**Hunting:** a coin that has genuinely run in the last hour, the same thing the **Big Movers** quick filter shows you.

| Condition | Operator | Value |
| --- | --- | --- |
| Change (1H) | `>` | `3` |
| Volume (1H) | `>` | `500000` |

**Why 3:** the Big Movers filter uses exactly `|Change 1h| > 3`, so this alert reproduces on your phone what that chip shows on screen. Change (1H) is a true rolling 60 minutes, so the number means what it says.

**Too noisy:** raise to `5`, then `7`. On a strong trend day even `5` will fire on a dozen contracts.

## 2. Big hourly move, down

Same recipe mirrored. You need a second alert because one metric can only carry one operator.

| Condition | Operator | Value |
| --- | --- | --- |
| Change (1H) | `<` | `-3` |
| Volume (1H) | `>` | `500000` |

**Too noisy:** `-5`. During a broad market flush this one will fire on almost everything liquid at once — that burst is itself the information.

## 3. Flash drop

**Hunting:** a sudden air pocket, not a slow bleed. This is the **Flash Crash 5m** preset with a liquidity floor added.

| Condition | Operator | Value |
| --- | --- | --- |
| Change (5m) | `<` | `-3` |
| Volume (1H) | `>` | `500000` |

**Why −3:** the preset's own seed. Note the window: Change (5m) measures the move since the last 5-minute bar boundary, so early in a bar it is describing a handful of seconds. That is a feature here — it catches the drop while it is happening.

**Too noisy:** `-4` or `-5`. Adding **Volume (5m)** `>` `1000000` also helps, because it demands that the drop happened on real turnover rather than a thin wick.

## 4. Open-interest spike on a liquid contract

**Hunting:** positions being opened fast — the alert equivalent of the **OI Spike** quick filter.

| Condition | Operator | Value |
| --- | --- | --- |
| OI Change (1H) | `>` | `5` |
| Volume (1H) | `>` | `500000` |

**Why 5:** the OI Spike filter fires above +5% over an hour, growth only. Open-interest windows are elastic — the "1h" window is measured from the nearest sample around an hour ago — so treat it as roughly an hour.

**Too noisy:** raise to `8`. For a faster version use **OI Change (15m)** `>` `5`, which is the **OI Pump 15m** preset.

## 5. Open-interest unwind

**Hunting:** positions being closed or liquidated in bulk, which often marks the end of a move rather than the start of one.

| Condition | Operator | Value |
| --- | --- | --- |
| OI Change (15m) | `<` | `-5` |
| Volume (1H) | `>` | `500000` |

**Why −5:** the **OI Dump 15m** preset seed. Note that the OI Spike filter in the screener is growth-only, so this alert has no chip equivalent — it is genuinely extra coverage.

**Too noisy:** `-8`. Pair it with **Change (1H)** `<` `-2` if you only care about unwinds that come with a falling price.

## 6. Quiet accumulation

**Hunting:** open interest climbing while price stays flat — the pattern behind the **Accumulation** quick filter.

| Condition | Operator | Value |
| --- | --- | --- |
| OI Change (1H) | `>` | `3` |
| Change (1H) | `<` | `2` |
| Volume (1H) | `>` | `500000` |

**Why these numbers:** the Accumulation preset seeds `OI Change 1h > 3` with `Change 1h < 2`, and the screener's chip demands the same OI growth with price still inside ±1%. You cannot express a two-sided band on one metric in the alert form, so `Change (1H) < 2` is the closest single-sided version — it admits falling prices too.

**Too noisy:** raise OI to `5`, and tighten price to `< 1`.

**Watch out:** this alert will also match coins that are dropping while open interest builds. That is not the same setup; check the direction on the chart before reading anything into it.

## 7. Rich funding

**Hunting:** contracts where one side is paying meaningfully to hold its position — the **High Funding** quick filter.

| Condition | Operator | Value |
| --- | --- | --- |
| Funding Rate | `>` | `0.1` |
| Volume (1H) | `>` | `500000` |

**Why 0.1:** the High Funding chip uses `|funding| > 0.1`, and funding here is a percent per funding period, so `0.1` means 0.1%. Positive funding means longs are paying shorts, i.e. the long side is crowded.

**The mirror:** build a second alert with **Funding Rate** `<` `-0.1` for a crowded short side.

**Too noisy:** `0.15`, which is the level the Squeeze filter treats as extreme.

## 8. Longs squeezed

**Hunting:** the long side is crowded *and* price is already going the other way — the **Squeeze** quick filter, long-side half.

| Condition | Operator | Value |
| --- | --- | --- |
| Funding Rate | `>` | `0.15` |
| Change (1H) | `<` | `-1` |
| Volume (1H) | `>` | `500000` |

**Why these numbers:** the Squeeze filter requires funding beyond 0.15% *and* a move of more than 1% against the crowded side over an hour. Both legs matter — expensive funding on its own says nothing about direction.

**Too noisy:** deepen the counter-move to `-2` or `-3`.

## 9. Shorts squeezed

The mirror image, as a separate alert.

| Condition | Operator | Value |
| --- | --- | --- |
| Funding Rate | `<` | `-0.15` |
| Change (1H) | `>` | `1` |
| Volume (1H) | `>` | `500000` |

**Too noisy:** raise the counter-move to `2`. Negative funding is rarer than positive funding, so this alert is usually the quieter of the pair.

## 10. One-sided taker flow

**Hunting:** a five-minute candle where aggressive buying or selling dominated. The **Breakout** quick filter looks for the same thing, but it measures it as a ratio — VDelta divided by that candle's volume. An alert cannot divide one metric by another, so this recipe uses the raw dollar figure instead and is a coarser instrument than the chip.

VDelta sits behind **Show advanced fields (volatility, ticks, vdelta)** in the form.

| Condition | Operator | Value |
| --- | --- | --- |
| VDelta (5m) | `>` | read it off the screener |
| Volume (1H) | `>` | `500000` |

**Why no fixed number:** VDelta is signed US dollars for one closed 5-minute candle, so a sensible threshold on a major coin is orders of magnitude larger than on a mid-cap. Make the **VDELTA (5m)** column visible, sort it descending with the caret, and take the value sitting around the tenth row as your starting threshold.

**Too noisy:** double it. For the sell side, build the mirror with `<` and a negative number.

## 11. Turnover burst

**Hunting:** a single 5-minute candle that traded far more than that contract normally does.

| Condition | Operator | Value |
| --- | --- | --- |
| Volume (5m) | `>` | read it off the screener |

**Why no fixed number:** there is no relative-volume condition available to alerts, so this is an absolute dollar threshold and it will naturally favour the largest contracts. Sort the **VOLUME (5m)** column descending and pick a number a little above what the top of the list shows on a normal day.

**Too noisy:** raise it. If it fires on the same three majors every hour, that is the threshold telling you it is measuring size, not surprise — pair it with **Change (5m)** `>` `2` so it only speaks up when the turnover came with a move.

**Watch out:** Volume (5m) is one *closed* 5-minute candle, not a rolling five minutes.

## 12. Price-level watch

**Hunting:** a specific high-priced contract, or a whole tier of the market.

| Condition | Operator | Value |
| --- | --- | --- |
| Price | `>` | your level |

**Why it is unusual:** alerts have no symbol field, so a price threshold is the closest thing to a symbol filter — only contracts trading above that price can ever match. Set it high enough and effectively one contract qualifies.

**Watch out:** the cooldown applies per contract — 60 minutes by default — so this is a "tell me it crossed" alert, not a ladder. And because the universe includes roughly 140 tokenized stock and commodity contracts, a mid-range price level will match those as well as coins.

## How many alerts should you actually run?

The account limit is 200, and it is the same on every plan. That number is not the constraint — your attention is.

Each alert can fire on many contracts in the same pass, and each match is its own message. A loose alert during a volatile hour can produce dozens of messages before its per-contract cooldown catches up, and there is no guaranteed pacing on delivery, so a burst can arrive slightly delayed or bunched.

A workable rule: start with **three to five** alerts covering genuinely different questions — one momentum, one positioning, one funding, one liquidity-filtered catch-all. Run them for a week.

Then audit. Count how many messages each alert produced and how many you acted on. Anything you never acted on is either mistuned or measuring something you do not trade — tighten it or delete it.

{% hint style="warning" %}
The moment you start swiping alerts away without reading them, the system has stopped working. Fewer, tighter alerts beat broad coverage every time. And none of these recipes is an edge or a signal — they are attention filters. What you do after a message arrives, and how much you risk doing it, is entirely your decision.
{% endhint %}

**Next:** [Manage your alerts](managing-alerts.md) — editing, pausing, deleting, and what to do when an alert never fires or a message never arrives.
