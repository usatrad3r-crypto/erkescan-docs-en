# Real-Time Screener

The Screener is the heart of ErkeScan. It's a live dashboard that displays real-time data for every futures trading pair across Binance, Bybit, and Hyperliquid — all on one screen.

Data streams directly to your browser with no page refreshes needed. Color-coded cells help you instantly spot unusual activity: green for bullish signals, red for bearish, with intensity scaling based on the magnitude of the move.

## Metrics Available

The Screener tracks 30+ metrics across multiple timeframes. Here's what each column means:

### Price & Change

| Metric | Description |
|--------|-------------|
| **Mark Price** | Current futures mark price |
| **Change 5m / 15m / 1h / 8h / 1d** | Percentage price change over each timeframe |
| **Change (USD)** | Absolute price change in dollar terms |
| **Volatility 5m / 15m / 1h** | Price volatility measurement for short timeframes |

### Volume

| Metric | Description |
|--------|-------------|
| **Volume 5m / 15m / 1h / 8h / 1d** | Total traded volume in each timeframe |
| **Volume Change %** | How current volume compares to previous period |
| **Relative Volume** | Current volume compared to the 24-hour average — values above 1.0 mean above-average activity |
| **vDelta (Volume Delta)** | The difference between buy and sell volume — positive means more buying, negative means more selling |

### Open Interest

| Metric | Description |
|--------|-------------|
| **Total OI** | Total open interest across exchanges |
| **OI Change 5m / 15m / 1h / 8h / 1d** | How open interest is changing over each timeframe |

### Other Metrics

| Metric | Description |
|--------|-------------|
| **Funding Rate** | The periodic payment between long and short holders — positive means longs pay shorts (bullish crowding), negative means shorts pay longs |
| **Ticks 5m / 15m / 1h** | Number of individual trade executions — high tick count with low volume can indicate retail activity |
| **Market Cap** | Total market capitalization |
| **BTC / ETH Correlation** | How closely the coin's price moves with Bitcoin or Ethereum |

## How to Use the Screener

### Sorting

Click any column header to sort the entire table by that metric. Click again to reverse the order. This is the fastest way to find outliers — for example, sort by "OI Change 1h" descending to find coins with the biggest surge in new positions.

### Favorites

Click the star icon (☆) next to any coin to add it to your favorites. Favorited coins appear at the top of the screener so you can always keep an eye on the pairs you trade most.

### Coin Detail Modal

Click on any coin name to open a detailed popup with:

- Interactive price chart
- Volume breakdown
- Open interest history
- Funding rate trend
- Key statistics

### Color Coding

The screener uses a heat-map style color system:

- **Bright green** = strong positive move or surge
- **Light green** = moderate positive
- **White/neutral** = normal range
- **Light red** = moderate negative
- **Bright red** = strong negative move or drop

The more intense the color, the more significant the data point is relative to normal conditions.

## Timeframes

Every volume and change metric is available across five timeframes:

- **5 minutes** — for scalpers and very short-term activity detection
- **15 minutes** — for intraday momentum shifts
- **1 hour** — the most popular timeframe for active traders
- **8 hours** — for swing trading and session-level analysis
- **1 day** — for daily trend and macro positioning

## Pro Tips

- **OI rising + price rising** = new longs entering → trend confirmation
- **OI rising + price falling** = new shorts entering → potential squeeze setup
- **OI dropping + price moving** = positions closing → move may be exhausting
- **High relative volume (>2.0)** with low price change = accumulation or distribution happening under the surface
- **Funding rate extremes** (above 0.05% or below -0.05%) often precede reversals as leverage gets flushed
