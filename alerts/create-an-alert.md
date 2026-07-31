# Create an alert

This page walks through the alert form field by field, lists all 29 conditions with their real units and time windows, and shows how to pick a threshold that fires a few times a day instead of a few times a minute — or never.

## Before you start

Two things must be true before an alert can do anything.

You need an active subscription. The alerts page renders an upgrade panel instead of your alerts if your subscription is inactive or expired.

Your Telegram must be linked, because Telegram is the only delivery channel. You can build and save alerts without it — they simply sit idle and start working the moment the link exists. The path that actually links your chat is described in [Connect Telegram and Discord](../getting-started/connect-integrations.md).

## Where the button is

There are two ways into the same form.

**From the alerts page.** Open your account menu (your avatar, top right) and choose **Alerts**. The alerts page is not in the main navigation bar. On that page, press **Create New Alert**.

**From the screener.** Press the gold **Alert** bell button in the screener header. A panel opens with your alerts in it and a dashed **Create New Alert** button at the top. On a phone the same panel opens as a drawer from the bottom of the screen.

On a wide screen the form opens as a dialog in the middle of the page; on a narrow screen it slides up from the bottom. The fields are identical either way.

## Step by step

1. Press **Create New Alert**.
2. Type a **Name**, between 2 and 255 characters. The form says *Alert name must be at least 2 characters.* if it is shorter. Use something you will still recognise at 3 a.m., such as `OI pump, liquid only`.
3. Find the metric you want in one of the seven groups. Each metric is one row.
4. In that row, open the operator dropdown and pick one of `=`, `>`, `<`, `>=`, `<=`.
5. Type the threshold into the value box on the same row. Digits and a period only.
6. Repeat for any further conditions. They are combined with AND.
7. Press save. You will see **Alert created** / *Your alert is now active.*

The new alert appears in your list with an **Active** pill. From the next evaluation pass — within about 30 seconds — it is live.

{% hint style="info" %}
Leave a row's value empty and that metric is simply not part of the alert. You must set at least one operator-plus-value pair, or the form refuses with *Add at least one condition (operator + value) before saving.*
{% endhint %}

## The quick-start presets

Above the create button, the alerts page shows six one-click preset cards. Clicking one opens the form already filled in, and every value stays editable before you save.

| Preset | What it seeds |
| --- | --- |
| **OI Pump 15m** | OI Change (15m) `>` `5` — open interest up more than 5% |
| **OI Dump 15m** | OI Change (15m) `<` `-5` — open interest down more than 5% |
| **Big Mover 1h** | Change (1H) `>` `3` — price up more than 3% over the rolling hour |
| **Flash Crash 5m** | Change (5m) `<` `-3` — price down more than 3% inside the current 5-minute bar |
| **Extreme Funding** | Funding Rate `>` `0.05` — funding above 0.05% per funding period |
| **Accumulation** | OI Change (1H) `>` `3` **and** Change (1H) `<` `2` |

A preset is a first draft, not a calibration. Some of the seeds are looser than the screener's own quick filters — the **Extreme Funding** preset seeds 0.05%, while the screener's **High Funding** chip only lights up beyond 0.1%. Every value stays editable, and none of them knows anything about your risk or how many messages you want.

Note that no preset carries a liquidity floor, so each will match thin contracts until you add one yourself.

## The seven condition groups

There are exactly 29 conditions. The metric name tells you the candle size, which is not always the same thing as the look-back window — the table below gives the real one.

The names below are the labels the platform uses for these metrics, including in the alert message you receive.

### Change — percent

| Condition | What the number really measures |
| --- | --- |
| Change (5m) | The move since the last 5-minute bar boundary. It resets at every boundary, so ten seconds into a bar it describes ten seconds of market, not five minutes. |
| Change (15m) | Same behaviour, measured from the last 15-minute bar boundary. |
| Change (1H) | A true rolling 60 minutes: the live price against the price of the 5-minute candle closest to an hour ago. If no candle sits within 15 minutes of that target, the contract simply has no value for this metric and is skipped. |
| Change (8H) | See the warning below — do not build alerts on this one. |
| Change (24h) | A true rolling 24 hours from the live price against the price 24 hours ago. Not a calendar day. |

{% hint style="danger" %}
**Change (8H) is not usable as an alert condition.** The value an alert reads for it is captured a few seconds after each 8-hour bar opens and then held frozen for the rest of the bar, so it sits within a couple of percent of zero for practically every contract. An alert on it will almost never fire, and it does not match the **CHANGE (8h)** column you see in the screener, which reads a corrected value. Use Change (1H) or Change (24h) instead.
{% endhint %}

### OI Change — percent

The percentage change in [open interest](../glossary.md), offered as **OI Change (5m)**, **(15m)**, **(1H)**, **(8H)** and **(1D)**.

