# Glossary

Definitions describe observations and controls; they are not predictions. For formulas and complete windows, use [Column reference](screener/column-reference.md).

**Alert / Оповещение** — A saved AND rule evaluated across supported contracts; a match is not necessarily a new threshold crossing.

**Aggregate trade event / Агрегированное торговое событие** — An exchange-provided grouped trade event. It is not a unique trader, an order count or necessarily one execution.

**Accumulation / Накопление** — A quick-filter name for specified OI, price and RVOL conditions. It does not establish who is accumulating an asset.

**Bar Vol Δ$ / Δ% / Объём свечи Δ$ / Δ%** — The difference in quote turnover and its percent change from a baseline candle. Fast branches include an unfinished candle; 8h and 1d compare completed candles.

**Basis / Базис** — The difference between derivative and spot prices for a comparable underlying. There is no dedicated basis column in this screener.

**Big Movers / Движение** — Quick filter for absolute rolling hourly price change above 3%.

**Breakout / Пробой** — A quick-filter label combining low relative volatility, RVOL, turnover and taker-flow conditions. It is not confirmation of a future breakout.

**BTC correlation / Корреляция BTC** — Linear correlation of paired candle returns with BTC, from −1 to +1. Near zero does not imply statistical independence or prove a separate catalyst.

**Candle / Свеча** — Price and trade statistics for a fixed interval. A forming candle is incomplete; a closed candle has reached the end of its interval.

**Change % / Изменение %** — Percentage price change. The 5m, 15m, 1h and 8h fields use rolling references, sometimes approximate; 24h uses the rolling exchange ticker.

**Change$ / Изменение$** — Change in price per instrument unit, in quote currency. It is not your profit or the change in total market capitalisation.

**Chip / Быстрый фильтр** — One of the eleven preset filter buttons. One can be selected at a time; an explicit sort can then reorder its result.

**Cohort / Когорта** — The currently selected group in Charts. Membership is based on current rankings and may change.

**Cooldown / Кулдаун** — Service-controlled repeat limit for the same alert-contract pair. The standard configuration is 60 minutes, with no form control.

**Contract / Контракт** — The specific derivative identified by venue, ticker, quote currency and contract type. The same base name on another market is not necessarily the same instrument.

**Density / Плотность** — The table row-spacing setting.

**Em dash / Прочерк —** — Unavailable data or an unusable baseline, not zero.

**Favourites / Избранное** — Locally stored marked instruments, displayed in a separate block when included by the active search and filter. They do not restrict alert scope.

**Funding rate / Ставка фандинга** — Percentage funding rate for a contract settlement period. Positive: longs pay shorts; negative: shorts pay longs. It is not annualised and does not count positions.

**High Funding / Высокий фандинг** — Quick filter for absolute funding above 0.1% per contract period.

**High Volume / Высокий объём** — Quick filter for RVOL 5m above 2; it ranks unusual relative volume rather than raw turnover.

**Liquidity / Ликвидность** — The ability to transact at available prices and size. Observed turnover is only one proxy; it does not establish spread or executable depth.

**Liquidity floor / Порог оборота** — An hourly quote-turnover inclusion rule, 500,000 USDT for the top filters and chart groups. Other inclusion rules can also apply.

**Mark price / Марк-прайс** — The exchange reference price used for specified derivatives calculations. It differs from last trade; read the exchange specification for its uses.

**OI Spike / Скачок OI** — Quick filter for OI Change 1h above 5%; positive change only.

**Open interest / Открытый интерес** — Outstanding open contract quantity. The screener displays its quote-currency valuation at current price. Dollar OI can rise solely because price rises. OI Change % compares quantities.

**Percent / Процент** — A relative amount per hundred. Enter 3 for a 3% alert threshold.

**Percentage point / Процентный пункт** — An absolute difference between percentages: 0.01% to 0.02% is +0.01 percentage points and +100% relative change.

**Percentile pNN / Перцентиль pNN** — A rank relative to the current usable sample, as with RetailHeat. It is not a probability of a price move.

**Perpetual / Бессрочный контракт** — A derivative with no scheduled expiration. Holding it remains subject to exchange rules, margin, funding and possible delisting.

**Premium / Премиум** — Active subscription access to the included product features; check the current plan and feature pages.

**Profit factor** — Gross realised profits divided by absolute gross realised losses for the stated trade sample and calculation method. A zero-loss sample needs separate handling.

**Profitable** — A strategy statistic for trades classified as profitable under that page’s calculation, including how partial exits are handled. Do not equate it with an independently defined win rate without matching methodology.

**RetailHeat (5m)** — A ratio of aggregate trade-event activity to quote turnover, with primary and smoothed paths. Differing input windows and aggregation prevent exact inference of order size or participant identity. An asterisk marks smoothing.

**Rolling window / Скользящее окно** — A lookback relative to the observation time, not necessarily the current candle boundary. Discrete references may make it approximate.

**RVOL / Относительный объём** — Turnover relative to a historical baseline, a multiple such as 2× rather than a percentage. 5m and 15m use completed candles; 1h has a mixed-series baseline.

**Sector tag / Секторный бейдж** — A descriptive category label; it does not establish listing status or legal ownership rights.

**Signal / Сигнал** — A published strategy event, separate from a user-defined numeric alert. Refer to the strategy methodology for entry, exit and result conventions.

**Snapshot / Снимок** — A combined dataset of the latest available inputs. Underlying timestamps can differ; the last usable snapshot may be retained during disruption.

**Squeeze / Сквиз** — In general, forced position closing under adverse conditions. The named quick filter only matches funding and opposing hourly price conditions; it does not verify forced closures.

**Stale / Устаревшие данные** — The app has not accepted sufficiently fresh data. Visible values can represent an earlier market state.

**Stock / commodity badge / Бейдж акции или товара** — Classification for a derivative linked to an equity, index or commodity. It does not mean ownership of a tokenized share or the physical underlying.

**Ticks / Тики** — Rolling count of aggregate exchange trade events for 5m, 15m or 1h. Not unique traders or individual executions.

**Top Active 10 / Топ-10 активных** — Up to ten eligible instruments ranked by Ticks 5m, with hourly turnover and primary RetailHeat availability gates. It is not a RetailHeat ranking.

**Top Gainers / Losers 24h / Топ роста / падения 24ч** — Up to ten qualifying directional movers over rolling 24h; minimum magnitude 1.5%, plus turnover and primary RetailHeat gates.

**Trend / Тренд** — A browser-built price sparkline with a target four-hour span. Short sessions can have shorter history; its colour compares the last and first available points.

**Universe / Набор инструментов** — The currently supported contracts, whose membership and count change. Use the live list, not a historical documentation count.

**USDT-quoted perpetual / Бессрочный контракт с котировкой USDT** — The contract type in this screener view. USDⓈ-M is a broader exchange category and does not by itself mean every contract is USDT-quoted.

**VDelta** — Taker-buy quote turnover minus taker-sell quote turnover for the stated window. It does not distinguish opening from closing trades.

**Volatility / Волатильность** — Sample standard deviation of candle open-to-close returns, in percent. The label is the candle size; the full buffer has 20 candles. It is not the average candle size.

**Volume / Объём** — Quote turnover. The 5m field uses one closed candle; 15m and 1h sum closed 5m candles; 24h uses the rolling ticker.

**Watchlist / Список наблюдения** — See Favourites. It is not a server-side symbol filter for custom alerts.

See also [Data & coverage](reference/data-and-coverage.md) and [How alerts work](alerts/how-alerts-work.md).
