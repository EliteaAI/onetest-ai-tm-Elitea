---
id: ELITEA-0777
title: "Bucket Expiration Notification Recipient Scoping — Immediate (Creator Only) vs Scheduled (All Team Project Users)"
priority: critical
type: functional
module: notifications
status: ready
execution_type: manual
tags: [feat:notifications, user_story:3414, feat:artifacts, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3414]
---
# ELITEA-0777: Bucket Expiration Notification Recipient Scoping — Immediate (Creator Only) vs Scheduled (All Team Project Users)

**Module:** Notifications · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that notification delivery recipients differ based on trigger type:
- Notifications triggered immediately at bucket creation (Days=1 retention, where 1-day-before = creation time) are delivered only to the bucket creator.
- Time-based scheduled notifications (triggered after a delay, e.g., Days=2+ retention) appear to be delivered to all users within the same Team Project.

Note: The scheduled notification scoping behavior (all team project users) is based on observed behavior and requires further verification by waiting for or simulating the scheduled trigger to fire.

## Preconditions

- Two test accounts available: User A (bucket creator) and User B (non-creator, same Team Project, at minimum Viewer role)
- Both users are members of the same Team Project in {{base_url}}
- Use separate browser profiles or one incognito window to maintain both sessions simultaneously
- Test environment supports date-offset simulation for the scheduled notification row
- Browser: Chrome (latest)

**Test Data:**

| Row | Bucket Name | Retention | Trigger Type | Expected Recipients |
|-----|-------------|-----------|--------------|---------------------|
| 1 | `scope-immediate-test` | Days = 1 | Immediate (fires at creation, since 1-day-before = creation time) | User A only (creator) |
| 2 | `scope-scheduled-test` | Days = 2 | Scheduled (fires 1 day before deletion, i.e., tomorrow) | All Team Project users (assumed — verify) |

## Test Data

- Bucket name: `creator-scope-test`; Retention: Days, Value: 1
- User A: bucket creator account
- User B: non-creator project member account (Viewer or Editor role)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in as User A. Navigate to Artifacts. Click '+ Create Bucket'. Enter name: `scope-immediate-test`, Period Type: Days, Value: 1. Click Save. | Bucket `scope-immediate-test` is created. An immediate notification fires (Days=1 means 1-day-before = creation time). |
| 2 | Open User A's Notification Center (bell icon). Locate the notification for `scope-immediate-test`. | Notification for `scope-immediate-test` is visible in User A's Notification Center. |
| 3 | Log out as User A. Log in as User B. Navigate to the same Team Project. Open the Notification Center. | User B's Notification Center opens. No notification referencing `scope-immediate-test` is present. |
| 4 | Press F5 to hard-reload the page as User B. Re-open the Notification Center. | Still no notification for `scope-immediate-test` after reload — immediate notifications are scoped to the creator only. |
| 5 | Log out as User B. Log in as User A. Navigate to Artifacts. Click '+ Create Bucket'. Enter name: `scope-scheduled-test`, Period Type: Days, Value: 2. Click Save. | Bucket `scope-scheduled-test` is created. No immediate notification appears (Days=2 fires 1 day before deletion, not at creation). |
| 6 | Wait 1 day OR use date-offset simulation to advance the environment to 1 day before `scope-scheduled-test` deletion. Log in as User A. Open the Notification Center. | Notification for `scope-scheduled-test` is visible in User A's Notification Center. |
| 7 | Log in as User B (same Team Project). Open the Notification Center. Scan for any entry referencing `scope-scheduled-test`. | Notification for `scope-scheduled-test` is also visible for User B — all Team Project users receive scheduled notifications (assumed behavior, verify here). |

## Expected Final State

Notification for `scope-scheduled-test` is also visible for User B — all Team Project users receive scheduled notifications (assumed behavior, verify here).

## Pass/Fail Criteria

**Pass:**
- Row 1 (immediate): Notification for `scope-immediate-test` visible for User A; NOT visible for User B before or after refresh.
- Row 2 (scheduled): Notification for `scope-scheduled-test` visible for both User A and User B after the scheduled trigger fires.

**Fail:**
- Immediate notification for `scope-immediate-test` visible for User B (non-creator).
- Scheduled notification for `scope-scheduled-test` not visible for User B after the trigger fires.
- Immediate notification does NOT appear for User A (creator) after bucket creation.
