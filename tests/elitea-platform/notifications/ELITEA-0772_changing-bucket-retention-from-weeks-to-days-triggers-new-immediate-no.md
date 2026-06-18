---
id: ELITEA-0772
title: "Changing Bucket Retention from Weeks to Days Triggers New Immediate Notification and Suppresses Old Weeks Schedule"
priority: high
type: functional
module: notifications
status: deprecated
execution_type: manual
tags: [feat:notifications, user_story:3414, feat:artifacts, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3414]
---
# ELITEA-0772: Changing Bucket Retention from Weeks to Days Triggers New Immediate Notification and Suppresses Old Weeks Schedule

**Module:** Notifications · **Priority:** High · **Type:** Functional

**Objective:** Verify that when a bucket's retention is changed from Weeks to Days, a new immediate Days notification is generated based on the updated expiration date, and the old Weeks-based notification schedule (5-day threshold) is suppressed — no stale notification fires at the old 5-day mark.

**Coverage:**
- Bucket created with Weeks retention generates no immediate notification (Weeks threshold = 5 days before expiry, not on creation)
- After changing retention to Days, an immediate notification appears reflecting the new expiration date
- New Days notification content is accurate (correct new expiry date, "in N days" text)
- Old Weeks-based notification does NOT fire at the 5-day-before-old-expiry mark after the retention change

## Preconditions

- Logged in to {{base_url}} as the bucket creator with `artifacts.buckets.create` and `artifacts.buckets.update` permissions
- Test environment supports date-offset simulation (to advance to the old Weeks 5-day threshold)
- Browser: Chrome (latest)

## Test Data

- Bucket name: `retention-change-test`
- Initial retention: Weeks, Value: 2 (creation date: March 30, 2026 → original expiry: April 13, 2026; old 5-day threshold: April 8, 2026)
- New retention: Days, Value: 7 (changed on March 30, 2026 → new expiry: April 6, 2026; immediate notification expected)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts. Click '+ Create Bucket'. Enter name: `retention-change-test`, Period Type: Weeks, Value: 2. Click Save. | Bucket `retention-change-test` is created with expiry April 13, 2026. No immediate notification is triggered (Weeks retention does not notify on creation). |
| 2 | Open the Notification Center (bell icon). Scan for any entry referencing `retention-change-test`. | No notification for `retention-change-test` is present — Weeks retention only notifies 5 days before expiry, not on creation. |
| 3 | Close the Notification Center. In the Artifacts sidebar, click the ⋮ icon next to `retention-change-test`. Click Edit. | Edit Bucket dialog opens showing current retention: Weeks, 2. Bucket name field is greyed out (read-only). |
| 4 | Change Period Type to Days. Change Value to 7. Click Save. | Dialog closes without error. Bucket remains in the sidebar. New expiry is now April 6, 2026. |
| 5 | Open the Notification Center immediately after saving. | A new notification for `retention-change-test` is present: '⚠️ Bucket retention-change-test will expire on April 6, 2026 (in 7 days). Consider extending retention or backing up important files.' |
| 6 | Verify the notification expiration date is April 6, 2026 (new Days-based expiry), not April 13, 2026 (old Weeks-based expiry). | Expiry date in the notification is April 6, 2026 — reflecting the new Days retention, not the old Weeks schedule. |
| 7 | Using date simulation, advance the environment date to April 8, 2026 — the point where the old Weeks notification would have triggered (5 days before the original April 13, 2026 expiry). Open the Notification Center. | No new notification appears for `retention-change-test` based on the old Weeks schedule. The only entry that exists is the Days notification generated in step 5 (or it may already be dismissed/expired). No stale Weeks-based notification fires. |
| 8 | Confirm the total notification count for `retention-change-test`: only the Days-based notification exists (if still present), and no Weeks-based '5 days before old expiry' notification has appeared. | Exactly the Days notification exists. No unexpected Weeks-schedule notification present. |

## Expected Final State

Exactly the Days notification exists. No unexpected Weeks-schedule notification present.

## Pass/Fail Criteria

**Pass:**
- Bucket created with Weeks retention generates no immediate notification
- After changing to Days retention, an immediate notification appears with the correct new expiry date (April 6, 2026)
- No stale Weeks-based notification fires at April 8, 2026 (the old 5-day-before threshold)

**Fail:**
- A notification fires immediately on creation of a Weeks-retention bucket (incorrect behavior)
- No new notification appears after changing retention to Days
- New notification shows old Weeks expiry date (April 13, 2026) instead of new Days expiry (April 6, 2026)
- A stale Weeks-based notification fires at the old April 8, 2026 threshold after the retention has been changed
