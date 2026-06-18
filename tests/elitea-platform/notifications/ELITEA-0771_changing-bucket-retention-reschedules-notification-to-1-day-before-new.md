---
id: ELITEA-0771
title: "Changing Bucket Retention Reschedules Notification to 1 Day Before New Deletion Date"
priority: high
type: functional
module: notifications
status: ready
execution_type: manual
tags: [feat:notifications, user_story:3414, feat:artifacts, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3414]
---
# ELITEA-0771: Changing Bucket Retention Reschedules Notification to 1 Day Before New Deletion Date

**Module:** Notifications · **Priority:** High · **Type:** Functional

**Objective:** Verify that when a bucket's retention policy is changed, the previously scheduled expiration notification is cancelled and a new one is scheduled for 1 day before the updated deletion date — ensuring no stale notifications fire for the old schedule.

**Coverage:**
- No notification fires on creation of a Weeks-retention bucket (notification is scheduled 1 day before expiry, not on creation)
- After changing retention from Weeks to Days, the scheduled notification is updated to 1 day before the new deletion date
- The old Weeks-based 1-day-before-expiry notification does NOT fire at the original scheduled date
- Only the new Days-based notification is present

## Preconditions

- Logged in to {{base_url}} as the bucket creator with bucket create/update permissions
- Test environment supports date-offset simulation
- Browser: Chrome (latest)

## Test Data

- Bucket name: `retention-change-test`
- Initial retention: Weeks, Value: 1

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts. Create bucket `retention-change-test` with retention: Weeks, Value: 1. Click Save. | Bucket created. Notification is scheduled for 1 day before the Weeks expiry (today + 6 days). No immediate notification appears. |
| 2 | Open the Notification Center. Scan for any entry referencing `retention-change-test`. | No notification for `retention-change-test` is present — notification only fires 1 day before deletion, not on creation. |
| 3 | In the Artifacts sidebar, click ⋮ next to `retention-change-test`. Click Edit. Change Period Type to Days, Value to 2. Click Save. | Bucket retention updated. New expiry is today + 1 day. No error shown. |
| 4 | Wait 1 day OR Using date simulation, advance the environment date to 1 day before the new Days expiry. Open the Notification Center. | Exactly 1 notification for `retention-change-test` appears. Message states files will start being deleted in 24 hours, bucket will remain. |
| 5 | Wait 13 days OR Using date simulation, advance further to +6 days (what would have been the old Weeks 1-day notification trigger). Open the Notification Center. | No new or stale notification fires for `retention-change-test` at the old Weeks schedule date. Only the Days-based notification (from step 4) exists. |

## Expected Final State

No new or stale notification fires for `retention-change-test` at the old Weeks schedule date. Only the Days-based notification (from step 4) exists.

## Pass/Fail Criteria

**Pass:**
- No notification on bucket creation
- After changing to Days retention, exactly 1 notification fires 1 day before the new deletion date
- No stale Weeks-based notification fires at the old 1-day-before-Weeks-expiry mark 

**Fail:**
- A notification fires on creation (before the 1-day threshold)
- No notification appears 1 day before the new Days deletion date
- A stale Weeks-schedule notification fires at the old trigger date after retention was changed
- New notification shows the old Weeks expiry date instead of the new Days expiry date
