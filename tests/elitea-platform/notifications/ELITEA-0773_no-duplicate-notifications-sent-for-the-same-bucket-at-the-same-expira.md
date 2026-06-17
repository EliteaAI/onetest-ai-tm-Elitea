---
id: ELITEA-0773
title: "No Duplicate Notifications Sent for the Same Bucket at the Same Expiration Threshold"
priority: high
type: functional
module: notifications
status: deprecated
execution_type: manual
tags: [feat:notifications, user_story:3414, feat:artifacts, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3414]
---
# ELITEA-0773: No Duplicate Notifications Sent for the Same Bucket at the Same Expiration Threshold

**Module:** Notifications · **Priority:** High · **Type:** Functional

**Objective:** Verify that the notification scheduler does not generate duplicate notifications for the same bucket at the same expiration threshold, even when the scheduler runs multiple times within the same threshold window.

**Coverage:**
- Exactly one notification per bucket per threshold after the first scheduler run
- No additional duplicate added when the scheduler runs again within the same threshold window
- The next scheduled threshold produces a new distinct entry (not a duplicate of the previous one)

## Preconditions

- Logged in to {{base_url}} as the bucket creator
- Test environment supports triggering the notification scheduler manually or via date-offset simulation
- Bucket `no-dupe-bucket` exists with Months, Value: 1; expiration approaching
- Browser: Chrome (latest)

## Test Data

- Bucket name: `no-dupe-bucket`; Retention: Months, Value: 1
- Threshold 1: 7 days before expiry ("1 week before" for Months retention)
- Threshold 2: 1 day before expiry ("1 day before" for Months retention)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Using date-offset simulation, advance the environment date to 7 days before `no-dupe-bucket` expiry. Trigger the notification scheduler (first run). | Scheduler runs without error. |
| 2 | Open the Notification Center. Count notification entries for `no-dupe-bucket` labelled 'in 7 days'. | Exactly 1 notification entry for `no-dupe-bucket` with text 'in 7 days'. No duplicates. |
| 3 | Trigger the notification scheduler a second time without advancing the date (still within the 7-day threshold window). | Scheduler runs again. |
| 4 | Open the Notification Center again. Count entries for `no-dupe-bucket`. | Still exactly 1 notification entry — no second duplicate has been added. |
| 5 | Using date simulation, advance to 1 day before `no-dupe-bucket` expiry. Trigger the scheduler. | Scheduler runs for the 1-day threshold. |
| 6 | Open the Notification Center. Look for a new 'in 1 day' notification for `no-dupe-bucket'. | A new distinct 'in 1 day' notification appears. The 'in 7 days' entry is still present as a separate entry. Total = 2 entries for `no-dupe-bucket`, each for a different threshold. |

## Expected Final State

A new distinct 'in 1 day' notification appears. The 'in 7 days' entry is still present as a separate entry. Total = 2 entries for `no-dupe-bucket`, each for a different threshold.

## Pass/Fail Criteria

**Pass:**
- Exactly one notification per threshold after the first scheduler run
- Re-running the scheduler within the same threshold window does not add duplicates
- Next threshold generates a new distinct entry

**Fail:**
- Two or more identical 'in 7 days' notifications exist after two scheduler runs
- 'in 1 day' notification does not appear as a separate distinct entry
