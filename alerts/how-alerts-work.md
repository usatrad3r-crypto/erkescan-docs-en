# How alerts work

A custom alert is a named set of numeric conditions. ErkeScan checks supported contracts and can send a Telegram message when every condition matches the same contract during one evaluation.

## Matching rules

Conditions use **AND**. There is one operator and one value per metric; the form does not support OR or two bounds on the same metric. `Change (1H) < 2` includes negative changes of any size. It does not mean that price is within ±2%.

Alerts scan the supported market universe. There is **no symbol selector**. Screener search, favourites and quick filters do not restrict an alert. A price threshold also does not identify one instrument. The available universe changes with listings and data availability; see [Data & coverage](../reference/data-and-coverage.md).

An alert checks the **current value against a threshold**. It is not a crossing detector. A condition already satisfied when you activate the alert can match at the next eligible check, and a continuously satisfied condition can match again after cooldown.

## Checks and cooldown

Active alerts are scheduled for evaluation periodically against a shared market snapshot. Scheduling, snapshot refresh and Telegram delivery are separate stages; there is no promise of delivery at a precise second. Brief conditions between evaluations may be missed.

After a match, repeat processing for the **same alert and same contract** is limited by a service cooldown. The standard configuration is 60 minutes; the form does not expose a cooldown setting. Another instrument or another alert has a separate cooldown.

Missing metrics, stale inputs, paused alerts, inactive access, an unavailable Telegram connection and service limits can prevent a message. A broad rule can match many instruments; processing limits and delivery queues mean that every match is not guaranteed an immediate message.

## Account and delivery

An active subscription and a linked Telegram account are required for working delivery. The account limit is **200 saved alerts**, including paused alerts. Edit or remove unused alerts if you reach the limit.

Custom alerts arrive through **@erkescanalert_bot**. They are distinct from premium strategy feeds: turning off one feed is not the same as pausing your custom alerts. Follow [Create an alert](create-an-alert.md) to link Telegram and check delivery before relying on a rule.

## Read a message

A message identifies the alert, the matched ticker, condition values and a timestamp. Use the timezone printed in the message rather than assuming your local timezone. Values may be rounded for display; the stored threshold is still in the metric's units.

**Alerts in Last 24H** is a per-user, per-symbol count based on recorded trigger activity across your alerts, including the current event. It is not a delivery receipt or a count for that alert alone. **Last Alert for** can repeat the current event time; it should not be interpreted as the previous alert's timestamp.

Chart links and buttons let you inspect the instrument and manage alerts. A chart image is best-effort and can be replaced by a text message. The accompanying chart uses a 15-minute interval independently of the condition's window; check the venue and indicators before comparing it with screener values. A chart from an external provider can use different sources or aggregation.

Messages may be delayed, truncated or dropped by delivery safeguards, including age limits. A notification records a matching observation, not a recommendation or a prediction of the next move.

Next: [Create an alert](create-an-alert.md).
