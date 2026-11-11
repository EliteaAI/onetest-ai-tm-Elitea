---
id: ELITEA-4686
title: "Old Chats Created Before This Release Show a Dash With Tracking Started Tooltip for Usage Totals"
priority: medium
type: functional
module: context-management
status: draft
execution_type: manual
regression: false
tags: [feat:context-management, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6898]
---

## Priority Note

Re-prioritized from High to Medium in QA lead review — display-only edge case for pre-release conversations with no functional risk.

## Preconditions

- A conversation exists that was created before this release and has no recorded `usage_totals`

## Test Data

| Field | Value |
|-------|-------|
| Legacy conversation | Created before this feature's release date, no `usage_totals` recorded |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the pre-release conversation with no usage totals. | Context management card renders without errors. |
| 2 | Inspect the Usage totals section. | Input tokens used, Output tokens used, and Approx. cost all display "—" (not 0, not an error). |
| 3 | Hover/click the relevant info icon. | Tooltip text similar to "Tracking started on <release date>" is shown. |
| 4 | Send a new message in this old conversation and wait for the response. | Usage totals now begin accumulating going forward from this point (new activity is tracked; no historical backfill is attempted or expected). |

## Expected Final State

Pre-release conversations show dash placeholders with an explanatory tooltip for historical usage, and begin tracking normally once new activity occurs.

## Pass/Fail Criteria

**Pass:**
- Usage totals show "—" (not 0 or an error) for a pre-release conversation with no history
- The "Tracking started on <date>" tooltip (or equivalent) is shown
- New activity in the old conversation begins accumulating totals going forward

**Fail:**
- Usage totals show 0 (implying data exists when it doesn't) or an error/crash
- No explanatory tooltip is shown
- New activity in the old conversation fails to start accumulating totals
