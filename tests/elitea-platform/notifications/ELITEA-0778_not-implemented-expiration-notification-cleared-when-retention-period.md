---
id: ELITEA-0778
title: "[Not Implemented] Expiration Notification Cleared When Retention Period Extended Beyond Warning Threshold"
priority: high
type: functional
module: notifications
status: deprecated
execution_type: manual
tags: [feat:notifications, user_story:3414, feat:artifacts, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3414]
---
# ELITEA-0778: [Not Implemented] Expiration Notification Cleared When Retention Period Extended Beyond Warning Threshold

**Module:** Notifications · **Priority:** High · **Type:** Functional

**Objective:** Verify that when a bucket's retention period is extended sufficiently to push the expiration beyond the current warning threshold, the active expiration notification is removed from the Notification Center.

**Coverage:**
- Active expiration notification present before retention extension
- Edit bucket dialog correctly updates Period Type and Value
- Notification removed from Notification Center after saving the extended retention
- Other unrelated notifications are unaffected

## Preconditions

- Logged in to {{base_url}} as the bucket creator with `artifacts.buckets.update` permission
- Test environment is at a point where `extend-clear-bucket` has 7 days remaining (Months retention, near threshold)
- Browser: Chrome (latest)

## Test Data

- Bucket name: `extend-clear-bucket`; Current retention: Months, Value: 1 (7 days remaining until expiry)
- New retention: Years, Value: 1
- Control notification: any other unrelated notification in the Notification Center (to verify no collateral removal)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Notification Center (bell icon). Confirm a '⚠️ extend-clear-bucket will expire ... (in 7 days)' notification is visible. | Notification for `extend-clear-bucket` is present with 'in 7 days' text. |
| 2 | Close the Notification Center. In the Artifacts sidebar, click the ⋮ (three-dot) icon next to `extend-clear-bucket`. Click Edit. | Edit Bucket dialog opens showing current retention: Months, 1. Bucket name field is greyed out (read-only). |
| 3 | Change Period Type to Years. Change Value to 1. Click Save. | Dialog closes without error. `extend-clear-bucket` remains in the sidebar. No error message shown. |
| 4 | Click the bell icon to open the Notification Center. | Notification Center opens. |
| 5 | Scan for any entry referencing `extend-clear-bucket`. | No notification for `extend-clear-bucket` is displayed — the previous 'in 7 days' entry has been removed. |
| 6 | Verify any other unrelated notifications that were present before are still visible and unaffected. | Other notifications are intact and unchanged. |

## Expected Final State

Other notifications are intact and unchanged.

## Pass/Fail Criteria

**Pass:**
- Notification for `extend-clear-bucket` is absent after extending retention to 1 year
- Edit dialog saves successfully with no error
- Other notifications unaffected

**Fail:**
- Notification for `extend-clear-bucket` still shows 'in 7 days' after retention extension
- Edit dialog returns an error on save
- Other notifications are erroneously removed
