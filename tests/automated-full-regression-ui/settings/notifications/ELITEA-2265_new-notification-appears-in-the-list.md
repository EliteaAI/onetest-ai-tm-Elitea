---
id: ELITEA-2265
title: "New notification appears in the list"
priority: medium
type: functional
module: settings-notifications
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2265: New notification appears in the list

**Module:** settings-notifications · **Priority:** medium · **Type:** functional

**Objective:** Verify that New notification appears in the list. Success is confirmed when verify the bell icon in the top navigation shows the red unread marker dot.

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
| 1 | Navigate to Settings → Notifications and note the current notification count | Target page/section loads successfully. |
| 2 | Navigate to Toolkits and open a toolkit that has indexing capability | Target page/section loads successfully. |
| 3 | Trigger an index operation and wait for it to complete | Action completes without error and produces the expected UI state. |
| 4 | Navigate back to Settings → Notifications | Target page/section loads successfully. |
| 5 | Verify a new notification appears at the top of the list confirming the index was created | Condition holds as described. |
| 6 | Verify the new notification is in unread state | Condition holds as described. |
| 7 | Verify the bell icon in the top navigation shows the red unread marker dot | Condition holds as described. |

---

## Expected Final State

Verify the bell icon in the top navigation shows the red unread marker dot.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: New notification appears in the list.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
