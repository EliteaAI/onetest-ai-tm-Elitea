---
id: ELITEA-2837
title: "Schedule Card Time Converts to Viewer's Local Timezone — Not Creator's Timezone"
priority: high
type: functional
module: toolkits-indexes
status: draft
execution_type: manual
tags: [feat:indexer, feat:toolkits, eng:frontend, schedule, timezone]
requirements: [EliteaAI/elitea_issues#6296]
---
# ELITEA-2837: Schedule Card Time Converts to Viewer's Local Timezone — Not Creator's Timezone

**Module:** Toolkits & Indexes · **Priority:** High · **Type:** Functional

**Objective:** Verify that when User A schedules an index in their own timezone, User B (a different browser/OS timezone) viewing the same schedule card sees the time converted to their own local timezone — not User A's raw, un-converted time.

**Coverage:**
- Scheduled time is stored/derived with timezone information (not a naive local string)
- Schedule card time is converted per-viewer to the viewer's browser timezone
- Two users with different timezones see two different (but equivalent) displayed times for the same underlying schedule
- Next run date/time is also converted per-viewer, consistent with the scheduled time

## Preconditions

- Two user accounts (User A, User B) with access to the same project/index, on machines/browsers set to different timezones (e.g. User A: UTC+5, User B: UTC-5)
- A toolkit with an index that has scheduling capability

## Test Data

| Field | Value |
|-------|-------|
| User A timezone | UTC+5 |
| User B timezone | UTC-5 |
| Scheduled time (set by User A, in User A's local time) | 14:30 |
| Expected time shown to User B (converted) | 04:30 (same absolute instant, User B's local time) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As User A (UTC+5), navigate to Index Details → SCHEDULE section and configure a schedule for 14:30. | Schedule saved; card shows 14:30 in User A's own timezone. |
| 2 | As User A, reload the page and re-check the schedule card. | Time still shows 14:30, consistent with User A's own timezone. |
| 3 | As User B (UTC-5), navigate to the same Index Details → SCHEDULE section for the same index. | Schedule card is visible to User B. |
| 4 | Observe the scheduled time shown on User B's schedule card. | Time shown is converted to User B's local timezone (04:30), representing the same absolute instant — not a raw copy of "14:30". |
| 5 | Compare the "Next run" value shown to User A vs. User B for the same schedule. | Both "Next run" values represent the same absolute instant, each displayed in the respective viewer's own local timezone. |

## Expected Final State

The same schedule, viewed by two users in different timezones, displays two different clock times that represent the identical underlying scheduled instant, each correctly converted to the viewer's own local timezone.

## Pass/Fail Criteria

**Pass:**
- User B sees the scheduled time converted to their own local timezone, not User A's raw local time
- "Next run" is consistently converted for both viewers

**Fail:**
- User B sees the same raw time/offset that User A set, un-converted
- "Next run" is correct for one viewer but not the other
