---
id: ELITEA-2263
title: "Clicking a bucket retention warning link navigates to the correct bucket"
priority: medium
type: functional
module: settings-notifications
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.admin.test_notification_link_navigates_to_bucket.TestNotificationBucketRetentionLinkNavigation.test_bucket_retention_link_navigates_to_bucket
automation_pr: "https://github.com/EliteaAI/elitea-testing-public/pull/1788"
---

# ELITEA-2263: Clicking a bucket retention warning link navigates to the correct bucket

**Module:** settings-notifications · **Priority:** medium · **Type:** functional

**Objective:** Verify that Clicking a bucket retention warning link navigates to the correct bucket. Success is confirmed when verify the bucket page opens without a "not found" error.

---

## Preconditions

- User is logged in to the Elitea platform.


---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings → Notifications | Target page/section loads successfully. |
| 2 | Find a notification of type "Bucket [bucket link] will start deleting files..." | Action completes without error and produces the expected UI state. |
| 3 | Click the bucket link in the notification text | Control responds; expected next state is shown. |
| 4 | Verify the browser navigates to the referenced artifact bucket | Condition holds as described. |
| 5 | Verify the bucket page opens without a "not found" error | Condition holds as described. |

---

## Expected Final State

Verify the bucket page opens without a "not found" error.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Clicking a bucket retention warning link navigates to the correct bucket.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