Open interest is sampled every five minutes, so these windows are elastic. **OI Change (5m)** can measure anything from about 2.5 to 10.5 minutes, **OI Change (15m)** from about 7.5 to 20.5 minutes, and **OI Change (1H)** from about 30 to 65 minutes. The longer windows stretch the same way. Read them as "roughly this window", never as an exact delta.

As a rule of thumb, rising open interest means new positions are being opened and falling open interest means positions are being closed or liquidated. It is a heuristic, not a measurement, and it never tells you which side opened them.

### Volume — US dollars

| Condition | Window |
| --- | --- |
| Volume (5m) | The last **closed** 5-minute candle only. Stable for the whole bar. |
| Volume (15m) | The sum of the last 3 closed 5-minute candles. |
| Volume (1H) | The sum of the last 12 closed 5-minute candles — a trailing hour that steps forward every 5 minutes. |
| Volume (8H) | The last closed 8-hour candle. |
| Volume (24h) | True rolling 24-hour turnover from the live ticker. |

All five are quote volume, i.e. US dollars traded, not coins traded.

### VDelta — signed US dollars

Taker buy volume minus taker sell volume, in US dollars. Positive means net aggressive buying, negative means net aggressive selling.

The windows mirror Volume exactly: **VDelta (5m)** is the last closed 5-minute candle, **(15m)** the sum of the last 3, **(1H)** the sum of the last 12, **(8H)** the last closed 8-hour candle, **(1D)** the last closed daily candle.

When a candle arrives without its taker-side breakdown, VDelta has no value at all for that contract rather than a zero — and a contract with no value for any metric your alert uses is skipped for that pass.

### Volatility — percent

**Volatility (5m)**, **(15m)** and **(1H)** are the standard deviation of the per-candle move across the last 20 candles of that size.

The label names the candle, not the window. The real look-back is roughly 100 minutes for 5m, roughly 5 hours for 15m and roughly 20 hours for 1h. A "Volatility (1H)" alert is therefore a statement about the last day of behaviour, not the last hour.

### Ticks — a whole number

**Ticks (5m)**, **(15m)** and **(1H)** count aggregated trade events over the trailing 5, 15 or 60 real-time minutes. This is a rolling wall-clock count, not a candle metric.

These are aggregated events, not individual fills, so the number is systematically lower than a raw trade count. Use it as an attention measure — how busy the tape is — rather than as an exact trade tally.

A genuinely quiet contract reads `0`. A contract whose trade feed has gone dead has no value at all, and is skipped rather than counted as zero.

### Others

| Condition | Unit and meaning |
| --- | --- |
| **[Funding Rate](../glossary.md)** | Percent per funding period, as published by Binance. Enter `0.01` for 0.01%, not `0.0001`. Positive means longs are paying shorts. It is not annualised, and the funding period is whatever that contract settles on. |
| **Open Interest** | Total open interest in **US dollars** of notional value. The form gives no unit hint, so this is the one people get wrong most often — `10000000` means $10M, not 10M contracts. |
| **Price** | Last traded price in US dollars. |

### Refresh caveat on the slow windows

The 5-minute, 15-minute and 1-hour candle data streams live. The 8-hour and daily candles are refreshed once per bar.

That means **Change (8H)**, **Volume (8H)** and **VDelta (8H)** can be up to about 8 hours old, and **VDelta (1D)** up to about 24 hours old. **Change (24h)** and **Volume (24h)** are unaffected — they come from the live 24-hour ticker.

### What you cannot alert on

RVOL, BTC correlation, Change$, Bar Vol Δ and RetailHeat exist as screener columns but are **not** available as alert conditions. If a recipe depends on relative volume, you have to approximate it with an absolute Volume threshold.

## The advanced fields toggle

**Volatility**, **Ticks** and **VDelta** — 11 of the 29 conditions — are hidden when the form first opens. They sit behind a toggle at the bottom labelled **Show advanced fields (volatility, ticks, vdelta)**.

Press it once and the three groups appear. If you open an existing alert or a preset that already uses one of those metrics, the section expands on its own.

Nothing about the toggle changes behaviour; it only reduces the size of the form for people who only ever use price, volume, open interest and funding.

## Operators

Five operators are available, shown as symbols in the dropdown: `=`, `>`, `<`, `>=`, `<=`.

`>` and `<` are strict. `>=` and `<=` include the threshold itself. In practice the difference almost never matters on live market data.

{% hint style="info" %}
`=` is not exact equality. It matches when the value is within about 0.01% of your threshold, and when your threshold is `0` it matches anything effectively equal to zero. Floating market data would never hit an exact match, so this tolerance is what makes `=` usable at all — but it still fires far less often than a comparison, and is rarely the operator you want.
{% endhint %}

