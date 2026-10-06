---
id: ELITEA-2258
title: "Unread notifications are visually distinct from read notifications"
priority: medium
type: functional
module: settings-notifications
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2258: Unread notifications are visually distinct from read notifications

**Module:** settings-notifications · **Priority:** medium · **Type:** functional

**Objective:** Verify that Unread notifications are visually distinct from read notifications. Success is confirmed when verify the previously unread notification is now shown in read state (styling changed).

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
| 2 | Identify at least one unread notification (e.g., bold text or highlighted row) | Action completes without error and produces the expected UI state. |
| 3 | Verify unread notifications have a distinct visual style compared to read ones | Condition holds as described. |
| 4 | Click the notification row or open the linked entity | Control responds; expected next state is shown. |
| 5 | Navigate back to Settings → Notifications | Target page/section loads successfully. |
| 6 | Verify the previously unread notification is now shown in read state (styling changed) | Condition holds as described. |

---

## Expected Final State

Verify the previously unread notification is now shown in read state (styling changed).

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Unread notifications are visually distinct from read notifications.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
