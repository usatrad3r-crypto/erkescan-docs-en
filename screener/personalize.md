# Make the screener your own

Open **Columns** above the table. The same panel also contains an **Alerts** tab. On mobile it opens as a bottom drawer.

## Visibility and order

The screener has 57 column definitions in twelve groups. The default layout shows 19. Symbol and Trend stay visible; the remaining 55 columns can be selected in the picker. Use:

| Control | Result |
| --- | --- |
| All | Show all available selectable columns, alongside Symbol and Trend |
| Defaults | Restore the default visibility |
| Core Only | Show Symbol, Trend, Price, Funding Rate, Open Interest, Change 5m, Change 1h, Volume 5m, OI Change 5m and OI Change 1h |
| Show All / Hide All in a group | Change the selectable columns in that group |
| Reset Column Order & Visibility | Restore both default visibility and default order |

The default 19 are Symbol, Trend, Price, RVOL 5m, Change 5m, Change 24h, Change$ 5m, Volume 5m, Bar Vol Δ% 5m, Ticks 5m, RetailHeat 5m, VDelta 5m, Volatility 15m, OI Change 5m, OI Change 1h, Funding Rate, BTC Corr 1h, Volume 1h and VDelta 1h.

Drag the header label sideways to reorder columns. The new order is saved on drop. Trend and Price are placed after Symbol when the layout loads. Use the small caret beside a header to sort; Trend has no sort. A quick filter initially sets its own order, and a later caret click can sort within that filter. Favourites remain in a separate block.

## What is saved

| Setting | Persistence |
| --- | --- |
| Favourites; visible columns; column order; row density | This browser's site storage |
| Tour completion and dismissed alert hint | This browser |
| Search; active quick filter; current sort | Reset on page reload |
| Custom alerts | Your account |

Clearing site data removes local preferences. Another device, browser or private session can start from defaults. Saving an alert does not save your current screen layout or favourites.

## Density, language and mobile

Choose **Compact**, **Default** or **Comfortable** for desktop row density. Pick the level that keeps labels and values readable for you.

The **EN | RU** switch changes the app language. Preference is remembered in the browser; it does not create a separate screener URL. RVOL, VDelta, RetailHeat, OI and BTC remain recognisable technical names. If an authentication dialog retains the previous language, reload it.

Mobile cards have a fixed set of fields, plus the active filter's relevant metric. Toggling desktop columns does not add fields to mobile cards. Search, quick filters, favourites and alert management remain available.

## Three example layouts

These are ways to organise information, not trading strategies.

1. **Price and activity:** start with Core Only, then add Change 15m, RVOL 5m, RVOL 15m, VDelta 5m and Ticks 5m. Compare the different time windows in the [column reference](column-reference.md).
2. **Hourly comparison:** start with Defaults; add Change 1h, RVOL 1h and Ticks 15m. Remove fields you do not use. RVOL 1h is an approximation based on trailing closed-candle volume and an hourly baseline.
3. **Longer context:** add Change 8h, Change 24h, Volume 24h, OI Change 1d and BTC Corr 1d. Change 8h is rolling; Volume 8h, VDelta 8h and the slow RVOL/Bar Vol fields use completed candles. The same label does not imply the same window type.

To replay the welcome tour, open [the screener with `tour=1`](https://app.erkescan.com/screener?tour=1).

Next: [Build your own screen](build-your-own-filters.md).
