# Screener tour

Open [the screener](https://app.erkescan.com/screener), sign in and check that your subscription is active. Each row describes one supported Binance USDT perpetual contract. The available list changes with listings, delistings and data availability.

## Find a contract

Type a ticker in **Search**. Search matches text inside the symbol, without regard to case. `btc` can match more than BTC; `usdt` matches the quote currency used by many rows. Clear the search to return to the complete list available under your active filter.

Select one of the eleven quick filters: **All**, **High Volume**, **OI Spike**, **Big Movers**, **High Funding**, **Accumulation**, **Squeeze**, **Breakout**, **Top Active 10**, **Top Gainers 1D**, **Top Losers 1D**. Only one filter can be active. Selecting a different filter replaces the previous one; **All** removes the quick filter. Search and favourites do not override its membership rules. [All filter rules](quick-filters.md).

The three top-ten filters first select their members from the whole available universe, then apply your search. Searching for a symbol while one is active does not create a new top ten from the search results.

## Sort and read a row

Click the small caret beside a header to sort; click again to reverse direction. The header label is the drag handle for reordering columns. **Trend** cannot be sorted. Selecting a quick filter restores its default order; a subsequent caret sort replaces that order while keeping the filter active.

Starred rows occupy their own block above other rows. Sorting works within these blocks. Rows without usable activity data appear in a separate subdued block under **All**. A dash in an individual cell means that value is unavailable, not zero.

The counter near the filters and the footer can count different sets: usable rows and filtered rows versus the full displayed list, including the no-data block. Clear search before comparing counts with the whole market.

## Change your layout

**Columns** opens the settings panel. Choose **All**, **Defaults** or **Core Only**, or toggle individual available columns. **Symbol** and **Trend** remain visible; they do not have hide controls. Drag headers to change the order of movable columns. Trend and Price return immediately after Symbol when the layout loads.

**Compact**, **Default** and **Comfortable** change desktop row density. Favourites, column choices, order and density are stored in this browser. They do not sync to another device. Search, the selected quick filter and the current sort reset on reload. [Personalise the screener](personalize.md).

## Open a chart or an alert

Click a ticker on desktop to open its TradingView chart. **Full Page →** opens the symbol page in a separate tab. Close the overlay with Escape, the close button or the backdrop. On mobile, tapping the card opens the symbol page; tapping its star only changes the favourite.

The **Alert** bell opens your saved alerts and the creation form. An alert checks the supported market, not the current search, quick filter or favourites. [Create an alert](../alerts/create-an-alert.md).

## Mobile and connection status

Below the desktop breakpoint, cards replace the table. Cards show Price, Change 15m, Change 1h, Volume 1h and Funding Rate, plus the active filter's sorting metric where applicable. Desktop column choices do not add fields to cards. The settings and alerts panels open from the bottom.

Check the footer status and any warning above the table. **Connected** with a green indicator means the stream is operating; a gold indicator with **Polling** means a fallback is supplying updates. **Stale** or **Error** means freshness needs attention. A healthy overall status does not certify every field of every contract. [Troubleshooting](troubleshooting.md).

The welcome tour runs once per browser. To replay it, open [the screener with the tour enabled](https://app.erkescan.com/screener?tour=1). Some steps are omitted when their target is not displayed.

Next: [Reading the table](reading-the-table.md).
