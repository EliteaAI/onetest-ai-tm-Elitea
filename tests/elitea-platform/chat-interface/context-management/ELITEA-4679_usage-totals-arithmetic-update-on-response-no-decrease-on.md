---
id: ELITEA-4679
title: "Usage Totals Arithmetic: Update on Response, No Decrease on Delete, Increase on Regenerate"
priority: high
type: functional
module: context-management
status: draft
execution_type: manual
regression: true
tags: [feat:context-management, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6898]
---

## Merge Note

Merges former draft cases "Usage totals update after every response" and "Deleting a message does not reduce usage totals; regenerating increases them" — both are assertions on the same cumulative Usage totals ledger.

## Preconditions

- User is logged in to `{{base_url}}`
- An active chat conversation with at least 3 message exchanges exists

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat` |
| Test message | Any short message, e.g. "Hello" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the chat and expand the Participants panel. | The Context management card shows a "Usage totals" section with Input tokens used, Output tokens used, and Approx. cost, distinct from the "latest call" Input used/Output used values shown above it. |
| 2 | Note the current Usage totals and, separately, the "Messages"/token count values. Send the test message and wait for the response to complete. | Immediately after the response, without reloading: Input tokens used, Output tokens used, and Approx. cost have all increased. |
| 3 | Hover/click the info icon next to Approx. cost. | Tooltip explains the estimate includes tool use, sub-agents, and summaries, and that deleting messages does not reduce the cost. |
| 4 | Delete the most recent message exchange. | The Messages/token count values drop immediately (consistent with existing ELITEA-0530 behavior), but the Usage totals values remain unchanged — they do NOT decrease. |
| 5 | Regenerate a response on a remaining message. Wait for completion. | Usage totals Input/Output tokens and Approx. cost increase after the regeneration completes. |
| 6 | If possible, stop a response mid-stream before it completes. | The tokens already consumed up to the stop point are still counted into the Usage totals (not discarded). |
| 7 | Collapse the Participants panel and open the ring's popover. | The same updated Usage totals values are shown in the popover as in the expanded card. |

## Expected Final State

Usage totals update immediately after every completed response (visible in both the expanded card and the popover), never decrease due to a message deletion, and increase on regeneration and on stopped-but-partially-consumed responses — while the separate live Messages/token count still drops on deletion as before.

## Pass/Fail Criteria

**Pass:**
- Usage totals increase immediately after a completed response, with no reload needed, and the tooltip text matches the documented explanation
- Messages/token count drops after deletion (unchanged existing behavior), while Usage totals remain the same or higher — never lower
- Usage totals increase after a regenerate action; a stopped mid-stream response still contributes its consumed tokens
- Popover shows the same values as the expanded card

**Fail:**
- Usage totals section is missing, conflated with the latest-call values, or fails to update after a response without a reload
- Usage totals decrease after a message deletion
- Usage totals do not increase after regenerating, or a stopped response's tokens are dropped
- Popover shows different/stale values compared to the expanded card
