---
id: ELITEA-2259
title: "Mark selected notifications as read and unread using checkboxes"
priority: high
type: functional
module: settings-notifications
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2259: Mark selected notifications as read and unread using checkboxes

**Module:** settings-notifications · **Priority:** high · **Type:** functional

**Objective:** Verify that Mark selected notifications as read and unread using checkboxes. Success is confirmed when reload the page — verify the two notifications remain in unread state.

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
| 2 | Check the checkbox on two unread notifications | Condition holds as described. |
| 3 | Click the "Mark as read" button | Control responds; expected next state is shown. |
| 4 | Verify only the two checked notifications change to read state | Condition holds as described. |
| 5 | Verify all other notifications remain in their original state unchanged | Condition holds as described. |
| 6 | Reload the page — verify the two notifications remain in read state | Action completes without error and produces the expected UI state. |
| 7 | Check the checkbox on the same two notifications (now in read state) | Condition holds as described. |
| 8 | Click the "Mark as unread" button | Control responds; expected next state is shown. |
| 9 | Verify only the two checked notifications change back to unread state | Condition holds as described. |
| 10 | Verify all other notifications remain unchanged | Condition holds as described. |
| 11 | Reload the page — verify the two notifications remain in unread state | Action completes without error and produces the expected UI state. |

---

## Expected Final State

Reload the page — verify the two notifications remain in unread state.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Mark selected notifications as read and unread using checkboxes.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
