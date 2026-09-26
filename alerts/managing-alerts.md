# Managing alerts

Open **Alerts** from the account menu or the alert bell in the screener. Cards show saved rules and whether each is active or paused. Use descriptive names so a Telegram message can be traced back to its rule.

## Edit, copy, pause and delete

**Edit:** open the pencil action, change the name or conditions and save. This updates the selected alert. Check every condition you intend to retain: clearing a row removes it from the saved rule. Editing a paused alert does not by itself make it active.

**Copy:** use the copy action to prepare a new draft based on the selected alert. On the new Draft card, click the pencil to open the copied alert form. Review the copied name and conditions, rename it if useful and save to create a separate alert. Opening a copy draft is not the same as saving a new alert. Editing another alert remains a separate operation; check the form title and the resulting card after saving.

**Pause:** use the play/pause control. A paused rule remains saved and occupies one of the 200 account slots. Resume it when you want future checks. Changes and delivery queues are asynchronous; the status control is not a delivery-time guarantee.

**Delete:** use the bin action and confirm the browser prompt. Deletion removes the saved alert and conditions; there is no customer-facing undo or archive. Pause a rule if you may need it later.

When access expires, the service can pause active alerts. After access is restored, alerts paused by the subscription system can resume. **Alerts you paused manually remain paused.** Review the displayed state after a renewal or connection change rather than assuming every rule is running.

## Diagnose delivery in order

1. **Access:** confirm you are signed in to the intended account and have active access.
2. **Telegram:** confirm the connected account on Alerts or Integrations. Use **Connect Telegram**, follow its bot link and complete confirmation. A blocked popup has a fallback link. Return and run **Test Telegram Bot**; repeated testing is rate-limited.
3. **Rule state:** confirm the rule is active and the saved values are the values you intended. Read any delivery warning shown after saving.
4. **Conditions:** all must match on the same contract in one check. Compare equivalent screener units and windows. A missing required metric excludes that contract for the check.
5. **Cooldown and timing:** an already-notified alert-contract pair may be cooling down. A brief match between evaluations may be missed. Queues and service limits can delay or suppress messages.
6. **Freshness:** stale snapshots and unusable candle inputs can prevent evaluation. A screenshot of a current row does not reconstruct a past evaluation.

Change (8H) is a supported rolling condition; it should not be discarded as a frozen near-zero field. Volume 8H and VDelta 8H use completed candles and therefore change much less often.

## Common misunderstandings

| Situation | Explanation |
| --- | --- |
| Saved, but no Telegram linked | The form warns about delivery. Complete the connection and test it; successful saving alone is not enough. |
| The rule notified for an unexpected ticker | Alerts are market-wide; favourites, search and price thresholds do not select one symbol. |
| It notified again without a new crossing | Matching is level-based; an eligible match can repeat after cooldown. |
| The picture is missing | Chart images are best-effort; a text message can contain the same observation. |
| Funding or a large number looks wrong | Check the input locale and interpreted value. `50,000` has different meanings in English and Russian. |
| A save, pause or delete fails | Read the specific error. Check the session, access, rule existence and action rate limit before retrying. |

If the bot is blocked or the chat becomes unusable, reconnect when prompted. Manually disconnecting Telegram affects delivery beyond a single alert; use an individual rule's pause control when that is your intention. Reconnecting does not imply that every premium feed subscription is restored.

For support, provide the alert name, exact saved conditions, ticker, expected time with timezone, whether the Telegram test succeeded, and any visible error. Do not send credentials. There is no customer alert-event history in the current alert list, so preserve relevant Telegram messages and timestamps when diagnosing a past event.
