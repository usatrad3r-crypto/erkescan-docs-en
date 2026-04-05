# Custom Alerts

Custom Alerts let you define your own trading rules and get notified instantly via Telegram when market conditions match your criteria. There's no limit to how many alerts you can create.

## How Alerts Work

1. You define a condition (e.g., "OI Change 15m is greater than 5%")
2. ErkeScan continuously monitors all coins against your conditions
3. When any coin matches, you receive an instant Telegram notification
4. The notification includes the coin name, the metric value, and current price

Alerts run 24/7 — even when you're not looking at the dashboard.

## Creating an Alert

1. Go to **Alerts** in the web app sidebar
2. Click **Create Alert**
3. Choose a **metric** from the dropdown
4. Set a **condition** (greater than, less than, equals)
5. Enter your **threshold value**
6. Save the alert

That's it. The alert is immediately active and will trigger whenever any coin meets your condition.

## Available Metrics

You can create alerts on any of these 30+ metrics:

### Price & Change Metrics
- Change 5m, 15m, 1h, 8h, 1d (%)
- Absolute price change (USD)
- Price threshold

### Open Interest Metrics
- OI Change 5m, 15m, 1h, 8h, 1d (%)
- Total Open Interest value

### Volume Metrics
- Volume 5m, 15m, 1h, 8h, 1d
- Volume Change (USD and %)
- Relative Volume (compared to 24h average)

### Advanced Metrics
- Volatility (5m, 15m, 1h)
- Ticks / Trade Count (5m, 15m, 1h)
- Volume Delta (vDelta)
- Funding Rate
- Market Cap

## Alert Conditions

For each metric, you can set:

- **Greater than** — triggers when the metric exceeds your value
- **Less than** — triggers when the metric drops below your value
- **Equals** — triggers on an exact match

## Alert Strategy Examples

Here are some practical alert setups used by experienced traders:

### Catch Volume Explosions
> **Metric:** Relative Volume\
> **Condition:** Greater than 3.0\
> **Why:** A relative volume above 3x the daily average means something unusual is happening — often before a breakout.

### Detect Open Interest Surges
> **Metric:** OI Change 1h\
> **Condition:** Greater than 8%\
> **Why:** A sudden 8%+ increase in open interest in one hour signals a flood of new positions — major move likely incoming.

### Funding Rate Extremes
> **Metric:** Funding Rate\
> **Condition:** Greater than 0.08% (or Less than -0.08%)\
> **Why:** Extreme funding rates indicate overleveraged positioning — these conditions often resolve with a sharp move against the crowded side.

### High Volatility Spike
> **Metric:** Volatility 5m\
> **Condition:** Greater than 2%\
> **Why:** A 2%+ move in 5 minutes is exceptional for most altcoins — this catches flash moves early.

### OI Drop with Price Rise (Short Squeeze Detection)
> **Metric:** OI Change 15m\
> **Condition:** Less than -3%\
> **Why:** Falling OI during a price rise means shorts are being forced out — a classic squeeze pattern.

## Managing Alerts

From the Alerts page, you can:

- **Edit** any existing alert to change its conditions
- **Delete** alerts you no longer need
- **View** all your active alerts and their configurations

## Where Notifications Are Delivered

All alert notifications are sent to your **Telegram** via the ErkeScan bot. Make sure you've connected your Telegram account (see [Connect Telegram & Discord](../getting-started/connect-integrations.md)).
