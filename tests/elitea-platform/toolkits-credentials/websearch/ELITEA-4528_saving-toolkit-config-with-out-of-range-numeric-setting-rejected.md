---
id: ELITEA-4528
title: "Verify saving the toolkit Configuration page with an out-of-range numeric setting is rejected with a clean message"
priority: critical
type: functional
module: tavily-toolkit
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6981]
---

## Preconditions

- A Tavily toolkit open in edit mode, with a valid credential selected

## Test Data

| Field | Out-of-range value |
|-------|---------------------|
| Max Results | 50 (ceiling 10) |
| Per Run Call Cap | 0, then a negative number |
| Max Page Chars | An extreme large value, then 0 |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Set Max Results to 50 and click "Save" | Clean, understandable error message, not an internal/implementation-level message |
| 2 | Reload the toolkit after the failed save | Neither the invalid Max Results value nor any other pending edit persisted — the save was fully rolled back |
| 3 | Set Per Run Call Cap to 0, then to a negative number, and attempt to save each | Clean rejection with an understandable message both times |
| 4 | Set Max Page Chars to an extreme large value, then to 0, and attempt to save each | Clean rejection with an understandable message both times |

## Expected Final State

Toolkit-level numeric settings are confirmed to be validated server-side with a clean rollback on failure.

## Pass/Fail Criteria

**Pass:**
- Every out-of-range setting is rejected with a clean message
- The save is fully rolled back

**Fail:**
- An out-of-range value is saved
- A failed save leaves a partial/inconsistent state