## Typing the number

The value box accepts digits `0-9` and a period for decimals. Nothing else.

Do not type `%`, `$`, spaces or thousands separators. The form rejects them with *Invalid input. Please enter a valid number using digits (0-9) and a period (.) for decimals. Symbols like %, $, or commas (,) are not allowed.*

Write `5` for five percent, `-3` for minus three percent, `500000` for half a million dollars. `0` is a valid threshold, and an empty box means "this metric is not part of the alert".

## Choosing a threshold that fires occasionally

This is the whole game. A threshold that is too loose buries you; a threshold that is too tight is indistinguishable from a broken alert.

**Step 1 — decide your budget.** Pick a number of messages per day you will genuinely read. For most people that is a handful per alert, not dozens.

**Step 2 — look at today's market first.** Open the screener, make the matching column visible, and sort it descending with the small caret next to the header. Now you can see the actual distribution instead of guessing.

**Step 3 — count the rows that clear your candidate number.** Read down the sorted column. If forty contracts already clear it on a quiet afternoon, the threshold is too loose. If nothing clears it while the market is clearly moving, it is too tight.

**Step 4 — borrow the platform's own calibration.** The screener's quick filters use thresholds that were measured against the live universe, and they make good anchors:

- Big move over an hour: 3% on **Change (1H)**
- Open-interest spike over an hour: 5% on **OI Change (1H)**
- Rich funding: 0.1% on **Funding Rate**
- Extreme funding, crowded-side territory: 0.15% on **Funding Rate**
- Quiet build-up: **OI Change (1H)** above 3% while **Change (1H)** stays inside ±1%
- Liquid enough to be tradable: 500,000 US dollars on **Volume (1H)**

The chips test these as absolute values, in both directions. An alert condition cannot do that — one operator points one way — so a two-sided chip becomes two alerts, one with `>` and one with `<` and a negative number.

**Step 5 — always add a liquidity floor.** Without one, your alert will keep matching contracts nobody can trade in size. **Volume (1H)** `>` `500000` is the same floor the screener uses to decide which contracts are liquid enough for its top-ten filters.

**Step 6 — check it on a calm day and a wild day.** A threshold tuned on a Sunday will scream on the next Monday open. If your alert produces one message on a flat day, expect ten to twenty when the market actually moves.

**Step 7 — remember the window.** `Volume (5m) > 1000000` means one closed 5-minute candle traded a million dollars — it is not "a million dollars in the last five minutes of trading". Getting the window wrong is the most common reason a threshold behaves nothing like expected.

Then tighten. Editing is cheap, and an alert that fires twice a day and gets read beats an alert that fires forty times and gets muted.

## Worked example

Goal: know when traders are piling into a position on a contract that is actually liquid, before the price has run.

**1. Name it.** `OI pump, liquid only`.

**2. The trigger.** In the **OI Change** group, set **OI Change (15m)** to `>` `5`. Open interest up more than 5% in roughly the last quarter of an hour means new positions are being opened quickly. This is the same number the **OI Pump 15m** preset uses.

**3. The liquidity floor.** In the **Volume** group, set **Volume (1H)** to `>` `500000`. Both conditions must hold on the same contract, so this quietly removes everything too thin to trade.

**4. The "not already gone" filter.** In the **Change** group, set **Change (1H)** to `<` `2`. Open interest rising while price is still flat is a build-up; open interest rising after a 9% candle is usually chasing.

**5. Save.** The alert now reads: OI Change (15m) `> 5` AND Volume (1H) `> 500000` AND Change (1H) `< 2`.

**6. Watch it for a day.** If it is silent through an active session, relax the trigger to `>` `4` or drop the liquidity floor to `250000`. If it fires on twenty contracts in an hour, raise the trigger to `>` `8` and the floor to `2000000`.

**7. When it fires.** You get one message per contract with the ticker, the values that triggered it, and a 15-minute chart. Open the coin, check whether the move is still forming or already extended, and decide your entry, stop and size *before* you act.

{% hint style="warning" %}
This example is a way to organise attention, not a strategy. Open interest rising with flat price is just as capable of resolving downwards as upwards, and ErkeScan makes no claim about the outcome. Nothing here is financial advice — you decide the trade and carry the risk.
{% endhint %}

## What the form does not have

So you do not go looking for them: there is no symbol or ticker picker, no timeframe picker beyond the fixed per-metric windows, no one-shot-versus-repeating switch, no expiry date, and no channel selector. Telegram is the only destination, and the per-contract cooldown is not something you can set.

**Next:** [Alert recipes](alert-recipes.md) — ready-made alerts with starting thresholds and instructions for tightening them.
