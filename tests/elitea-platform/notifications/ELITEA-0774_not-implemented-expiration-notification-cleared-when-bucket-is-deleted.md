---
id: ELITEA-0774
title: "[Not Implemented] Expiration Notification Cleared When Bucket Is Deleted"
priority: medium
type: functional
module: notifications
status: deprecated
execution_type: manual
tags: [feat:notifications, user_story:3414, feat:artifacts, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3414]
---
# ELITEA-0774: [Not Implemented] Expiration Notification Cleared When Bucket Is Deleted

**Module:** Notifications · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that when a bucket is deleted by its creator, any active expiration notification for that bucket is automatically removed from the Notification Center.

**Coverage:**
- Active expiration notification present before bucket deletion
- Bucket deletion via the ⋮ menu → Delete workflow completes successfully
- Notification for the deleted bucket is removed from the Notification Center after deletion
- Other buckets' notifications are unaffected (no collateral removal)

## Preconditions

- Logged in to {{base_url}} as the bucket creator with `artifacts.buckets.delete` permission
- Browser: Chrome (latest)

## Test Data

- Bucket to delete: `delete-clear-bucket`; Retention: Days, Value: 5
- Control bucket (must also exist): `control-bucket`; Retention: Days, Value: 10 (to verify no collateral notification removal)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts. Click '+ Create Bucket'. Create `delete-clear-bucket` (Days, Value: 5). Then create `control-bucket` (Days, Value: 10). | Both buckets appear in the Artifacts sidebar. |
| 2 | Open the Notification Center (bell icon). | Two notifications visible: one for `delete-clear-bucket` ('in 5 days') and one for `control-bucket` ('in 10 days'). |
| 3 | Close the Notification Center. In the Artifacts sidebar, click the ⋮ icon next to `delete-clear-bucket`. Click Delete. | Confirmation dialog appears: 'Deleting a bucket is a permanent action. All files and folders within the bucket will be deleted and cannot be recovered.' |
| 4 | Click the Delete button in the confirmation dialog. | `delete-clear-bucket` is removed from the Artifacts sidebar. No error shown. |
| 5 | Click the bell icon to open the Notification Center. | Notification Center opens. |
| 6 | Scan for any entry referencing `delete-clear-bucket`. | No notification for `delete-clear-bucket` is present — the entry has been removed. |
| 7 | Verify the notification for `control-bucket` is still present and unchanged. | `control-bucket` notification ('in 10 days') is intact and unaffected by the deletion of the other bucket. |

## Expected Final State

`control-bucket` notification ('in 10 days') is intact and unaffected by the deletion of the other bucket.

## Pass/Fail Criteria

**Pass:**
- Notification for `delete-clear-bucket` removed from Notification Center after deletion
- `control-bucket` notification remains intact

**Fail:**
- Notification for `delete-clear-bucket` still present after deletion
- `control-bucket` notification is also removed (collateral removal)
