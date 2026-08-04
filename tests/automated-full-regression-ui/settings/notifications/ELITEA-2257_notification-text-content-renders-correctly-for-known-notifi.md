---
id: ELITEA-2257
title: "Notification text content renders correctly for known notification types"
priority: high
type: functional
module: settings-notifications
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id: [tests.ui.admin.test_notification_text_content.TestNotificationTextContent.test_notification_text_content_renders_correctly]
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1165
---

# ELITEA-2257: Notification text content renders correctly for known notification types

**Module:** settings-notifications · **Priority:** high · **Type:** functional

**Objective:** Verify that Notification text content renders correctly for known notification types. Success is confirmed when verify no notification row shows raw json, broken html, or "undefined" text.

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
| 2 | Verify at least one notification of each type is rendered correctly: | Condition holds as described. |
| 3 | Chat mention: "[User] mentioned you in [Chat link]" | Action completes without error and produces the expected UI state. |
| 4 | Chat participant added: "[User] added you to [Chat link]" | Action completes without error and produces the expected UI state. |
| 5 | Index success: "Index [index link] is successfully created: {\"indexed\": N}" | Action completes without error and produces the expected UI state. |
| 6 | Bucket retention warning: "Bucket [bucket link] will start deleting files in 24 hours according to its retention policy (files are removed based on each file's creation date; the bucket itself will remain)." | Action completes without error and produces the expected UI state. |
| 7 | Verify no notification row shows raw JSON, broken HTML, or "undefined" text | Condition holds as described. |

---

## Expected Final State

Verify no notification row shows raw JSON, broken HTML, or "undefined" text.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Notification text content renders correctly for known notification types.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
